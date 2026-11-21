# Day 15 – Suspicious Login Patterns

## Environment
- SIEM Tool: Splunk Enterprise
- Log Source: Windows Security Event Logs
- Sourcetype: WinEventLog:Security
- Event IDs: 4624 and 4625

---

## Practical 1 – Hourly Successful Login Activity

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" EventCode=4624
| eval Login_Hour=strftime(_time,"%H")
| stats count by Login_Hour
| sort Login_Hour
```

### Observation
Highest activity:
- 20:00 – 392 events
- 18:00 – 361 events
- 17:00 – 330 events

### Conclusion
Login activity was highest around 17:00–20:00. Hourly activity alone cannot confirm suspicious behaviour.

---

## Practical 2 – Login Type Distribution

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" EventCode=4624
| stats count by Logon_Type
| sort -count
```

### Observation

| Logon Type | Count |
|---|---:|
| 5 | 1765 |
| 2 | 63 |
| 11 | 34 |
| 7 | 34 |
| 0 | 15 |

Logon Type 10 was not present in the returned results.

### Conclusion
Service logons (Type 5) were the most frequent in the selected dataset.

---

## Practical 3 – RDP Login Investigation

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" EventCode=4624 Logon_Type=10
| table _time Account_Name Account_Domain Logon_Type Source_Network_Address
```

### Observation
No results were returned.

### Conclusion
No successful RDP logon events (Type 10) were observed in the selected data and time range.

---

## Practical 4 – Source IP Analysis

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" EventCode=4624
| stats count by Source_Network_Address
| sort -count
```

### Observation

| Source Address | Count |
|---|---:|
| - | 1879 |
| 127.0.0.1 | 34 |

### Conclusion
Most events did not contain an available source address. The address 127.0.0.1 represents the local loopback address. No external suspicious IP was established from these results.

---

## Practical 5 – Account-wise Successful Login Analysis

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" EventCode=4624
| stats count by Account_Name
| sort -count
| head 10
```

### Observation
The results included:
- A machine account
- SYSTEM
- DWM accounts
- LOCAL SERVICE
- NETWORK SERVICE
- Splunkd
- A personal user account

The most frequent displayed account was the machine account.

### Conclusion
Windows system and service accounts also generate successful logon events. Not every login event represents a person manually entering a password.

---

## Practical 6 – Account-specific Logon Type Analysis

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" EventCode=4624
| search Account_Name="<YOUR_ACCOUNT>"
| stats count by Logon_Type
| sort -count
```

### Observation

| Logon Type | Count |
|---|---:|
| 11 | 34 |
| 7 | 34 |

### Conclusion
The selected account had 34 cached interactive logons and 34 workstation unlock events.

Note: Replace `<YOUR_ACCOUNT>` with the actual account value when running locally. Do not publish personal email addresses.

---

## Practical 7 – Successful vs Failed Login Comparison

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)
| eval Login_Status=if(EventCode=4624,"Successful","Failed")
| stats count by Login_Status
```

### Observation

| Login Status | Count |
|---|---:|
| Successful | 1915 |
| Failed | 1 |

### Conclusion
Successful logons were much more frequent than failed logons in this search result. Only one failed event was observed.

---

## Practical 8 – Login Activity Timeline

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)
| eval Login_Status=if(EventCode=4624,"Successful","Failed")
| timechart span=1h count by Login_Status
```

### Observation

| Time Bucket | Failed | Successful |
|---|---:|---:|
| 19:30 | 0 | 100 |
| 20:30 | 0 | 25 |
| 21:30 | 0 | 90 |
| 22:30 | 1 | 24 |

### Conclusion
One failed login event appeared in the 22:30 time bucket. No sudden increase in failed logins was observed.

---

## Practical 9 – Account-wise Login Correlation

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)
| eval Login_Status=if(EventCode=4624,"Successful","Failed")
| stats count by Account_Name Login_Status
| sort Account_Name
```

### Observation
The results showed:
- One failed event for the machine account.
- 1903 successful events for the same machine account.
- 1748 successful SYSTEM events.
- 68 successful events for the personal account.
- Other successful events for Windows service accounts and Splunkd.

### Conclusion
Account-wise correlation helped distinguish machine, system, service and user account activity. One failed event was observed for the machine account.

---

## Final SOC Investigation Conclusion

Based on the available Splunk search results:

1. Successful login activity was significantly higher than failed login activity.
2. Only one failed login event appeared in the successful-versus-failed comparison.
3. No successful RDP login was observed in the selected data.
4. Most source address values were unavailable (`-`), while 127.0.0.1 represented local loopback activity.
5. System and service accounts generated many events.
6. No clear brute-force pattern was identified in the investigated results.

### Learning Outcome

I learned how to:
- Analyse successful and failed login events.
- Identify different Windows Logon Types.
- Investigate RDP logins.
- Analyse source IP addresses.
- Compare account-wise login activity.
- Build login timelines using Splunk.
- Correlate authentication events.
- Write evidence-based SOC investigation conclusions.

**Important:** Event counts can differ between searches when time ranges or collected data change. These results represent the observations from the individual searches, not necessarily one identical time window.
