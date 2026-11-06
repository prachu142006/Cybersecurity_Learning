# Day 4 – Network Traffic Analysis

## 1. What is Network Traffic?
Network traffic refers to the data transferred between devices over a network.

Example: When we open a website, our computer sends requests to a server and receives responses.

## 2. What is a Packet?
A packet is a small unit of data transmitted over a network.

A packet commonly contains:
- Source IP address
- Destination IP address
- Protocol information
- Port information (when applicable)
- Payload (data)

## 3. What is Wireshark?
Wireshark is a network protocol analyzer used to capture and inspect network traffic.

It helps security professionals:
- Monitor network communication.
- Analyze packets.
- Identify protocols.
- Investigate suspicious traffic.
- Troubleshoot network problems.

## 4. Important Wireshark Terms

- Capture: Recording network packets.
- Source IP: Address of the sending device.
- Destination IP: Address of the receiving device.
- Protocol: Rules used for communication.
- Packet Length: Size of a packet.
- Payload: Data carried inside a packet.
- Display Filter: Used to display selected packets.

## 5. Important Wireshark Filters

| Filter | Purpose |
|---|---|
| dns | Displays DNS packets |
| icmp | Displays ICMP packets |
| tcp | Displays TCP packets |
| udp | Displays UDP packets |
| http | Displays HTTP packets |
| ip.addr == 8.8.8.8 | Displays traffic involving the specified IP |

## 6. Capture Filter vs Display Filter

Capture Filter:
- Applied before packet capture.
- Controls which packets are captured.

Display Filter:
- Applied after packets are captured.
- Controls which packets are displayed.
- Does not delete captured packets.

## 7. Importance of Wireshark in SOC

A SOC Analyst uses Wireshark to:
- Investigate suspicious network connections.
- Identify unusual communication.
- Analyze source and destination IP addresses.
- Monitor network protocols.
- Detect possible security threats.

## Conclusion
Wireshark is an important tool for network traffic analysis and security investigations.

