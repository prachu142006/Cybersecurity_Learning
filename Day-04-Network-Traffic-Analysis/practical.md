# Day 4 – Network Traffic Analysis Practical

## Objective
To capture and analyze network packets using Wireshark in Kali Linux.

## Tools Used
- Kali Linux
- Wireshark
- Terminal

## Commands Executed

### 1. Check Wireshark Version
```bash
wireshark --version
```
Purpose: Checks the installed Wireshark version.

### 2. Open Wireshark
```bash
wireshark
```
Purpose: Opens the Wireshark graphical interface.

### 3. Generate ICMP Traffic
```bash
ping -c 4 8.8.8.8
```
Purpose: Generates ping traffic for packet analysis.

### 4. Generate DNS Traffic
```bash
nslookup example.com
```
Purpose: Generates DNS queries to resolve a domain name.

## Network Interface
Selected interface: eth0

## Wireshark Display Filters Used

1. `dns` – To inspect DNS packets.
2. `icmp` – To inspect ping-related packets.
3. `tcp` – To inspect TCP packets.

## Observations
- Captured network packets using Wireshark.
- Observed source and destination information.
- Identified different network protocols.
- Used display filters to find specific packets.
- Inspected packet details.

## Security Note
Only authorized network traffic was captured and analyzed. Personal network information and raw packet captures were not uploaded publicly.

## Conclusion
Successfully learned how to capture and analyze network traffic using Wireshark. Practiced DNS and ICMP traffic analysis and understood the importance of packet inspection in SOC operations.
