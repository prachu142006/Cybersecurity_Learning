# Day 08 – Windows Process Monitoring Practical

## Objective

To understand Windows processes, enable process creation auditing, investigate Event ID 4688 and identify parent-child process relationships.

## 1. Tools Used

- Windows Task Manager
- Windows Event Viewer
- PowerShell
- AuditPol

## 2. Process Monitoring

Opened Task Manager using:

```text
Ctrl + Shift + Esc
```

Navigated to the Details tab to observe running processes and their PIDs.

Used PowerShell commands:

```powershell
Get-Process
```

```powershell
Get-Process | Select-Object ProcessName, Id, CPU
```

## 3. Process Creation Auditing

Initially checked the audit policy:

```powershell
auditpol /get /subcategory:"Process Creation"
```

Initial result:

```text
Process Creation    No Auditing
```

### Observation

Process creation auditing was disabled. Therefore, Windows was not recording Event ID 4688 process creation events in the Security log.

Enabled successful process creation auditing using Administrator PowerShell:

```powershell
auditpol /set /subcategory:"Process Creation" /success:enable
```

Result:

```text
The command was successfully executed.
```

After enabling auditing, Event ID 4688 events became visible in Event Viewer.

## 4. Event Viewer Investigation

Navigation:

```text
Event Viewer
  → Windows Logs
    → Security
      → Filter Current Log
        → Event ID: 4688
```

Opened a 4688 event and inspected its details.

### Actual Observation

| Field | Observed Value |
|---|---|
| Event ID | 4688 |
| New Process Name | C:\Windows\System32\dllhost.exe |
| New Process ID | 0x6b8 |
| Creator Process Name | C:\Windows\System32\svchost.exe |
| Subject Account Name | Masked for privacy |

Process ID conversion:

```text
0x6b8 = 1720 (decimal)
```

## 5. Process Relationship

Observed process relationship:

```text
svchost.exe
     |
     v
dllhost.exe
```

### Analysis

- svchost.exe is a Windows Service Host process.
- dllhost.exe is also known as COM Surrogate.
- Both were observed with System32 paths.
- This process relationship alone does not confirm malicious activity.

Further investigation would require checking digital signatures, process behaviour, command-line information and related events.

## 6. Suspicious Process Scenario

Example:

```text
WINWORD.exe → powershell.exe
```

This relationship may be suspicious because Microsoft Word normally does not need to start PowerShell.

An attacker may misuse a malicious document to execute PowerShell commands.

A SOC Analyst should investigate the command line, parent process, user account and related activities before confirming an attack.

## 7. Key Learnings

1. Learned how to monitor running Windows processes.
2. Understood PID and parent-child process relationships.
3. Learned how to enable Process Creation auditing using AuditPol.
4. Successfully located Event ID 4688 in Windows Security logs.
5. Investigated svchost.exe and dllhost.exe.
6. Understood why suspicious process activity requires further investigation.

## 8. Conclusion

Successfully enabled Windows Process Creation auditing and investigated Event ID 4688.

Identified a parent-child process relationship and learned how SOC Analysts investigate suspicious process activity without making conclusions based on a single event.

**Practical Status: Completed**
