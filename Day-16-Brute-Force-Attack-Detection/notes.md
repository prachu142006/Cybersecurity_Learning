# Day 16 – Brute Force Attack Detection Using Splunk

## 1. Objective
To understand brute-force attacks and detect repeated failed login attempts using Splunk Enterprise.

## 2. What is a Brute Force Attack?
A brute-force attack is an authentication attack in which multiple password combinations are attempted to gain unauthorized access.

## 3. Important Windows Event IDs
- 4624 – Successful Logon
- 4625 – Failed Logon
- 4634 – Account Logoff
- 4648 – Explicit Credentials
- 4672 – Special Privileges Assigned

## 4. Types of Password Attacks
- Brute Force
- Password Spraying
- Credential Stuffing
- Dictionary Attack

## 5. Splunk Detection
Splunk can identify repeated failed logins using Event ID 4625.

Example detection logic:

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name Source_Network_Address
| where count >= 3
| sort -count
```

## 6. SOC Investigation
A SOC Analyst investigates:
- Target account
- Source IP address
- Failed login count
- Login timestamps
- Logon type
- Successful login after failures

## 7. Conclusion
Splunk was used to collect and investigate Windows Security events. Three controlled failed login attempts were generated and successfully detected using SPL queries.
