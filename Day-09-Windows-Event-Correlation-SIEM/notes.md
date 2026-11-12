# Day 09 – SIEM and Event Correlation

## 1. What is SIEM?

SIEM stands for Security Information and Event Management.

SIEM is a security tool that collects logs from multiple systems in one place.

It helps SOC Analysts monitor systems and detect suspicious activities.

### Why do we need SIEM?

- Checking every system individually takes time.
- SIEM collects logs from different systems.
- It helps detect suspicious activities.
- It generates security alerts.
- It makes investigation easier.

### Popular SIEM Tools

1. Splunk
2. Microsoft Sentinel
3. IBM QRadar

## 2. What is Event Correlation?

Event Correlation means connecting multiple events to understand what happened.

Example:

| Event ID | Activity |
|---|---|
| 4625 | Failed login |
| 4625 | Failed login |
| 4625 | Failed login |
| 4624 | Successful login |

If multiple failed logins are followed by a successful login, it may be suspicious.

A SOC Analyst should investigate before deciding whether it is an attack.

## 3. Important Windows Event IDs

| Event ID | Meaning |
|---|---|
| 4624 | Successful login |
| 4625 | Failed login |
| 4634 | Logoff |
| 4648 | Explicit credentials used |
| 4672 | Special privileges assigned |
| 4688 | New process created |

## 4. Windows Logon Types

| Logon Type | Meaning |
|---|---|
| 2 | Interactive login |
| 3 | Network login |
| 4 | Batch login |
| 5 | Service login |
| 7 | Unlock |
| 10 | Remote login (RDP) |

## 5. What should a SOC Analyst check?

While investigating login events, check:

1. Timestamp – When did the event happen?
2. Username – Which account was involved?
3. Source IP – Where did the login come from?
4. Logon Type – How did the login happen?
5. Failure Reason – Why did the login fail?

## 6. Useful PowerShell Commands

### Check successful and failed logins

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624,4625
} -MaxEvents 20
```

### Check process creation events

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4688
} -MaxEvents 10
```

### Display event time and ID

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624,4625,4688
} -MaxEvents 20 |
Select-Object TimeCreated, Id
```

### Display detailed event information

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624,4625
} -MaxEvents 5 |
Format-List TimeCreated, Id, Message
```

Note: Run PowerShell as Administrator if you get an access error.

## 7. SOC Analyst Investigation Steps

1. Detect suspicious activity.
2. Check the security logs.
3. Compare related events.
4. Check timestamps and account details.
5. Investigate suspicious activity.
6. Prepare an investigation report.

## 8. Important Points

- SIEM collects logs from multiple systems.
- Event Correlation connects related events.
- Failed login does not always mean an attack.
- Suspicious activity needs investigation.
- Always verify evidence before making a conclusion.

## Conclusion

Today I learned about SIEM, Event Correlation and Windows Security Event IDs.

I also learned how SOC Analysts investigate login activities and identify suspicious patterns.
