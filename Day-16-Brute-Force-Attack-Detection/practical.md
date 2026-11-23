# Day 16 – Practical

## Objective
To generate controlled failed login events and detect repeated login failures using Splunk.

## Practical 1 – Generate Failed Login Events
Generated three intentional failed login attempts on the local Windows system.

Event ID: 4625

## Practical 2 – Investigate Failed Logins

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| table _time Account_Name Logon_Type Source_Network_Address Failure_Reason
| sort -_time
```

Observed three failed login events.

## Practical 3 – Detect Repeated Failed Logins

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name Source_Network_Address
| where count >= 3
| sort -count
```

Result: Three failed attempts detected.

## Practical 4 – Successful vs Failed Login

```spl
index=* sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)
| eval Login_Status=if(EventCode=4624,"Successful","Failed")
| stats count by Account_Name Login_Status
```

Compared successful and failed login events.

## Practical 5 – Login Timeline

```spl
index=* sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)
| eval Login_Status=if(EventCode=4624,"Successful","Failed")
| timechart span=1m count by Login_Status
```

Analysed login activity minute by minute.

## Practical 6 – Failed Login Detection Within One Minute

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| bin _time span=1m
| stats count by _time Account_Name Source_Network_Address
| where count >= 3
| sort -count
```

Detected three failed login attempts within one minute.

## Practical 7 – Splunk Alert
Created a saved alert using the repeated failed login detection query.

## Practical 8 – Alert Conditions
Studied scheduled alerts, trigger conditions, and alert frequency.

## Practical 9 – SOC Investigation
Investigated account names, source IP addresses, logon types, event counts, and timestamps.

## Final Conclusion
Successfully generated and detected three controlled failed login attempts using Windows Security logs and Splunk Enterprise.

