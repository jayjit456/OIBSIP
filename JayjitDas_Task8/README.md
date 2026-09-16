# OASIS INFOBYTE - Security Analyst Internship

# Task 8: Capture Network Traffic with Wireshark

## Project Information

- **Internship:** OASIS Infobyte – Security Analyst
- **Selected Task:** Task 8 – Capture Network Traffic with Wireshark
- **Level:** Intermediate
- **Tool:** Wireshark
- **Operating System:** Kali Linux
- **Network Interface:** eth0
- **Environment:** Controlled local network / virtual machine laboratory
- **Capture File:** `wireshark_capture.pcap`

---

## 1. Objective

The objective of this task is to capture and analyze live network
traffic using Wireshark.

The assessment focuses on:

- Capturing live network traffic
- Filtering HTTP traffic
- Filtering DNS traffic
- Filtering TCP traffic
- Analyzing a TCP three-way handshake
- Identifying unencrypted HTTP data
- Understanding packet-level network communication
- Documenting security observations

All traffic analysis was performed in an authorized local laboratory
environment.

---

## 2. What is Wireshark?

Wireshark is a network protocol analyzer used to capture and inspect
network packets.

It allows security analysts and network administrators to examine
network communications at the packet level.

Wireshark can be used to:

- Capture network traffic
- Identify protocols
- Analyze packet headers
- Inspect packet contents
- Troubleshoot network problems
- Investigate suspicious network activity
- Understand communication between systems

---

## 3. Lab Environment

The packet capture was performed on a Kali Linux system using the
`eth0` network interface.

The testing was performed only on a controlled and authorized
laboratory network.

The capture was allowed to run for at least two minutes to collect
live network traffic for analysis.

---

## 4. Wireshark Installation

Wireshark was verified on Kali Linux using:

