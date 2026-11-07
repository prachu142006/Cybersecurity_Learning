# Day 5 – Nmap & Network Reconnaissance

## 1. Objective

To perform network scanning on my own Kali Linux system using Nmap, identify open and closed ports, detect running services, and understand the scan results from a SOC Analyst's perspective.

## 2. Lab Environment

- Operating System: Kali Linux
- Tool: Nmap
- Nmap Version: 7.98
- Target: Localhost
- Target IP: 127.0.0.1

## 3. Practical Tasks

### Task 1: Service and Version Detection

**Command:**

```bash
nmap -sV 127.0.0.1
```

**Actual Observation:**

```text
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 10.2p1 Debian 5 (protocol 2.0)
```

Additional output:
- Host was up.
- 999 closed TCP ports were reported.
- Service detection identified SSH.

**Analysis:**

- Port 22 was open.
- SSH service was running.
- Detected version was OpenSSH 10.2p1 Debian 5.
- The scan identified the service running on the target.

### Task 2: Selected Port Scanning

**Command:**

```bash
nmap -p 22,80,443 127.0.0.1
```

**Actual Observation:**

```text
PORT    STATE  SERVICE
22/tcp  open   ssh
80/tcp  closed http
443/tcp closed https
```

**Analysis:**

- Port 22: Open – SSH service was accepting connections.
- Port 80: Closed – No HTTP service was listening.
- Port 443: Closed – No HTTPS service was listening.

### Task 3: Identify the Process Listening on Port 22

**Command:**

```bash
sudo ss -tulnp | grep ':22'
```

**Actual Observation:**

```text
tcp LISTEN 0 128 0.0.0.0:22 0.0.0.0:* users:(("sshd",pid=749,fd=6))
tcp LISTEN 0 128 [::]:22 [::]:* users:(("sshd",pid=749,fd=7))
```

**Analysis:**

- Port 22 was in LISTEN state.
- Process name: sshd
- Process ID: 749
- SSH was listening on IPv4 and IPv6 addresses.

### Task 4: Check SSH Service Status

**Command:**

```bash
sudo systemctl status ssh
```

**Actual Observation:**

- SSH service was loaded.
- SSH service was enabled.
- SSH service was active (running).
- Main process ID was 749.

**Analysis:**

The SSH service was running on my Kali Linux system.

### Task 5: Investigate SSH Logs

**Command:**

```bash
sudo journalctl -u ssh -n 30 --no-pager
```

**Actual Observation:**

- SSH service startup messages were present.
- Logs showed SSH listening on IPv4 and IPv6.
- Some localhost connection-closed messages were present.
- No `Accepted`, `Failed password`, or `Invalid user` entries appeared in the displayed 30 log lines.

**Analysis:**

The SSH logs helped me understand service activity and identify authentication-related events.

The displayed logs did not provide evidence of successful or failed authentication attempts.

## 4. Command Error and Correction

I initially executed:

```bash
nmap -p 127.0.0.1
```

**Error:**

```text
Error #487: Your port specifications are illegal.
```

**Reason:**

The `-p` option is used to specify port numbers. I mistakenly provided the target IP address after `-p`.

**Correct command:**

```bash
nmap -p 22 127.0.0.1
```

**Learning:**

The port specification and target IP address must be provided separately.

## 5. Final Investigation Findings

1. The localhost system was active.
2. TCP port 22 was open.
3. SSH service was identified as OpenSSH 10.2p1 Debian 5.
4. TCP ports 80 and 443 were closed.
5. The SSH process (`sshd`) was listening on port 22.
6. The SSH service was active and running.
7. The displayed SSH logs did not show authentication success or failure entries.

## 6. SOC Analyst Perspective

As a SOC Analyst, I learned that identifying an open port is only the beginning of an investigation.

An analyst should check:

- Whether the service is authorized.
- Whether the service is required.
- Which process is using the port.
- Whether the software is updated.
- Whether suspicious login activity is present.

An open port does not automatically indicate a vulnerability or security incident.

## 7. Conclusion

In this practical, I used Nmap to scan my own Kali Linux system and identify open and closed ports.

I also used `ss`, `systemctl`, and `journalctl` to investigate the SSH service, identify its process, check its status, and examine its logs.

This practical helped me understand basic network reconnaissance and how a SOC Analyst investigates exposed services.

**Safety:** All Nmap scans in this practical were performed against my own localhost system (127.0.0.1).
