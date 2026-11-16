# Day 12 - Practical: Importing and Searching Logs

## 1. Verify Windows Security Logs

SPL Query:

    index=* sourcetype="WinEventLog:Security"
    | head 20

Purpose:
To verify that Windows Security events are available in Splunk.

## 2. Search Successful Logons

Event ID: 4624

    index=* sourcetype="WinEventLog:Security" EventCode=4624

Purpose:
To search for successful login events.

## 3. Search Failed Logons

Event ID: 4625

    index=* sourcetype="WinEventLog:Security" EventCode=4625

Purpose:
To search for failed login events.

Note:
If no results appear, it only means that no matching events were found in the selected time range and collected data.

## 4. Search Process Creation Events

Event ID: 4688

    index=* sourcetype="WinEventLog:Security" EventCode=4688

Purpose:
To investigate process creation activity.

## 5. Identify Important Fields

Inspected the following fields:

- Host: Local Windows machine
- Source: WinEventLog:Security
- Sourcetype: WinEventLog:Security

Purpose:
To understand where the event came from and how Splunk identifies it.

## 6. Verify Data Input Configuration

Steps:

1. Open Splunk Web.
2. Go to Settings.
3. Open Data Inputs.
4. Select Local Event Log Collection.
5. Open Edit.
6. Verify the Security channel.

Observation:

- Security channel was selected.
- Configured destination index showed `default`.

## 7. Inspect Raw Event and Extracted Fields

Searched for Event ID 4688 and inspected an event.

Observed fields:

- LogName: Security
- EventCode: 4688
- TaskCategory: Process Creation
- Keywords: Audit Success
- Account_Name: Splunkd
- Account_Domain: NT SERVICE
- New_Process_Name: postgres.exe
- Creator_Process_Name: postgres.exe

The process command line contained:

`--forkchild="autovacuum worker"`

Observation:

The event was consistent with Splunk's internal PostgreSQL autovacuum activity. A single event is not enough to classify an activity as malicious.

## 8. Index Observation

The Data Input configuration showed destination index `default`, but the inspected event showed index `main`.

This difference was recorded for further investigation.

## 9. Log Collection Workflow

Windows generates security events.

↓

Splunk collects the configured Security channel.

↓

Events are stored in an index.

↓

Splunk extracts fields.

↓

SOC analyst searches events using SPL.

↓

Analyst investigates and records findings.

## 10. Conclusion

Successfully verified Windows Security log collection in Splunk and searched for important security events.

Learned how to identify event fields, inspect raw events, and understand the log ingestion workflow.
