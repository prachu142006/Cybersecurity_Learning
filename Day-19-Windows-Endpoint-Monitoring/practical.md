# Day 19 – Practical Activities

## Practical 1: Windows Process Monitoring

**Tool:** Windows Task Manager

**Steps:**
1. Opened Task Manager using Ctrl + Shift + Esc.
2. Opened the Processes tab.
3. Observed running applications.
4. Opened the Details tab.

**Observation:**

Observed running applications, process names, CPU usage, and memory usage.

**Result:**

Successfully identified running processes and monitored basic system resource usage.

---

## Practical 2: Parent and Child Process Investigation

**Tool:** Windows PowerShell

**Command:**

`Get-CimInstance Win32_Process`

**Observation:**

Identified the process name, Process ID (PID), and ParentProcessId.

**Result:**

Successfully understood how to identify a process and its parent process using Windows PowerShell.

---

## Practical 3: Sysmon Process Investigation

**Tool:** Windows Event Viewer (Sysmon)

**Event ID:** 1 – Process Creation

**Steps:**
1. Opened Event Viewer.
2. Navigated to Sysmon Operational logs.
3. Filtered Event ID 1.
4. Located the Notepad process creation event.

**Observation:**

Identified four important event fields:

- User
- Image
- ParentImage
- CommandLine

**Result:**

Successfully investigated process creation details using Sysmon Event ID 1.

---

## Practical 4: PowerShell Monitoring

**Tool:** Windows PowerShell

**Commands:**

`Get-Date`

`Get-Process`

**Observation:**

- Get-Date displays the current date and time.
- Get-Process displays the list of currently running processes.

**Result:**

Successfully performed basic system monitoring using PowerShell commands.

---

## SOC Investigation Scenario

**Scenario:**

A SOC Analyst observes the following process relationship:

`winword.exe → powershell.exe`

The PowerShell process also contains an encoded command.

**Investigation:**

1. Check why Microsoft Word launched PowerShell.
2. Analyse the encoded command.
3. Check related network connections.
4. Investigate user activity.
5. Classify the activity based on available evidence.

**Conclusion:**

This activity is potentially suspicious and requires further investigation. It should not automatically be classified as a confirmed attack.

---

## Final Learning

Learned how to monitor Windows processes, identify parent-child process relationships, examine Sysmon events, and investigate potentially suspicious PowerShell activity.
