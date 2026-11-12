# Day 08 – Windows Process Monitoring & Suspicious Process Investigation

## 1. What is a Process?

A process is a program that is currently running on a computer.

Examples:
- Notepad
- Google Chrome
- PowerShell
- Windows background services

## 2. What is PID?

PID stands for Process Identifier.

- Every running process gets a unique Process ID.
- Windows uses PID to identify and manage processes.
- We can view PIDs in Task Manager.

## 3. Parent and Child Processes

A parent process can start another process.

- Parent Process: The process that starts another process.
- Child Process: The newly started process.

Example:

WINWORD.exe → powershell.exe

This relationship may be suspicious because Microsoft Word normally does not need to start PowerShell.

However, it is not automatically proof of malware.

## 4. Important Windows Processes

### svchost.exe
- Full name: Service Host.
- Hosts Windows background services.
- Normally located in C:\Windows\System32\.

### dllhost.exe
- Also known as COM Surrogate.
- Hosts COM components used by Windows applications.
- Normally located in C:\Windows\System32\.

Important: A legitimate process name does not guarantee that a file is safe. Check its location, digital signature and behaviour.

## 5. Event ID 4688

Event ID 4688 means a new process has been created.

It is recorded in:

Windows Logs → Security

It helps SOC Analysts investigate:
- Which process started?
- Which user started it?
- What was its parent process?
- What was the process ID?
- What was its executable path?

## 6. Important Event 4688 Fields

| Field | Meaning |
|---|---|
| New Process Name | Newly started program path |
| New Process ID | PID of the new process |
| Creator Process Name | Parent process name |
| Creator Process ID | Parent process ID |
| Subject Account Name | Account that created the process |
| Process Command Line | Command and arguments, if auditing is configured |

Note: Command-line information requires an additional Windows policy setting.

## 7. Useful PowerShell Commands

Check running processes:

```powershell
Get-Process
```

Display process names, IDs and CPU:

```powershell
Get-Process | Select-Object ProcessName, Id, CPU
```

Display parent and child process information:

```powershell
Get-CimInstance Win32_Process | Select-Object Name, ProcessId, ParentProcessId
```

Check process creation auditing:

```powershell
auditpol /get /subcategory:"Process Creation"
```

Enable successful process creation auditing (Administrator PowerShell):

```powershell
auditpol /set /subcategory:"Process Creation" /success:enable
```

## 8. SOC Analyst Investigation

When investigating a suspicious process:

1. Identify the process name.
2. Check its executable path.
3. Identify its parent process.
4. Check the user account.
5. Review its command line, if available.
6. Investigate related network and file activity.
7. Decide whether the activity is legitimate or suspicious based on evidence.

## 9. Important SOC Concepts

- Suspicious does not always mean malicious.
- A legitimate tool can be misused by attackers.
- Unusual parent-child relationships need investigation.
- One event alone may not prove an attack.

## Conclusion

Windows process monitoring helps SOC Analysts understand program execution and identify potentially suspicious activities.

Event ID 4688 is useful for investigating process creation and understanding parent-child relationships.
