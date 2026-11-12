# Day 09 – Windows Event Log Investigation

## Aim

To investigate Windows Security Logs and understand Event Correlation and SIEM.

## 1. Tools Used

- Windows Event Viewer
- Windows PowerShell
- Windows Security Logs

## 2. Event Viewer Practical

Opened Event Viewer using:

```text
eventvwr.msc
```

Navigated to:

```text
Event Viewer
    → Windows Logs
        → Security
            → Filter Current Log
```

Filtered these Event IDs:

```text
4624, 4625, 4688
```

### Observation

All three Event IDs were available.

| Event ID | Meaning | Status |
|---|---|---|
| 4624 | Successful login | Available |
| 4625 | Failed login | Available |
| 4688 | New process created | Available |

## 3. Login Investigation

### Event ID 4624

Observed:

- Date: 12-11-2026
- Time: 19:40:32
- Logon Type: 5
- Result: Successful service logon

### Failed Login Observation

Reported event details:

- Date: 09-11-2026
- Time: 23:01:01
- Logon Type: 2
- Failure message: An error occurred during logon.

Note: Verify the Event ID in Event Viewer before recording it as 4625. The initially reported ID was 4635.

## 4. Event Correlation

Compared the successful and failed login events.

Findings:

- Both events occurred on different dates.
- Their Logon Types were different.
- No connection between these events was established.

### SOC Conclusion

There is not enough evidence to confirm a brute-force attack.

A SOC Analyst should check more logs before making a final decision.

## 5. PowerShell Commands for Investigation

### Command 1: Check login events

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624,4625
} -MaxEvents 20
```

Purpose: Shows recent successful and failed login events.

### Command 2: Check process events

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4688
} -MaxEvents 10
```

Purpose: Shows recent process creation events.

### Command 3: Check event timestamps

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624,4625,4688
} -MaxEvents 20 |
Select-Object TimeCreated, Id
```

Purpose: Helps compare event times.

### Command 4: Check detailed login information

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624,4625
} -MaxEvents 5 |
Format-List TimeCreated, Id, Message
```

Purpose: Displays detailed login event information.

## 6. What I Learned

1. What SIEM is and why it is important.
2. How SIEM collects logs from multiple systems.
3. What Event Correlation means.
4. How to identify successful and failed login events.
5. How to investigate Windows Security Logs.
6. Why SOC Analysts must verify suspicious activities.

## Conclusion

Successfully investigated Windows Security Logs and learned the basics of Event Correlation.

Understood how SIEM helps SOC Analysts monitor multiple systems and detect suspicious activities.

Practical Status: Event Viewer investigation completed.
