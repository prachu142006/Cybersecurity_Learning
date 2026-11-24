# Day 17: Practical – Password Spraying Attack Detection Using Splunk

## 1. Lab Environment

| Component | Details |
|---|---|
| SIEM Tool | Splunk Enterprise |
| Splunk Version | 10.6.1 |
| Operating System | Windows |
| Data Source | Windows Security Event Logs |
| Sourcetype | WinEventLog:Security |
| Search Interface | http://localhost:8000 |

## 2. Practical Objectives

1. Search failed login events.
2. Identify multiple accounts from one source IP.
3. Compare successful and failed logins.
4. Detect multiple account failures within five minutes.
5. Generate simulated login events.
6. Count unique accounts from one IP.
7. Investigate successful logins after failures.
8. Visualize login activity using timechart.

---

## Practical 1: Search Failed Login Events

### Objective
To identify failed login attempts using Windows Security Event ID 4625.

### SPL Query

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| table _time Account_Name Source_Network_Address Logon_Type Failure_Reason
| sort -_time
```

### Explanation

- `index=*` – Searches available indexes.
- `sourcetype` – Selects Windows Security log events.
- `EventCode=4625` – Filters failed login events.
- `table` – Displays selected fields.
- `sort -_time` – Displays newest events first.

### Observation

Three failed login events were identified in the available Windows logs.

Observed details:

| Field | Observed Value |
|---|---|
| Event ID | 4625 |
| Account | PRACHITI$ |
| Source IP | 127.0.0.1 |
| Logon Type | 2 |
| Failure Reason | An Error occurred during Logon |

These events were generated during controlled testing.

127.0.0.1 is the loopback address representing the local system.

### Result
Successfully identified failed login events using Splunk.

---

## Practical 2: Identify Multiple Accounts From One IP

### Objective
To identify source IP addresses associated with failed login attempts against multiple accounts.

### SPL Query

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| stats count dc(Account_Name) as Unique_Accounts values(Account_Name) as Accounts by Source_Network_Address
| where Unique_Accounts >= 2
| sort -Unique_Accounts
```

### Explanation

- `stats` – Calculates statistics.
- `count` – Counts failed login events.
- `dc(Account_Name)` – Counts distinct account names.
- `values(Account_Name)` – Displays unique account names.
- `by Source_Network_Address` – Groups results by source IP.
- `where` – Displays IP addresses associated with at least two distinct accounts.

### Initial Observation

The initial query included the value `-` as an account.

The value `-` represents missing account information, not a valid username.

### Corrected SPL Query

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| where isnotnull(Account_Name) AND Account_Name!="-"
| stats count dc(Account_Name) as Unique_Accounts values(Account_Name) as Accounts by Source_Network_Address
| where Unique_Accounts >= 2
| sort -Unique_Accounts
```

### Observation

No results were returned.

The available real Windows events did not show failed login attempts against multiple valid accounts.

### Result
Successfully understood how to count distinct accounts and filter missing account values.

---

## Practical 3: Compare Successful and Failed Logins

### Objective
To investigate successful and failed authentication events.

### SPL Query

```spl
index=* sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)
| eval Login_Status=if(EventCode=4624,"Successful","Failed")
| stats count by Account_Name Login_Status
| sort Account_Name
```

### Explanation

- `EventCode=4624` – Successful login.
- `EventCode=4625` – Failed login.
- `eval` – Creates a new field.
- `if()` – Assigns Successful or Failed status.
- `stats` – Counts events for each account and status.

### Observation

The query compares successful and failed authentication events for each account.

### Result
Successfully learned how to compare authentication outcomes using Splunk.

---

## Practical 4: Detect Multiple Accounts Within Five Minutes

### Objective
To identify failed login attempts against multiple accounts from the same IP address within a five-minute interval.

### SPL Query

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| where isnotnull(Account_Name) AND Account_Name!="-"
| bin _time span=5m
| stats count dc(Account_Name) as Unique_Accounts values(Account_Name) as Accounts by _time Source_Network_Address
| where Unique_Accounts >= 2
| sort -_time
```

