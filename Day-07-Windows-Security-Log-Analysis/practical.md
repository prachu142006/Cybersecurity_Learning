# Day 7 – Windows Security Event Log Analysis Practical

## 1. Objective

To investigate Windows Security Logs using Event Viewer and understand successful and failed authentication events.

## 2. Environment

- Operating System: Windows
- Tool: Windows Event Viewer
- Log Category: Windows Logs → Security

## 3. Practical Steps

### Step 1: Open Event Viewer

Opened Event Viewer using:

`eventvwr.msc`

### Step 2: Navigate to Security Logs

Opened:

`Event Viewer → Windows Logs → Security`

### Step 3: Filter Login Events

Used the Filter Current Log option and entered:

`4624,4625`

This displayed available successful and failed login events.

### Step 4: Investigate Event ID 4625

Observed the following:

<<<<<<< HEAD
Field              Observation 

Event ID           4625 
 Activity          Failed login 
 Logon Type        2 
Failure            Information An error occurred during logon 
 Source Address    Associated with own computer (as observed) 
=======
| Field | Observation |
|---|---|
| Event ID | 4625 |
| Activity | Failed login |
| Logon Type | 2 |
| Failure Information | An error occurred during logon |
| Source Address | Associated with own computer (as observed) |
>>>>>>> 3f0e4c6 (Day 7: Windows Security Log Analysis)

**Analysis:**

Logon Type 2 represents an interactive login attempt. It can occur when someone enters an incorrect password on the local Windows login screen.

This event alone does not confirm a brute-force attack.

### Step 5: Investigate Event ID 4624

Observed the following:

<<<<<<< HEAD
 Field                   Observation 

 Event ID                4624 
 Activity                Successful login 
 Logon Type              5 
 Account                 Own account 
 Authentication Package  Negotiate 
=======
| Field | Observation |
|---|---|
| Event ID | 4624 |
| Activity | Successful login |
| Logon Type | 5 |
| Account | Own account |
| Authentication Package | Negotiate |
>>>>>>> 3f0e4c6 (Day 7: Windows Security Log Analysis)

**Analysis:**

Logon Type 5 represents a service logon. Negotiate is a Windows authentication package that can select Kerberos or NTLM.

This event is different from an interactive user login.

## 4. SOC Analyst Investigation Scenario

Scenario:

- 20 failed login attempts.
- 1 successful login.
- Same target account.
- Events occurred within two minutes.

A SOC Analyst should investigate:

1. Target account.
2. Source IP address.
3. Logon Type.
4. Timestamps.
5. Authentication details.
6. Whether the successful login was legitimate.

Repeated failures followed by a successful login may indicate brute-force activity or account compromise. However, further investigation is necessary.

## 5. Key Learnings

- Learned to navigate Windows Event Viewer.
- Identified Event IDs 4624 and 4625.
- Understood the difference between successful and failed logins.
- Learned Logon Types 2 and 5.
- Understood the Negotiate authentication package.
- Learned how SOC Analysts investigate suspicious authentication activity.
- Understood why events must be correlated before declaring an incident.

## 6. Conclusion

Successfully performed a basic Windows Security Log investigation using Event Viewer.

Identified successful and failed authentication events and examined their Logon Types and authentication details.

This practical helped develop foundational SOC Analyst skills in Windows log monitoring and authentication investigation.

## 7. Privacy and Security

Personal usernames, computer names, IP addresses and sensitive log information are not included in this public report.
