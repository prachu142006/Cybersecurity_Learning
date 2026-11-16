# Day 12 - Importing and Searching Logs in Splunk

## Objective
Understand how Windows Security Logs are collected, stored and searched in Splunk.

## 1. Log Ingestion
Log ingestion means collecting data from different sources and bringing it into Splunk for monitoring and investigation.

Workflow:
Log Generation -> Collection -> Indexing -> Parsing -> Searching -> Investigation

## 2. Important Splunk Fields

- Host: Machine from which the log was generated.
- Source: Input or source from which Splunk collected the log.
- Sourcetype: Data format/type identified by Splunk.
- Index: Location where Splunk stores events.

## 3. Windows Event Log Configuration

Verified configuration:
- Input: Local Event Log Collection
- Computer: localhost
- Selected Channel: Security
- Configured Destination Index: default

## 4. Important Event IDs

- 4624: Successful Logon
- 4625: Failed Logon
- 4688: Process Creation

## 5. Raw Events vs Extracted Fields

Raw Event:
Original detailed event data received by Splunk.

Extracted Fields:
Individual fields parsed from the raw event.

Examples:
- EventCode
- Account_Name
- New_Process_Name
- Creator_Process_Name
- Process_Command_Line
- host
- source
- sourcetype

## 6. SOC Analyst Importance

SOC Analysts use logs to:
- Investigate login activities.
- Monitor process creation.
- Identify unusual process behaviour.
- Investigate suspicious account activity.

## 7. Learning Outcomes

- Understood log ingestion.
- Verified Windows Security log collection.
- Identified Host, Source and Sourcetype.
- Understood indexes and extracted fields.
- Learned the log collection and investigation workflow.
