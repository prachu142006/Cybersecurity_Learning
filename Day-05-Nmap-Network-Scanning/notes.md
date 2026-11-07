# Day 5 – Nmap & Network Reconnaissance

## 1. Introduction to Nmap

Nmap stands for Network Mapper.

It is a network scanning tool used to:
- Discover active devices.
- Identify open ports.
- Identify running services.
- Detect service versions.
- Understand network exposure.

Nmap is commonly used by cybersecurity professionals and network administrators.

## 2. Important Nmap Terminology

**Host Discovery:** Finding active devices on a network.

**Port Scanning:** Checking the status of ports on a target system.

**Service Detection:** Identifying services running on open ports.

**Version Detection:** Identifying the versions of running services.

**OS Detection:** Estimating the operating system of a target.

## 3. Understanding Ports

A port is a communication endpoint used by network services.

Common ports:

- Port 22 – SSH
- Port 80 – HTTP
- Port 443 – HTTPS
- Port 3306 – MySQL

## 4. Port States

**Open:** A service is accepting connections on that port.

**Closed:** The port is reachable, but no service is listening.

**Filtered:** A firewall or other filter prevents Nmap from determining the port state clearly.

## 5. Important Nmap Commands

| Command | Purpose |
|---|---|
| `nmap --version` | Checks Nmap version |
| `nmap 127.0.0.1` | Performs a basic scan of localhost |
| `nmap -p 22,80,443 127.0.0.1` | Scans selected ports |
| `nmap -sV 127.0.0.1` | Detects service versions |
| `nmap -p- 127.0.0.1` | Scans all TCP ports |
| `nmap -sV 127.0.0.1 -oN nmap_results.txt` | Saves scan results in a text file |

## 6. Role of Nmap in SOC

A SOC Analyst may use Nmap during an authorized security investigation to:

1. Identify exposed ports.
2. Discover running services.
3. Check whether services are expected.
4. Identify potentially outdated software.
5. Investigate unnecessary network exposure.
6. Document findings and report them to the senior analyst.

## 7. Important Security Point

An open port does not automatically mean that a system is hacked or vulnerable.

A security analyst must investigate whether the service is authorized, required, and properly secured.

## 8. Interview Questions

**Q1. What is Nmap?**

Nmap is a network scanning tool used to discover devices, open ports, and running services.

**Q2. What is port scanning?**

Port scanning is the process of checking ports on a system to identify their states.

**Q3. Difference between open and filtered ports?**

Open means a service is accepting connections. Filtered means a firewall or filter prevents Nmap from determining the port state clearly.

**Q4. What does -sV do?**

The `-sV` option attempts to identify the services and their versions.

**Q5. Why does a SOC Analyst investigate an unexpected open port?**

Because an unexpected service may create unnecessary network exposure and require further investigation.

**Q6. Does an open port always indicate a vulnerability?**

No. An open port only indicates that a service is accepting connections. Further investigation is required.

## 9. Conclusion

Nmap helps cybersecurity professionals understand network exposure and identify accessible services. It is an important tool for network reconnaissance and security investigation.
