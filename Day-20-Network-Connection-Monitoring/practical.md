# Day 20 – Network Connection Monitoring Practical

## Objective
To monitor and investigate network connection activity using Sysmon Event ID 3 and Splunk.

## Tools Used
- Windows Event Viewer
- Sysmon
- Splunk Enterprise

## Practical 1: Event Viewer Monitoring

1. Open Windows Event Viewer.
2. Navigate to:

   Applications and Services Logs → Microsoft → Windows → Sysmon → Operational

3. Filter the log using Event ID 3.
4. Open a network connection event.
5. Observe the application name, source IP, destination IP, destination port, and protocol.

## Practical 2: Network Connection Investigation

Observed event details:

| Field | Observed Value |
|---|---|
| Event ID | 3 |
| Application | splunkd.exe |
| Source IP | 127.0.0.1 |
| Destination IP | 127.0.0.1 |
| Destination Port | 8089 |
| Protocol | TCP |

### Investigation

The application `splunkd.exe` was communicating with localhost (`127.0.0.1`) over TCP port `8089`.

This appeared to be normal internal Splunk communication. No immediate security threat was identified from the available evidence.

## Practical 3: Splunk Monitoring

The following SPL search was used to search for Sysmon logs:

```spl
index=main sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational"
```

The search was used to verify that Sysmon events were available in Splunk.

Event ID 3 records were then examined for network connection activity.

## Conclusion

Successfully monitored network connection activity using Sysmon Event ID 3 and investigated localhost communication using Windows Event Viewer and Splunk.
