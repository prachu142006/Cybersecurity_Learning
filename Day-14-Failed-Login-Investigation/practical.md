# Day 14 – Failed Login Investigation Practical

## Environment
- Operating System: Windows
- SIEM Tool: Splunk Enterprise
- Log Source: Windows Security Event Logs
- Sourcetype: WinEventLog:Security

## Practical 1 – Failed Login Detection

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| table _time Account_Name Logon_Type Workstation_Name
| sort -_time
```

### Observation
One failed login event was identified.

## Practical 2 – Investigating Failed Login Details

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| table _time Account_Name Account_Domain Logon_Type Source_Network_Address Failure_Reason Status Sub_Status
```

### Observed Results

| Field | Result |
|---|---|
| Event ID | 4625 |
| Account | PRACHITI$ |
| Domain | WORKGROUP |
| Logon Type | 2 |
| Source IP | 127.0.0.1 |
| Failure Reason | An Error occurred during Logon |
| Status | 0xC000006D |
| SubStatus | 0xC0000380 |

Note: The account and machine identifiers should be masked before publishing screenshots publicly.

## Practical 3 – Failed Login Frequency

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name
| sort -count
```

### Observation
Only one failed login event was found.

## Practical 4 – Failed Login Timeline

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| timechart span=1h count
```

### Observation
One failed login event appeared in the 22:30 hourly time bucket on 9 November 2026.

## Practical 5 – Successful vs Failed Login Comparison

### SPL Query
```spl
index=* sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)
| stats count by EventCode
```

### Observed Results

| Event ID | Description | Count |
|---|---|---:|
| 4624 | Successful Login | 1903 |
| 4625 | Failed Login | 1 |

## Final SOC Investigation Findings

- Total successful login events: 1903.
- Total failed login events: 1.
- One account was involved in the observed failed login.
- Logon Type was 2 (Interactive).
- Source address was 127.0.0.1 (localhost).
- Only one failed attempt was observed in the available dataset.

## SOC Analyst Conclusion

One failed login event was identified in the collected Windows Security Logs.

The event involved an interactive login attempt originating from the local machine. No repeated failed login attempts were observed in the available dataset.

There was insufficient evidence to classify this activity as a brute-force attack.

**Final Assessment:** Isolated failed login event. No confirmed brute-force activity.

## Skills Practised

- Splunk Search Processing Language (SPL).
- Windows Event ID 4625 investigation.
- Failed login frequency analysis.
- Timeline analysis.
- Successful and failed login comparison.
- SOC investigation reporting.
