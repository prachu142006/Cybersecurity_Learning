# Day 19 – Windows Endpoint Monitoring & Suspicious Process Investigation

## 1. What is a Process?

A process is an instance of a program that is currently running in the operating system.

Examples:
- notepad.exe
- chrome.exe
- powershell.exe

## 2. Parent and Child Process

- **Parent Process:** A process that starts another process.
- **Child Process:** A process that is started by another process.

Example:

`powershell.exe → notepad.exe`

Here:
- PowerShell is the Parent Process.
- Notepad is the Child Process.

## 3. PID and ParentProcessId

- **PID (Process ID):** A unique identification number assigned to a running process.
- **ParentProcessId:** The identification number of the process that started another process.

## 4. Why SOC Analysts Monitor Processes

SOC Analysts monitor running processes because attackers may execute suspicious programs through processes and perform unauthorized activities.

Process monitoring helps identify potentially malicious behaviour.

## 5. Sysmon Event ID 1 – Process Creation

Sysmon Event ID 1 records process creation.

It provides important information:

| Field | Meaning |
|---|---|
| Image | Location/path of the executable file |
| User | Account that started the process |
| ParentImage | Location/path of the parent process |
| CommandLine | Command used to start the process |

## 6. Suspicious Process Relationships

Example:

`winword.exe → powershell.exe`

Microsoft Word does not normally need to launch PowerShell.

A malicious Word document may attempt to execute commands or scripts through PowerShell.

Therefore, SOC Analysts should investigate this activity.

**Classification:** Potentially suspicious, not automatically a confirmed attack.

## 7. Encoded PowerShell

Encoded PowerShell is a PowerShell command represented in an encoded format instead of normal readable text.

Attackers may use encoded commands to make their activity harder to understand or analyse.

**Important:** Encoded commands are not always malicious. SOC Analysts must investigate them.

## 8. SOC Investigation Approach

When suspicious activity is detected, analysts should:

1. Check the process name.
2. Identify the user account.
3. Examine the parent process.
4. Analyse the command line.
5. Check related network connections.
6. Investigate other related events.

We cannot directly classify every suspicious activity as an attack. Further investigation is required to understand the context.

## 9. Conclusion

I learned how to monitor Windows processes and investigate suspicious activities using Task Manager, PowerShell, and Sysmon.

I also learned how to identify potentially suspicious activities by examining process names, parent processes, user accounts, command lines, and event details.

These skills help SOC Analysts investigate unusual behaviour and identify potential security threats.
