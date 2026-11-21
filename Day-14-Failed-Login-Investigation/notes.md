# Day 14 – Failed Login Investigation

## Objective
To investigate failed login attempts using Splunk and Windows Security Event Logs.

## 1. Windows Event ID 4625
Event ID 4625 represents a failed login attempt in Windows.

It helps SOC analysts investigate:
- Incorrect password attempts.
- Unauthorized login attempts.
- Repeated login failures.
- Possible brute-force activity.

## 2. Important Event Fields

- Account_Name: Account involved in the login attempt.
- Account_Domain: Domain or workgroup associated with the account.
- Logon_Type: Type of login attempt.
- Source_Network_Address: Source IP address.
- Failure_Reason: Reason for login failure.
- Status: Main failure status code.
- Sub_Status: Additional failure information.

## 3. Logon Type 2
Logon Type 2 represents an interactive login.

It generally occurs when a user logs on locally using the computer's keyboard and screen.

## 4. Status Codes

- 0xC000006D: Generic logon failure.
- 0xC0000380: Additional failure status observed in the investigated event.

## 5. Failed Login Analysis

SOC analysts investigate:
- Number of failed login attempts.
- Accounts targeted.
- Source IP addresses.
- Login timestamps.
- Repeated failures within a short period.

A single failed login does not automatically indicate an attack.

## 6. Brute-Force Detection

A brute-force attack involves repeated attempts to guess account credentials.

Indicators may include:
- Multiple failed logins.
- Repeated attempts against one account.
- Attempts from suspicious source IPs.
- Multiple accounts targeted within a short period.

## 7. SOC Investigation Workflow

1. Search for Event ID 4625.
2. Identify the account involved.
3. Check the logon type.
4. Investigate source IP and failure status.
5. Analyse failed login frequency.
6. Compare successful and failed logins.
7. Document findings and reach an evidence-based conclusion.

## Learning Outcomes

- Learned to investigate Windows Event ID 4625.
- Understood important failed login fields.
- Analysed login failure status codes.
- Used Splunk SPL for failed login investigation.
- Compared successful and failed login activity.
- Understood how SOC analysts assess possible brute-force attacks.
