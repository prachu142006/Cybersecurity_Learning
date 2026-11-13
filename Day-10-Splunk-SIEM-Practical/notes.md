# Day 10 – Splunk SIEM

## 1. What is Splunk?

Splunk is a SIEM tool used to collect, search, monitor and analyse machine-generated data such as security logs.

## 2. What is SIEM?

SIEM stands for Security Information and Event Management.

It helps SOC analysts:
- Collect logs from systems.
- Monitor security events.
- Search suspicious activities.
- Investigate security alerts.
- Identify potential threats.

## 3. What is SPL?

SPL stands for Search Processing Language.

It is used to search and analyse data in Splunk.

Important commands:

- `search` – Search events.
- `stats` – Calculate statistics.
- `table` – Display selected fields.
- `sort` – Sort results.
- `head` – Display the first results.
- `timechart` – Display events over time.

## 4. Important Windows Event IDs

| Event ID | Description |
|---|---|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4634 | Account Logoff |
| 4648 | Explicit Credentials Used |
| 4672 | Special Privileges Assigned |
| 4688 | Process Creation |

## 5. What is Process Monitoring?

Process monitoring means observing which processes are created and executed on a system.

Event ID 4688 records process creation when the appropriate auditing is enabled.

## 6. Parent-Child Process Analysis

A parent process is the process that starts another process.

A child process is the newly created process.

Example:

`postgres.exe → cmd.exe`

SOC analysts investigate these relationships to identify unusual process behaviour.

## 7. Important Learning

A single event does not prove an attack.

SOC analysts investigate timestamps, accounts, process names, parent processes and command lines before making conclusions.