### Explanation

- `bin _time span=5m` – Groups events into five-minute intervals.
- `stats` – Calculates event counts and distinct accounts.
- `Unique_Accounts >= 2` – Filters intervals containing multiple accounts.

### Observation

No matching results were found in the available real Windows logs.

This was expected because the available events contained failed logins for only one valid account.

### Result
Learned how to investigate multiple account failures within a defined time interval.

---

## Practical 5: Generate Simulated Login Events

### Objective
To generate synthetic authentication events for understanding password spraying detection.

**Important:** These events are simulated inside Splunk. They are not actual Windows Security events.

### SPL Query

```spl
| makeresults count=6
| streamstats count
| eval Account_Name=case(
    count=1,"Rahul",
    count=2,"Priya",
    count=3,"Amit",
    count=4,"Sneha",
    count=5,"Neha",
    count=6,"Priya"
)
| eval EventCode=if(count=6,4624,4625)
| eval Source_Network_Address="185.100.20.10"
| eval Login_Status=if(EventCode=4624,"Successful","Failed")
| eval _time=relative_time(now(),"-".(7-count)."m")
| table _time Account_Name EventCode Source_Network_Address Login_Status
```

### Explanation

- `makeresults count=6` – Generates six synthetic events.
- `streamstats count` – Assigns sequential event numbers.
- `case()` – Assigns account names.
- `if()` – Makes the sixth event successful and the remaining five failed.
- `eval` – Creates source IP and login status fields.
- `relative_time()` – Assigns timestamps.
- `table` – Displays selected fields.

### Expected Observation

| Account | Event ID | Login Status |
|---|---|---|
| Rahul | 4625 | Failed |
| Priya | 4625 | Failed |
| Amit | 4625 | Failed |
| Sneha | 4625 | Failed |
| Neha | 4625 | Failed |
| Priya | 4624 | Successful |

All six events use the same simulated source IP address.

### Result
Successfully generated synthetic login events for password spraying analysis.

---

## Practical 6: Count Unique Accounts From One Source IP

### Objective
To count failed login attempts and distinct user accounts associated with one source IP.

### SPL Query

```spl
| makeresults count=6
| streamstats count
| eval Account_Name=case(
    count=1,"Rahul",
    count=2,"Priya",
    count=3,"Amit",
    count=4,"Sneha",
    count=5,"Neha",
    count=6,"Priya"
)
| eval EventCode=if(count=6,4624,4625)
| eval Source_Network_Address="185.100.20.10"
| where EventCode=4625
| stats count dc(Account_Name) as Unique_Accounts values(Account_Name) as Accounts by Source_Network_Address
```

### Explanation

- `where EventCode=4625` – Keeps only failed login events.
- `count` – Counts failed attempts.
- `dc(Account_Name)` – Counts unique accounts.
- `values(Account_Name)` – Displays affected accounts.

### Expected Result

| Field | Expected Value |
|---|---|
| Source IP | 185.100.20.10 |
| Failed Attempts | 5 |
| Unique Accounts | 5 |
| Accounts | Rahul, Priya, Amit, Sneha, Neha |

### Observation

Five different accounts received failed login attempts from the same simulated source IP.

This demonstrates a password spraying pattern.

### Result
Successfully identified five distinct accounts associated with one simulated source IP.

---

## Practical 7: Compare Failed and Successful Logins

### Objective
To investigate failed and successful login attempts for each account.

### SPL Query

```spl
| makeresults count=6
| streamstats count
| eval Account_Name=case(
    count=1,"Rahul",
    count=2,"Priya",
    count=3,"Amit",
    count=4,"Sneha",
    count=5,"Neha",
    count=6,"Priya"
)
| eval EventCode=if(count=6,4624,4625)
| eval Source_Network_Address="185.100.20.10"
| eval Login_Status=if(EventCode=4624,"Successful","Failed")
| stats count(eval(Login_Status="Failed")) as Failed_Attempts count(eval(Login_Status="Successful")) as Successful_Logins by Account_Name Source_Network_Address
```

