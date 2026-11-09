# Day 6 – SSH Brute Force Detection

## 1. Objective

To investigate SSH service activity and examine Linux authentication logs for possible brute-force activity.

## 2. Environment

- Operating System: Kali Linux
- Tool: Linux Terminal
- Log Investigation: journalctl
- Target: Own local Kali Linux system

## 3. Commands Executed

### Check SSH service logs

```bash
sudo journalctl -u ssh --since today --no-pager
```

### Check authentication log file

```bash
sudo ls -l /var/log/auth.log
```

Result: File was not available.

### Search SSH daemon logs

```bash
sudo journalctl --since "7 days ago" _COMM=sshd --no-pager
```

### Search SSH session logs

```bash
sudo journalctl --since "7 days ago" _COMM=sshd-session --no-pager
```

### Search authentication failures

```bash
sudo journalctl --since "7 days ago" | grep -Ei 'accepted|failed password|invalid user|authentication failure'
```

### Search SSH authentication events

```bash
sudo journalctl --since "7 days ago" | grep -Ei 'sshd.*(failed|accepted|invalid)|failed password|accepted password|invalid user'
```

## 4. Observations

1. SSH service was active and listening on TCP port 22.
2. SSH startup events were identified.
3. Three localhost connection-closure events were found.
4. Two local authentication failure events were identified.
5. One event originated from LightDM.
6. One event originated from the XFCE screen unlock dialog.
7. No matching SSH authentication failure or successful login events were found in the reviewed journal records.

## 5. Security Analysis

The identified LightDM and XFCE authentication failures were related to local graphical authentication.

They were not evidence of SSH brute-force activity.

No confirmed SSH brute-force activity was identified in the available logs.

## 6. Conclusion

The practical helped me understand SSH authentication, Linux journal investigation, authentication failure events and the difference between graphical login failures and SSH login failures.

I learned that SOC Analysts must investigate event sources and supporting evidence before classifying an activity as a security incident.

## 7. Skills Practised

- SSH service investigation
- Linux authentication log analysis
- journalctl
- grep
- Security event identification
- Basic SOC investigation and reporting
