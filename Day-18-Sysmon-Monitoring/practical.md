# Day 18 – Sysmon Practical

## Practical 1: Process Monitoring

**Objective:** To monitor process creation using Sysmon.

### Steps
1. Opened Notepad in Windows.
2. Opened Event Viewer.
3. Navigated to Microsoft-Windows-Sysmon/Operational.
4. Searched for the Notepad process creation event.
5. Observed Event ID 1.

**Observation:** Sysmon records process creation when an application starts.

**Result:** Successfully observed process creation activity.

## Practical 2: DNS Monitoring

**Objective:** To monitor DNS queries using Sysmon.

### Steps
1. Opened a web browser.
2. Visited google.com.
3. Opened Sysmon Operational logs in Event Viewer.
4. Searched for the DNS query.
5. Observed Event ID 22.

**Observation:** Sysmon records DNS query activity when applications request domain resolution.

**Result:** Successfully observed DNS query activity.

## SOC Analyst Learning

- Event ID 1 helps investigate newly started processes.
- Event ID 3 helps investigate network connections.
- Event ID 5 helps investigate terminated processes.
- Event ID 22 helps investigate DNS requests.

**Important:** An event alone does not confirm malicious activity. Further investigation is required.