### Explanation

- `eval` – Creates login status.
- `count(eval(...))` – Counts events matching a specific login status.
- `by Account_Name` – Groups events by account.
- `Source_Network_Address` – Groups results by source IP.

### Expected Observation

| Account | Failed Attempts | Successful Logins |
|---|---:|---:|
| Rahul | 1 | 0 |
| Priya | 1 | 1 |
| Amit | 1 | 0 |
| Sneha | 1 | 0 |
| Neha | 1 | 0 |

Priya has one failed login and one successful login.

This requires further investigation.

A successful login after a failed attempt does not automatically prove account compromise.

### Result
Successfully compared failed and successful authentication events for different accounts.

---

## Practical 8: Visualize Login Activity Using Timechart

### Objective
To visualize failed and successful login activity over time.

### SPL Query

```spl
| makeresults count=6
| streamstats count
| eval Account_Name=case(
    count=1,"Rahul",
    count=2,"Priya",
    count=3,"Amit",
    count=4,"Sneha",
    count=5,"Neha",
    count=6,"Priya"
)
| eval EventCode=if(count=6,4624,4625)
| eval Login_Status=if(EventCode=4624,"Successful","Failed")
| eval _time=relative_time(now(),"-".(7-count)."m")
| timechart span=1m count by Login_Status
```

### Explanation

- `makeresults` – Generates synthetic events.
- `streamstats` – Creates event numbers.
- `eval` – Assigns usernames and login status.
- `relative_time` – Creates timestamps.
- `timechart` – Groups events into one-minute intervals.
- `count by Login_Status` – Displays failed and successful event counts separately.

### Actual Lab Observation

The generated timeline showed:

| Time | Failed | Successful |
|---|---:|---:|
| 17:13 | 1 | 0 |
| 17:14 | 1 | 0 |
| 17:15 | 1 | 0 |
| 17:16 | 1 | 0 |
| 17:17 | 1 | 0 |
| 17:18 | 0 | 1 |

The chart displayed five failed login events followed by one successful login event.

**Note:** These timestamps are from the simulated Splunk dataset.

### Result
Successfully visualized authentication activity using Splunk timechart.

---

## 3. SOC Incident Investigation

### Scenario

A SOC Analyst observes five failed login attempts against different accounts followed by a successful login.

All attempts originate from the same simulated source IP.

### Investigation Steps

1. Check timestamps of failed and successful login events.
2. Identify the source IP address.
3. Identify all affected accounts.
4. Check whether the successful login was expected.
5. Investigate the device and login location.
6. Review unusual activity after successful authentication.
7. Check suspicious processes and network connections.
8. Contact the account owner when necessary.
9. Escalate or contain the incident if compromise is confirmed.

### Important Investigation Findings

- Multiple accounts received failed login attempts.
- The attempts originated from one simulated source IP.
- One account had a subsequent successful login.
- The pattern is suspicious and requires investigation.
- The simulated data does not prove a real account compromise.

---

## 4. Interview Question

**Question:**

If you are a SOC Analyst and observe five failed login attempts followed by one successful login, what would you investigate first?

**Answer:**

I would first check the timestamps and source IP address of the login attempts. Then I would investigate unusual activities after the successful login to determine whether the account was compromised.

---

## 5. Final Conclusion

In this practical, I learned how to investigate password spraying patterns using Splunk.

I performed the following activities:

- Searched Windows failed login events.
- Identified account names and source IP addresses.
- Counted distinct user accounts.
- Compared successful and failed logins.
- Grouped authentication events into time intervals.
- Generated synthetic login events.
- Visualized login activity using timechart.
- Studied SOC incident investigation procedures.

I also learned the importance of distinguishing real Windows Security logs from synthetic events.

Password spraying detection helps SOC Analysts identify suspicious authentication patterns and investigate possible unauthorized access.
