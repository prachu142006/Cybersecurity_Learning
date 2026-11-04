# Day 3 – Networking Practical

## Objective

To understand basic networking concepts and inspect network configuration using Kali Linux.

## Tools Used

* Kali Linux
* Terminal
* Linux networking commands

## Commands Executed

### 1. Check IP Address

```bash
ip -br addr
```

Purpose: Displays network interfaces and their IP addresses.

### 2. Check Network Interfaces

```bash
ip link show
```

Purpose: Displays network interfaces and MAC addresses.

### 3. Check Routing Table

```bash
ip route
```

Purpose: Displays the routing table and default gateway.

### 4. Check DNS Configuration

```bash
cat /etc/resolv.conf
```

Purpose: Displays configured DNS servers.

### 5. Test Network Connectivity

```bash
ping -c 4 8.8.8.8
```

Result: 4 packets transmitted and 4 received, with 0% packet loss.

### 6. Test DNS Resolution

```bash
nslookup google.com
```

Result: DNS resolution was successful and returned IPv4 and IPv6 addresses.

## Observations

* Kali Linux had an active network interface.
* A private IPv4 address was assigned.
* A default gateway was configured.
* DNS servers were configured.
* Internet connectivity was successful.
* Domain name resolution was successful.

Sensitive IP addresses, MAC addresses and DNS server details have intentionally been excluded.

## Conclusion

I learned how to inspect network interfaces, IP addresses, MAC addresses, routing tables and DNS configuration. I also tested network connectivity and domain name resolution using Kali Linux.

These skills are useful for basic network troubleshooting and SOC investigations.
