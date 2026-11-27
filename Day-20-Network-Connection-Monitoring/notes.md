# Day 20 – Network Connection Monitoring

## 1. Introduction
Network connection monitoring helps security analysts monitor and investigate network activity performed by applications and processes on a Windows system.

Sysmon Event ID 3 records network connection activity.

## 2. Sysmon Event ID 3
Event ID 3 captures network connections associated with processes on a Windows system.

It helps analysts identify which application is communicating, where the connection is going, and which protocol is being used.

## 3. Important Fields

- **Image:** Application or executable path responsible for the connection.
- **SourceIp:** IP address from which the connection originates.
- **SourcePort:** Port number used by the source.
- **DestinationIp:** IP address of the destination.
- **DestinationPort:** Port number of the destination.
- **Protocol:** Network protocol used, such as TCP or UDP.
- **User:** Account associated with the process.

## 4. Localhost

The IP address `127.0.0.1` represents localhost. It refers to the same computer.

Applications may communicate with services running on the same system through localhost.

## 5. SOC Investigation

A SOC Analyst investigates network connections by checking:

- Application name.
- Source and destination IP addresses.
- Destination port.
- Protocol.
- User and application context.

An unusual connection does not automatically indicate an attack. The analyst must investigate and verify the activity before classifying it as malicious.

## 6. Splunk Monitoring

Splunk can collect and search Sysmon logs to help analysts monitor network connections and investigate potentially suspicious activity.

## 7. Key Learning

Sysmon Event ID 3 helps SOC Analysts monitor network connections, understand application communication, and investigate suspicious network activity.
