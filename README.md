# Snort Ruleset Protections
![Tested OS: Ubuntu 24.04.1 x64](https://img.shields.io/badge/Tested%20OS-Ubuntu%2024.04.1%20x64-green)
![Snort](https://img.shields.io/badge/Snort-version%202.9.20-red) 
![TeamSpeak 3 version 3.13.7 Linux](https://img.shields.io/badge/TeamSpeak%203%20version%203.13.7%20Linux-blue)


### Anti ddos

This Snort ruleset contains various protections against network attacks, including measures specifically designed for securing TeamSpeak 3 servers. Below is a summary of the protections provided and instructions on integrating these rules into your Snort deployment.

---
How to Add Rules to Snort:

1. edit config  ```nano /etc/snort/snort.conf```
2. add this **include $RULE_PATH/local.rules** (if it's not already there)
3. save ctrl+x y
4. add [local.rules](https://github.com/Yamiru/anti-ddos-snort-rules/blob/main/local.rules) to /etc/snort/rules/local.rules
5. test snort ```snort -T -c /etc/snort/snort.conf```



---
# Protections Provided:

## **1. ICMP (Internet Control Message Protocol) Attack Protections**
- **ICMP Echo Request**: Detects frequent ICMP echo requests (potential ping sweeps or floods).
- **ICMP Flood**: Flags ICMP packets exceeding a size threshold, indicating flood attempts.
- **ICMP Fragmentation Flood**: Detects fragmented ICMP packets, often used in evasion techniques.
- **Smurf Attack**: Detects ICMP packets indicative of a Smurf amplification attack.
- **Ping of Death**: Flags oversized ICMP packets that may cause buffer overflows.

---

## **2. UDP (User Datagram Protocol) Attack Protections**
- **Bandwidth Flood**: Detects UDP traffic patterns indicative of a flood attack.
- **Fragmentation Flood**: Identifies fragmented UDP packets, suggesting potential exploits.
- **SSDP Amplification**: Detects SSDP amplification attacks leveraging "ssdp:alive" messages.
- **CHARGEN Amplification**: Identifies flood attacks using CHARGEN protocol.
- **SNMP Amplification**: Detects use of SNMP responses in amplification attacks.
- **VoIP Flood**: Flags excessive "INVITE" messages, often used in VoIP DoS attacks.

---

## **3. TCP (Transmission Control Protocol) Attack Protections**
- **SYN Amplification/Flood**: Detects excessive SYN packets, typical in DoS attacks.
- **ACK Amplification/Flood**: Flags excessive ACK packets used in some DoS strategies.
- **RST/FIN Floods**: Identifies excessive TCP RST or FIN packets indicative of flooding.
- **Spoofed Session Flood**: Flags TCP sessions with suspicious or spoofed headers.
- **LAND Attack**: Detects packets with source and destination addresses set to the same value.
- **Slowloris Attack**: Detects prolonged TCP sessions, often used to exhaust server resources.

---

## **4. DNS Amplification Attack Protections**
- **DNS Amplification**: Detects amplification attacks exploiting DNS response payloads.

---

## **5. NTP (Network Time Protocol) Amplification Protections**
- **NTP Amplification**: Identifies amplified responses from misconfigured NTP servers.

---

## **6. HTTP Attack Protections**
- **HTTP GET Flood**: Flags high-frequency GET requests aimed at overwhelming web servers.
- **Recursive HTTP GET Flood**: Detects looping GET requests.

---

## **7. Smurf and Fraggle Attacks**
- **Smurf Attack**: Flags ICMP packets used in Smurf-style amplification.
- **Fraggle Attack**: Detects UDP packets similar to Smurf, leveraging UDP echoes.

---

## **8. General IP Protections**
- **IP Null Attack**: Detects packets with protocol set to 0, a technique used in evasion.
- **Zero-Day DDoS**: Identifies suspicious patterns indicating new DDoS attacks.

---

## **9. ReDoS (Regular Expression Denial of Service) Protections**
- **ReDoS**: Detects patterns in traffic indicative of regex-based resource exhaustion attacks.

---

## **10. Application-Specific Protections**
- **TeamSpeak 3**:
  - Brute force attempts.
  - Flood attacks.
  - Excessive join requests.
- **VoIP (e.g., SIP)**: Detects high-frequency INVITE messages.

---

## **11. Amplification Attacks**
- **SSDP, CHARGEN, DNS, and NTP**: Flags amplification-based DDoS attacks leveraging misconfigured services.
