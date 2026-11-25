# Day 18 – Sysmon Monitoring

## 1. Introduction

Sysmon (System Monitor) is a Microsoft Windows tool used to monitor and record system activities.

It helps SOC Analysts investigate suspicious activities on Windows systems.

Sysmon stores its logs in:

`Microsoft-Windows-Sysmon/Operational`

## 2. Important Sysmon Event IDs

| Event ID | Description |
|---|---|
| 1 | Process Creation |
| 3 | Network Connection |
| 5 | Process Terminated |
| 22 | DNS Query |

### Event ID 1 – Process Creation

Records when a program or process starts.

Example: Opening Notepad.

SOC Analyst checks:
- Process name
- User account
- Parent process

### Event ID 3 – Network Connection

Records network connections made by processes.

SOC Analyst checks:
- Process name
- Source IP
- Destination IP
- Port number

### Event ID 5 – Process Terminated

Records when a process stops or closes.

Example: Closing Notepad.

### Event ID 22 – DNS Query

Records DNS requests made by applications.

Example: Visiting google.com.

SOC Analyst checks which domain was requested and whether it looks suspicious.

## 3. Practical Activities

### Practical 1 – Process Monitoring

1. Opened Notepad.
2. Opened Event Viewer.
3. Navigated to Sysmon Operational logs.
4. Located the process creation event.
5. Observed Event ID 1.

**Result:** Notepad process creation was monitored using Sysmon.

### Practical 2 – DNS Monitoring

1. Opened a web browser.
2. Visited google.com.
3. Opened Sysmon Operational logs.
4. Searched for the DNS query.
5. Checked Event ID 22.

**Result:** DNS query activity was monitored using Sysmon.

## 4. Importance of Sysmon in SOC

Sysmon helps SOC Analysts:

- Monitor process creation.
- Investigate network connections.
- Monitor DNS queries.
- Identify unusual system activity.
- Collect endpoint security evidence.

**Important:** A Sysmon event does not automatically mean an attack has occurred. Analysts must investigate the context.

## 5. Interview Questions

**Q1. What is Sysmon?**

Sysmon is a Windows monitoring tool that records detailed system activities for security investigation.

**Q2. What is Event ID 1?**

It records process creation.

**Q3. What is Event ID 3?**

It records network connections.

**Q4. What is Event ID 5?**

It records process termination.

**Q5. What is Event ID 22?**

It records DNS queries.

**Q6. Why is Sysmon useful for SOC Analysts?**

It helps monitor endpoint activities and investigate suspicious behaviour.

## 6. Conclusion

In this session, I learned about Sysmon, its important Event IDs, process monitoring and DNS monitoring. I also performed practical activities using Windows Event Viewer.

Sysmon provides useful endpoint information that helps SOC Analysts investigate security incidents.
