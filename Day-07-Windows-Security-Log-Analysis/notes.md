# Day 7 – Windows Security Event Log Analysis

## 1. Objective
To understand Windows Event Logs and learn how SOC Analysts investigate successful and failed login attempts.

## 2. What are Windows Event Logs?

Windows Event Logs record important activities performed on a Windows computer.

Examples:
- Successful login attempts.
- Failed login attempts.
- Application errors.
- System activities.
- User account changes.
- Security-related activities.

SOC Analysts use these logs to identify suspicious activities and investigate possible security incidents.

## 3. Types of Windows Event Logs

### Application Logs
Record activities and errors related to applications.

### System Logs
Record operating system and Windows service activities.

### Security Logs
Record security-related activities such as login attempts, account changes and privilege assignments.

## 4. Important Windows Security Event IDs

<<<<<<< HEAD
 Event ID -> Description 

  4624       Successful login 
  4625       Failed login 
  4634       Account logged off 
  4648       Login using explicit credentials 
  4672       Special privileges assigned 
  4688       New process created 
  4720       User account created 
  4726       User account deleted 

## 5. Important Logon Types

 Logon Type   Description 

 2            Interactive login 
 3            Network login 
 5            Service login 
 7            Workstation unlock 
 10           Remote Interactive login (Remote Desktop) 
=======
| Event ID | Description |
|---|---|
| 4624 | Successful login |
| 4625 | Failed login |
| 4634 | Account logged off |
| 4648 | Login using explicit credentials |
| 4672 | Special privileges assigned |
| 4688 | New process created |
| 4720 | User account created |
| 4726 | User account deleted |

## 5. Important Logon Types

| Logon Type | Description |
|---|---|
| 2 | Interactive login |
| 3 | Network login |
| 5 | Service login |
| 7 | Workstation unlock |
| 10 | Remote Interactive login (Remote Desktop) |
>>>>>>> 3f0e4c6 (Day 7: Windows Security Log Analysis)

## 6. Authentication Package – Negotiate

Negotiate is a Windows authentication package that selects an appropriate authentication protocol.

It can negotiate between:
- Kerberos
- NTLM

## 7. SOC Analyst Investigation Process

When investigating suspicious login activity, a SOC Analyst should:

1. Identify the Event ID.
2. Check the target account.
3. Examine the source IP address, if available.
4. Check the Logon Type.
5. Review timestamps.
6. Identify repeated failed login attempts.
7. Check whether a successful login occurred afterward.
8. Correlate the events before deciding whether an attack occurred.

## 8. Suspicious Login Patterns

Examples:
- Multiple failed login attempts within a short period.
- Repeated login attempts against multiple accounts.
- Login attempts from unusual source addresses.
- Failed login attempts followed by a successful login.
- Unexpected privileged account activity.

## 9. Important SOC Concepts

- A failed login does not automatically indicate an attack.
- Legitimate users can enter incorrect passwords.
- A successful login does not automatically indicate malicious activity.
- Multiple related events should be correlated.
- An alert must be investigated before being classified as a confirmed incident.

## 10. Conclusion

Windows Security Event Logs are important sources of information for SOC Analysts. Understanding Event IDs, Logon Types and authentication details helps analysts investigate suspicious login activity and identify possible brute-force attacks.