```bash
wireshark --version
The Wireshark application was then opened for packet capture.

The capture was performed from the available active network interface.

5. Network Traffic Capture

The active network interface used for the capture was:

eth0
The capture was started in Wireshark and live network traffic was
recorded for at least two minutes.

After the capture was completed, the packet capture was saved as:

wireshark_capture.pcap
The .pcap file contains the captured network packets and can be
reopened in Wireshark for further analysis.

6. HTTP Traffic Analysis
Display Filter
http

The http display filter was applied to isolate HTTP traffic from
the captured packets.

The filtered results were used to identify HTTP requests and responses.

Evidence
screenshots/01-http-filter.png

7. DNS Traffic Analysis
Display Filter
dns
The dns display filter was applied to isolate DNS traffic.

The filtered packets showed DNS queries and responses generated during
normal network communication.

Evidence
screenshots/02-dns-filter.png

8. TCP Traffic Analysis
Display Filter
tcp

The tcp display filter was used to isolate TCP packets from the
capture.

TCP traffic was analyzed to identify the connection-establishment
process.

Evidence
screenshots/03-tcp-handshake.png

9. TCP Three-Way Handshake

A TCP connection is established using a three-step handshake.

The captured packets showed the following sequence:

SYN
   ↓
SYN-ACK
   ↓
ACK
Observed Packets
Packet 105 → [SYN]
Packet 106 → [SYN, ACK]
Packet 107 → [ACK]

Explanation :-
1. SYN
The client sends a SYN packet to request the establishment of a TCP
connection with the server.

2. SYN-ACK
The server responds with SYN-ACK, acknowledging the client's request
and indicating that it is ready to establish the connection.

3. ACK
The client sends an ACK packet to acknowledge the server response.
The TCP connection can then continue with application data transfer.

Security Observation :-
The three-way handshake is an important part of TCP communication.
Analyzing the sequence helps a security analyst understand how
connections are established and investigate abnormal or incomplete
connection attempts.

10. Unencrypted HTTP Traffic

An HTTP packet containing a request such as:

GET / HTTP/1.1

was identified in the capture.

The HTTP traffic was inspected using the:

http

display filter.

Information Visible in HTTP

Depending on the request, the packet may expose information such as:

HTTP method
Requested path
Host information
User-Agent information
Other HTTP headers
Application data transmitted through HTTP

Because HTTP does not provide encryption by itself, information sent
through HTTP can potentially be observed by someone who can capture
the traffic.

Evidence
screenshots/04-unencrypted-http.png

11. Why Unencrypted HTTP is Dangerous :-

HTTP traffic is transmitted without the encryption provided by TLS.

If an attacker can observe the network traffic, information carried
in an HTTP request or response may be readable.

Potential risks include:

Information disclosure
Exposure of application data
Credential exposure when insecure authentication is used
Session-related information exposure
Privacy loss

For this reason, sensitive web communications should use HTTPS.

12. How HTTPS Helps

HTTPS is HTTP transmitted over TLS.

TLS provides cryptographic protections that help protect application
traffic against interception and tampering while it is transmitted
between the client and server.

Compared with plain HTTP, HTTPS helps provide:

Confidentiality
Integrity
Server authentication

Therefore, sensitive web applications should use HTTPS rather than
plain HTTP.


13. Wireshark Terminology
Packet

A packet is a unit of data transmitted across a network.

Wireshark displays individual packets so that their headers and
contents can be examined.

Protocol

A protocol is a defined set of rules used by systems to communicate.

Examples observed in the capture include:
TCP
DNS
HTTP
TLS

Port

A port is a logical communication endpoint associated with a network
service or application.

Examples:

TCP 80  → HTTP
TCP 443 → HTTPS

Payload

The payload is the application or data portion carried inside a packet
or protocol message.

The exact data visible depends on whether the communication is
encrypted.

Handshake

A handshake is a sequence of messages used to establish communication
between systems.

In this task, the TCP handshake was:

SYN → SYN-ACK → ACK

14. Security Observations

The packet capture demonstrates several important security concepts.

HTTP

Plain HTTP can expose application-level information because the
traffic is not protected by TLS.

DNS

DNS traffic can reveal information about which domains a system is
querying.

TCP

The TCP three-way handshake provides useful information about how
connections are established.

Packet Analysis

Packet-level inspection helps analysts understand communication
patterns and investigate network behavior.

15. Evidence

The following screenshots document the analysis performed during the
task:

screenshots/
├── 01-http-filter.png
├── 02-dns-filter.png
├── 03-tcp-handshake.png
└── 04-unencrypted-http.png

The complete packet capture is stored as:
wireshark_capture.pcap

16. Project Structure :-
SecurityAnalyst-Intermediate-Task8-Wireshark/
│
├── README.md
├── wireshark_capture.pcap
└── screenshots/
    ├── 01-http-filter.png
    ├── 02-dns-filter.png
    ├── 03-tcp-handshake.png
    └── 04-unencrypted-http.png

17. Ethical Considerations

The packet capture was performed only on a controlled and authorized
local laboratory network.

Network traffic should only be captured on systems or networks that
you own or have explicit permission to monitor.

Traffic from public Wi-Fi, university networks, company networks, or
other third-party environments should not be captured without
authorization.

18. Conclusion

Wireshark was successfully used to capture and analyze live network
traffic on the Kali Linux eth0 interface.

The capture was analyzed using the following display filters:

http
dns
tcp

The HTTP filter was used to isolate web traffic, the DNS filter was
used to identify DNS communication, and the TCP filter was used to
analyze a complete TCP three-way handshake.

The captured handshake demonstrated the sequence:

SYN → SYN-ACK → ACK

An HTTP GET request was also identified as an example of
unencrypted application traffic.
This task demonstrates how packet analysis can help a security analyst
understand network communication, identify information exposed by
unencrypted protocols, and investigate network activity.

19. Disclaimer

This project was performed solely for authorized educational and
security-training purposes in a controlled local laboratory.

Do not capture or analyze network traffic on systems or networks
without explicit authorization.