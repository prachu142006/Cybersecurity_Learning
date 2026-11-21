# Day 15 – Suspicious Login Patterns

## 1. Objective
To investigate Windows successful and failed login activities using Splunk and identify unusual login patterns.

## 2. Important Event IDs

| Event ID | Meaning |
|---|---|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4800 | Workstation Locked |
| 4801 | Workstation Unlocked |

## 3. Important Logon Types

| Logon Type | Meaning |
|---|---|
| 0 | System |
| 2 | Interactive Login |
| 5 | Service Login |
| 7 | Workstation Unlock |
| 10 | Remote Interactive (RDP) |
| 11 | Cached Interactive Login |

## 4. Suspicious Login Patterns

A SOC Analyst investigates:

- Multiple failed login attempts.
- Unusual login timings.
- Unexpected remote logins.
- Login activity from unusual source IP addresses.
- Unusual account activity.
- Sudden increases in login failures.

## 5. Important SPL Commands

| Command | Purpose |
|---|---|
| eval | Creates or modifies fields |
| stats | Calculates statistics |
| sort | Sorts search results |
| timechart | Displays activity over time |
| table | Displays selected fields |
| search | Filters search results |
| head | Limits the number of results |

## 6. SOC Investigation Workflow

1. Collect Windows Security Logs.
2. Identify successful and failed login events.
3. Analyse login timings.
4. Check Logon Types.
5. Investigate source IP addresses.
6. Analyse account-wise login activity.
7. Correlate events.
8. Prepare an investigation conclusion.

## 7. Important Learning

A single failed login does not automatically indicate a brute-force attack.

SOC Analysts must investigate the timestamp, account, source address, Logon Type and surrounding events before classifying activity as suspicious.

## 8. Conclusion

This practical helped me understand how to investigate login patterns using Splunk SPL queries and how to identify potentially suspicious authentication activity.
