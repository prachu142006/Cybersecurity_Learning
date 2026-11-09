# Day 6 – SSH Brute Force Attack Detection

## 1. Introduction

SSH stands for Secure Shell. It is a network protocol used to securely access and manage remote systems.

SSH commonly uses TCP port 22.

## 2. What is a Brute Force Attack?

A brute force attack is an attempt to gain unauthorized access by repeatedly trying different passwords.

Attackers may target SSH services to access remote systems.

## 3. Important Authentication Events

| Event | Meaning |
|---|---|
| Accepted | Successful authentication |
| Failed password | Incorrect password attempt |
| Invalid user | Unknown username used |
| Authentication failure | Authentication unsuccessful |
| Connection closed | Connection terminated |

## 4. Linux Authentication Log Sources

Linux authentication events may be recorded in:

- `/var/log/auth.log` on systems using traditional authentication logging.
- `journalctl` on systems using systemd-journald.

The available log sources depend on the Linux distribution and configuration.

## 5. What is PAM?

PAM stands for Pluggable Authentication Modules.

It provides authentication mechanisms for Linux applications and services.

Examples:
- SSH authentication
- Graphical login authentication
- Screen unlock authentication

## 6. SOC Analyst Responsibilities

A SOC Analyst investigates:

1. Repeated failed login attempts.
2. Suspicious source IP addresses.
3. Targeted usernames.
4. Successful logins following repeated failures.
5. Unusual authentication activity.

## 7. Important Security Lesson

An authentication failure does not automatically indicate an attack.

Analysts must identify the application or service that generated the event before classifying it.

For example:
- LightDM: Graphical login.
- SSH: Remote terminal login.

## 8. Conclusion

Authentication log analysis helps SOC Analysts identify suspicious login activity, investigate possible brute-force attacks and distinguish normal authentication failures from security incidents.




