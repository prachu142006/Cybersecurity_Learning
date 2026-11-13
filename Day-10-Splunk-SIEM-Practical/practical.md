# Day 10 – Splunk SIEM Practical

## Objective
To install Splunk Enterprise, collect Windows Security Logs and investigate security events using SPL queries.

## 1. Splunk Setup

- Installed Splunk Enterprise on Windows.
- Opened Splunk Web using localhost port 8000.
- Added Windows Security Event Logs through the Monitor option.
- Selected the Security log channel.

## 2. Search Windows Security Logs

```spl
index=* sourcetype="WinEventLog:Security"
```

## 3. Successful and Failed Logon Analysis

```spl
index=* sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)
```

Result:
- Event ID 4624 was found.
- Event ID 4625 was not found in the selected 24-hour search window.

## 4. Logon Type Analysis

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4624
| stats count by Logon_Type
```

Observed Logon Types:
- Type 0 – System
- Type 2 – Interactive
- Type 5 – Service
- Type 7 – Unlock
- Type 11 – Cached Interactive

## 5. Failed Logon Investigation

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| stats count
```

Result: No failed logon events were found in the selected search window.

## 6. Process Creation Analysis

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4688
| stats count by New_Process_Name
| sort - count
| head 10
```

Observed processes included:
- splunk-optimize.exe
- postgres.exe
- splunkd.exe
- cmd.exe
- svchost.exe
- splunk.exe

## 7. Parent Process Investigation

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4688 New_Process_Name="*cmd.exe"
| table _time New_Process_Name Creator_Process_Name
| sort - _time
```

Observation:

- New Process: cmd.exe
- Parent Process: postgres.exe
- Repeated process creation was observed approximately every 10 seconds.

## 8. Command Line Investigation

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4688 New_Process_Name="*cmd.exe"
| table _time Creator_Process_Name Process_Command_Line
| sort - _time
```

Result:
- Parent process: postgres.exe
- Process command line: Blank

## 9. Investigation Conclusion

Repeated cmd.exe creation by postgres.exe was observed.

The command line was not available in the collected events. Therefore, the activity requires further investigation.

No confirmed malicious activity was established from this evidence.

## 10. Conclusion

Successfully installed Splunk, collected Windows Security Logs and performed basic SIEM investigations using SPL.

Learned how to analyse logon events, monitor process creation and investigate parent-child process relationships.
