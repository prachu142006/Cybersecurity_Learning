# Day 17: Password Spraying Attack Detection Using Splunk

## 1. Introduction

Password Spraying is a type of cyberattack in which an attacker tries one common password or a small number of passwords against multiple user accounts.

The objective is to gain unauthorized access without triggering account lockout policies.

**Example:**

An attacker targets five accounts:
- Rahul
- Priya
- Amit
- Sneha
- Neha

Instead of trying multiple passwords against one account, the attacker tries the same password against all five accounts.

This activity is known as Password Spraying.

## 2. Objectives

- Understand password spraying attacks.
- Understand the difference between password spraying and brute force.
- Identify failed login attempts using Splunk.
- Detect multiple accounts receiving login failures from one IP address.
- Investigate successful logins after failed attempts.
- Analyse login activity using timestamps.
- Understand SOC incident investigation procedures.

## 3. What is Password Spraying?

Password spraying is an authentication attack where an attacker attempts to access multiple accounts using commonly guessed passwords.

### Characteristics

1. Multiple user accounts are targeted.
2. One or a few common passwords are used.
3. Attempts may originate from the same IP address.
4. Attempts may be distributed over time.
5. A successful login may indicate possible account compromise.

## 4. Password Spraying vs Brute Force Attack

| Password Spraying | Brute Force |
|---|---|
| Targets multiple accounts. | Usually targets one account. |
| Uses one or a few common passwords. | Tries many different passwords. |
| Focuses on multiple usernames. | Focuses on guessing one account's password. |
| Attempts may be distributed over time. | May generate repeated failures against one account. |
| Detect using distinct account counts. | Detect using repeated failures for one account. |

## 5. Important Windows Security Event IDs

| Event ID | Description |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4634 | Account logoff |
| 4648 | Logon using explicit credentials |
| 4672 | Special privileges assigned |
| 4688 | Process creation |

### Important Events for Password Spraying

- **4625:** Used to investigate failed authentication attempts.
- **4624:** Used to investigate successful authentication.

Both events help SOC Analysts understand authentication patterns.

## 6. Important Splunk Fields

| Field | Meaning |
|---|---|
| _time | Date and time of event |
| Account_Name | Account involved in the event |
| EventCode | Windows Event ID |
| Source_Network_Address | Source IP address |
| Logon_Type | Type of logon |
| Failure_Reason | Reason for authentication failure |
| sourcetype | Type of collected data |
| index | Location where events are stored |

## 7. Important SPL Commands

**stats:** Calculates statistics from search results.

**count:** Counts the number of events.

**dc():** Counts distinct or unique values.

**values():** Displays unique values of a field.

**where:** Filters results based on a condition.

**eval:** Creates or modifies fields.

**if():** Checks a condition and returns one of two values.

**case():** Evaluates multiple conditions.

**bin:** Groups events into time intervals.

**timechart:** Creates a time-based visualization.

**makeresults:** Generates synthetic events for testing.

**streamstats:** Calculates statistics across events in sequence.

## 8. Password Spraying Detection Logic

A SOC Analyst can investigate a possible password spraying attack using the following approach:

1. Search for failed login events (4625).
2. Group events by source IP address.
3. Count distinct usernames.
4. Identify IP addresses targeting multiple accounts.
5. Examine timestamps and time intervals.
6. Search for successful logins (4624).
7. Investigate unusual activity after successful authentication.

**Example detection condition:**

Multiple failed login attempts against different accounts from one source IP address within a short period.

This is a suspicious pattern, not automatic proof of an attack.

## 9. SOC Analyst Investigation Process

### Step 1: Alert Validation
Check whether the alert represents genuine suspicious activity.

### Step 2: Source IP Investigation
Identify the source IP and determine whether it is internal or external.

### Step 3: Account Investigation
Identify all affected user accounts.

### Step 4: Timeline Analysis
Compare failed and successful login timestamps.

### Step 5: Successful Login Investigation
Check whether any account successfully authenticated after repeated failures.

### Step 6: Post-Login Investigation
Check for:
- Unusual process execution.
- Sensitive file access.
- Unexpected network connections.
- Unusual account activity.
- Suspicious privilege usage.

### Step 7: Containment
If compromise is confirmed, appropriate actions may include:
- Resetting affected passwords.
- Revoking active sessions.
- Temporarily disabling compromised accounts.
- Blocking malicious IP addresses when appropriate.
- Enforcing multi-factor authentication.
- Escalating the incident.

## 10. Real Windows Logs vs Simulated Events

**Real Windows Security Logs:** Generated by the operating system and collected by Splunk.

**Simulated Events:** Manually generated inside Splunk using commands such as `makeresults` and `eval`.

Simulated events help analysts understand detection logic when real attack events are unavailable.
