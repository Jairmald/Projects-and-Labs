# Honeypot Detection System Implemenation

![Lab Report](https://img.shields.io/badge/Status-Completed-brightgreen)
![Framework](https://img.shields.io/badge/Framework-Deception%20Technology-blue)
![Tools](https://img.shields.io/badge/Tools-Pentbox%20%26%20Kali-orange)
![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-yellow)
![Duration](https://img.shields.io/badge/Duration-2--3%20Hours-lightblue)

---

## **1. Lab Title**

> Honeypot Deployment and Intrusion Detection: Pentbox Configuration and Attack Analysis

---

## **2. Purpose and Objectives**

Deploy and configure Pentbox honeypot on Kali Linux to create decoy systems that detect, log, and analyze unauthorized access attempts. This exercise demonstrates deception-based threat detection and provides insights into attacker behavior and capabilities.

**Key Learning Outcomes:**
- Install and configure Pentbox honeypot framework
- Deploy honeypots using automatic and manual configuration methods
- Monitor intrusion detection and unauthorized access attempts
- Analyze honeypot logs for attacker behavior patterns
- Understand deception technology as a security control
- Implement port-specific honeypots for targeted monitoring
- Document and respond to intrusion attempts

---

## **3. Frameworks & Technologies**

- **Honeypot Technology** — Decoy systems designed to attract and monitor attackers
- **Deception Detection** — Identifying unauthorized access through intentional vulnerabilities
- **Network Emulation** — Simulating vulnerable services without actual vulnerabilities
- **Telnet Protocol** — Legacy remote access protocol (port 23)
- **Pentbox Framework** — Multi-purpose penetration testing and honeypot tool
- **Ruby Scripting** — Pentbox implementation language
- **Intrusion Logging** — Recording and analyzing attack attempts

---

## **4. Lab Environment**

**Host System:** Kali Linux (Penetration Testing Distribution)
**Honeypot Framework:** Pentbox 1.8 (Ruby-based)
**Network Configuration:** Localhost (127.0.0.1) and LAN (192.168.88.0/24)
**Access Methods:** Web browser, SSH terminal, PuTTY client
**Operating System:** Linux kernel with honeypot service

---

## **5. Phase 1: Pentbox Installation and Setup**

### **Step 1: Navigate to Installation Directory**

```bash
$ cd ~/Documents
```

**Purpose:** Create dedicated directory for honeypot framework
**Location:** Home directory Documents folder

---

### **Step 2: Clone Pentbox Repository**

```bash
$ git clone https://github.com/Firefart/pentbox.git
```

**Repository Details:**
- **Repository:** https://github.com/Firefart/pentbox.git
- **Framework:** Pentbox - Penetration Testing Framework
- **Language:** Ruby
- **Purpose:** Multi-tool penetration testing suite with honeypot capabilities

**Git Clone Output:**
```bash
Cloning into 'pentbox'...
remote: Enumerating objects: 287, done.
remote: Counting objects: 100% (287/287), done.
remote: Compressing objects: 100% (165/165), done.
remote: Receiving objects: 100% (287/287), done.
Unpacking objects: 100% (287/287), done.
```

---

### **Step 3: Verify Download Location**

```bash
$ ls
Desktop    Documents    Downloads    pentbox
```

**Verification:**
- Pentbox directory created in home directory
- Repository successfully cloned
- Ready for extraction and configuration

---

### **Step 4: Navigate into Pentbox Directory**

```bash
$ cd pentbox
$ ls
pentbox.tar.gz    README.md    LICENSE    .gitignore
```

**Contents:**
- `pentbox.tar.gz` — Compressed archive of honeypot framework
- `README.md` — Installation and usage documentation
- `LICENSE` — Software license file
- Supporting documentation and configuration files

---

### **Step 5: Extract Pentbox Archive**

```bash
$ tar -zxvf pentbox.tar.gz
```

**Extraction Flags:**
- `-z` — Decompress gzip file
- `-x` — Extract archive contents
- `-v` — Verbose output (show extracted files)
- `-f` — Specify archive filename

**Extraction Output:**
```bash
pentbox-1.8/
pentbox-1.8/pentbox.rb
pentbox-1.8/lib/
pentbox-1.8/lib/pentbox/
pentbox-1.8/lib/pentbox/honeypot.rb
pentbox-1.8/lib/pentbox/network.rb
pentbox-1.8/lib/pentbox/utils.rb
[... additional files ...]
```

---

### **Step 6: Navigate to Extracted Directory**

```bash
$ cd pentbox-1.8
$ ls
pentbox.rb    lib/    README    LICENSE
```

**Directory Structure:**
```
pentbox-1.8/
├── pentbox.rb              (Main executable)
├── lib/
│   └── pentbox/
│       ├── honeypot.rb     (Honeypot module)
│       ├── network.rb      (Network utilities)
│       └── utils.rb        (Utility functions)
├── README                  (Documentation)
└── LICENSE                 (License file)
```

---

### **Step 7: Launch Pentbox Framework**

```bash
$ ruby pentbox.rb
```

**Alternative Execution:**
```bash
$ ./pentbox.rb
```

**Initial Output:**
```
╔═══════════════════════════════════════════════════════════════════════════╗
║                    PenTBox 1.8 - Pentesting Framework                     ║
║                                                                           ║
║   1 - Network Tools                                                       ║
║   2 - Honeypots                                                           ║
║   3 - Forensics                                                           ║
║   4 - VPN Tools                                                           ║
║   5 - Other Tools                                                         ║
║   0 - Exit                                                                ║
╚═══════════════════════════════════════════════════════════════════════════╝

Select an option:
```

---

## **6. Phase 2: Automatic Honeypot Configuration**

### **Step 1: Select Honeypots Module**

```
Select an option: 2
```

**Menu Selection:**
- Navigates to Honeypots section of Pentbox
- Displays available honeypot options

---

### **Step 2: Choose Honeypot Tool**

**Output:**
```
╔═════════════════════════════════════════╗
║         PENTBOX - HONEYPOTS             ║
║                                         ║
║   1 - FTP Honeypot                      ║
║   2 - SSH Honeypot                      ║
║   3 - Honeypot Server                   ║
║   0 - Back                              ║
╚═════════════════════════════════════════╝

Select an option:
```

**Selection:**
```
Select an option: 3
```

**Purpose:** Generic Honeypot Server for multiple protocol support

---

### **Step 3: Select Configuration Method**

**Output:**
```
╔═════════════════════════════════════════╗
║    HONEYPOT CONFIGURATION METHOD        ║
║                                         ║
║   1 - Fast Auto Configuration           ║
║   2 - Manual Configuration              ║
║   0 - Back                              ║
╚═════════════════════════════════════════╝

Select an option:
```

**Selection for Automatic:**
```
Select an option: 1
```

---

### **Step 4: Automatic Configuration Execution**

**Automatic Setup Process:**
```
[*] Initializing Fast Auto Configuration...
[+] Detecting network interfaces...
[+] Interface detected: eth0
[+] Binding honeypot to 127.0.0.1:80 (HTTP)
[+] Binding honeypot to 127.0.0.1:23 (Telnet)
[+] Binding honeypot to 127.0.0.1:21 (FTP)
[+] Setting default honeypot message...
[+] Honeypot started successfully!

[*] Honeypot is now running:
    - HTTP on port 80
    - Telnet on port 23
    - FTP on port 21
    
[*] Monitoring for intrusion attempts...
```

**Honeypot Status:**
- ✅ Running on localhost (127.0.0.1)
- ✅ Multiple ports monitored
- ✅ Ready for intrusion detection

---

## **7. Phase 2: Testing Automatic Honeypot Configuration**

### **Step 1: Identify Honeypot IP Address**

**Open new terminal tab:**
```bash
$ ifconfig
```

**Network Configuration Output:**
```
lo: flags=73<UP,LOOPBACK,RUNNING>
    inet 127.0.0.1  netmask 255.255.255.255
    inet6 ::1  prefixlen 128
    loop txqueuelen 1000 (Local Loopback)
    RX packets 1234  bytes 98765 (98.7 KB)
    TX packets 1234  bytes 98765 (98.7 KB)

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>
    inet 192.168.88.128  netmask 255.255.255.0
    broadcast 192.168.88.255
```

**Target IP:** `127.0.0.1` (localhost)

---

### **Step 2: Access Honeypot via Web Browser**

**Browser Attempt:**
```
Open Firefox
Navigate to: http://127.0.0.1
```

**Expected Response:**
```
HTTP/1.1 403 Forbidden

Access Denied
```

**Honeypot Trigger:**
- Web request received on port 80
- Honeypot identifies as intrusion attempt
- Fake "Access Denied" message displayed
- Attack logged and reported

---

### **Step 3: Monitor Honeypot Alert**

**Pentbox Terminal Output:**
```
[!] ========================================
[!] INTRUSION ATTEMPT DETECTED
[!] ========================================
[*] Timestamp: 2024-04-20 14:32:45.123456
[*] Source IP: 127.0.0.1
[*] Destination Port: 80 (HTTP)
[*] Protocol: TCP
[*] Action: HTTP GET /
[*] Message: Access Denied
[*] Status: LOGGED
[!] ========================================
```

**Alert Details:**
- Source: Local system (127.0.0.1)
- Target: Honeypot HTTP service (port 80)
- Result: Intrusion detected and recorded
- Action: Alert triggered; event logged

**Result:** ✅ Automatic configuration successful; intrusion detected

---

## **8. Phase 3: Manual Honeypot Configuration**

### **Step 1: Launch Pentbox Again**

```bash
$ ruby pentbox.rb
```

---

### **Step 2: Navigate to Honeypots**

```
Select an option: 2  (Honeypots)
Select an option: 3  (Honeypot Server)
```

---

### **Step 3: Select Manual Configuration**

```
Select an option: 2  (Manual Configuration)
```

**Manual Setup Prompt:**
```
[*] Manual Honeypot Configuration
[?] Enter port to monitor (default 80): 23
[?] Enter fake service message: Unauthorized Access - Access DENIED
[?] Enable logging? (y/n): y
[?] Save configuration? (y/n): y

[+] Honeypot configured successfully!
    Port: 23 (Telnet)
    Message: "Unauthorized Access - Access DENIED"
    Logging: Enabled
    Status: Running
```

**Configuration Summary:**
- **Port:** 23 (Telnet)
- **Fake Message:** "Unauthorized Access - Access DENIED"
- **Service Type:** Telnet protocol emulation
- **Logging:** Enabled for intrusion tracking

---

## **9. Phase 3: Testing Manual Honeypot Configuration**

### **Step 1: Identify Target IP Address**

```bash
$ ifconfig | grep "inet "
```

**Output:**
```
inet 192.168.88.128  netmask 255.255.255.0  broadcast 192.168.88.255
inet 127.0.0.1  netmask 255.255.255.255
```

**Target IP:** `192.168.88.128` (LAN address)

---

### **Step 2: Connect via PuTTY from Host Machine**

**PuTTY Configuration:**
```
Host Name: 192.168.88.128
Port: 23
Connection Type: Telnet
```

**PuTTY Connection Attempt:**
```
Connecting to 192.168.88.128:23...
```

**Connection Response:**
```
Unauthorized Access - Access DENIED

Connection closed.
```

**Honeypot Response:**
- Accepts connection on port 23 (Telnet)
- Displays fake security message
- Closes connection immediately
- Logs intrusion attempt

---

### **Step 3: Monitor Honeypot Alert in Kali Terminal**

**Pentbox Output:**
```
[!] ========================================
[!] INTRUSION ATTEMPT DETECTED
[!] ========================================
[*] Timestamp: 2024-04-20 14:45:32.654321
[*] Source IP: 192.168.88.1 (PuTTY client)
[*] Destination Port: 23 (Telnet)
[*] Protocol: TCP
[*] Connection Type: Manual Honeypot
[*] Fake Message Displayed: "Unauthorized Access - Access DENIED"
[*] Action: Telnet connection attempt
[*] Status: LOGGED
[!] ========================================

[*] Intrusion logged to honeypot.log
```

**Alert Analysis:**
- Source: External host (192.168.88.1)
- Target: Honeypot Telnet service (port 23)
- Attack Type: Credential collection attempt
- Response: Fake message + connection termination
- Logging: Event recorded for analysis

**Result:** ✅ Manual configuration successful; attack detected and logged

---

## **10. Honeypot Logs Analysis**

### **Viewing Honeypot Log Files**

```bash
$ cat honeypot.log
```

**Log File Contents:**
```
[2024-04-20 14:32:45] INTRUSION: HTTP access from 127.0.0.1:45234 to port 80
[2024-04-20 14:32:46] ALERT: GET / HTTP/1.1 User-Agent: Mozilla/5.0
[2024-04-20 14:32:47] LOG: Response sent - "Access Denied"

[2024-04-20 14:45:32] INTRUSION: Telnet connection from 192.168.88.1:52341 to port 23
[2024-04-20 14:45:32] ALERT: Connection type: TCP Telnet
[2024-04-20 14:45:33] LOG: Message displayed - "Unauthorized Access - Access DENIED"
[2024-04-20 14:45:33] LOG: Connection closed by honeypot
```

### **Log Analysis Summary**

| Metric | Automatic Config | Manual Config |
|--------|-----------------|--------------|
| Attacks Detected | 1 | 1 |
| Source IPs | 127.0.0.1 | 192.168.88.1 |
| Ports Targeted | 80 (HTTP) | 23 (Telnet) |
| Protocol | HTTP | Telnet |
| Response Time | <1ms | <1ms |
| Status | Logged | Logged |

---

## **11. Honeypot Effectiveness Analysis**

### **Detection Capabilities**

**Automatic Configuration:**
- ✅ HTTP service emulation effective
- ✅ Multiple port monitoring
- ✅ Instant detection and alerting
- ✅ Real-time logging capability

**Manual Configuration:**
- ✅ Port-specific honeypot creation
- ✅ Custom deception messaging
- ✅ Targeted protocol emulation
- ✅ Granular attack logging

### **Attack Pattern Insights**

**From Captured Events:**
1. **Local Access Testing** — 127.0.0.1 accessed HTTP (port 80)
   - Type: Reconnaissance/Testing
   - Intent: Verify honeypot functionality
   - Risk: Low (local testing)

2. **Remote Telnet Access** — 192.168.88.1 attempted Telnet (port 23)
   - Type: Service enumeration
   - Intent: Identify running services
   - Risk: Medium (potential credential attempt)

---

## **12. Key Takeaways**

- **Automatic Configuration:** Fast deployment with pre-configured services
- **Manual Configuration:** Flexible, targeted honeypot creation
- **Detection Effectiveness:** Both configurations successfully detected connection attempts
- **Logging Capability:** All intrusion attempts recorded for analysis
- **Deception Value:** Attackers revealed through honeypot interaction
- **Low Resource Overhead:** Honeypot consumes minimal system resources
- **Valuable Intelligence:** Captured attack patterns inform security decisions
- **Early Warning System:** Honeypots provide first-line threat detection

---

## **13. Honeypot Use Cases**

**Threat Detection:**
- Identify unauthorized access attempts
- Monitor suspicious network activity
- Detect port scanning and enumeration

**Attacker Intelligence:**
- Understand attacker methodologies
- Capture attack timelines and patterns
- Analyze targeting strategies

**Incident Response:**
- Generate alerts for security team
- Provide forensic evidence
- Enable rapid response procedures

**Network Monitoring:**
- Track unauthorized service access
- Monitor unusual port usage
- Identify reconnaissance activities

---

## **14. Limitations & Considerations**

**Honeypot Limitations:**
- Cannot detect sophisticated attacks that skip obvious targets
- Requires active monitoring and response
- False positives possible (legitimate users accessing honeypot)
- Honeypot itself could be compromised if misconfigured
- Resource overhead with multiple concurrent connections

**Security Considerations:**
- Ensure honeypot isolated from production systems
- Monitor honeypot for unauthorized modifications
- Implement network segmentation
- Track honeypot interaction carefully
- Have incident response plan in place

---

## **15. Recommendations**

**Short-Term:**
1. Deploy honeypots on network perimeter
2. Configure port-specific honeypots for critical services
3. Implement centralized logging
4. Set up automated alerts for intrusion attempts
5. Monitor logs regularly for patterns

**Long-Term:**
1. Integrate honeypot with SIEM system
2. Develop incident response playbooks
3. Conduct quarterly threat analysis
4. Expand honeypot deployment across network segments
5. Use honeypot data for security awareness training

---

## **16. Conclusion**

This honeypot lab successfully demonstrated deception-based threat detection through Pentbox deployment on Kali Linux. By implementing both automatic and manual honeypot configurations, the exercise illustrated how decoy systems effectively attract, detect, and log unauthorized access attempts.

The lab revealed that honeypots provide valuable security benefits: immediate detection of reconnaissance activities, detailed logging of attack patterns, and low-cost early warning systems. Attackers targeting the honeypot services revealed their presence through port access attempts, providing security teams with actionable intelligence.

Organizations should consider honeypot deployment as part of comprehensive defense strategy. Combining honeypots with traditional security controls (firewalls, IDS, antivirus) creates multi-layered defense that detects attacks at multiple stages. The intelligence gathered from honeypot interactions enables proactive security hardening and informed incident response procedures.

---

## **17. Artifacts & Deliverables**

- **Pentbox Installation Scripts:** Clone and setup commands
- **Configuration Files:** Automatic and manual honeypot configurations
- **Honeypot Logs:** Complete intrusion attempt records
- **Alert Demonstrations:** Screenshots of detected intrusions
- **Analysis Reports:** Attack pattern and timing analysis
- **Network Topology:** Lab environment diagram
- **Testing Results:** Successful deployment verification

---

## **18. References**

- Pentbox GitHub Repository: https://github.com/Firefart/pentbox
- Pentbox Documentation: https://pentbox.readthedocs.io/
- Honeypot Technology: https://www.owasp.org/index.php/Honeypot
- Deception Detection Framework: https://www.gartner.com/en/topics/honeypot
- Telnet Protocol (RFC 854): https://tools.ietf.org/html/rfc854

---

