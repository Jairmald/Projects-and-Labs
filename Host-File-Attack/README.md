# Host File Attack Report

![Lab Report](https://img.shields.io/badge/Status-Completed-brightgreen)
![Framework](https://img.shields.io/badge/Framework-DNS%20Spoofing-blue)
![Tools](https://img.shields.io/badge/Tools-Hosts%20File-orange)
![Difficulty](https://img.shields.io/badge/Difficulty-Beginner-yellow)
![Duration](https://img.shields.io/badge/Duration-30%20Minutes-lightblue)

---

## **1. Lab Title**

> Hosts File Manipulation Attack: Local DNS Spoofing and Traffic Redirection

---

## **2. Purpose and Objectives**

Simulate a hosts file attack to demonstrate how attackers manipulate local DNS resolution for malicious purposes. This exercise illustrates client-side DNS spoofing vulnerabilities and the potential for phishing, credential harvesting, and malware distribution.

**Key Learning Outcomes:**
- Understand local DNS resolution hierarchy and hosts file priority
- Modify hosts file to redirect domain traffic
- Verify DNS redirection via ping and browser testing
- Identify attack vectors and endpoint protection solutions
- Develop defensive strategies against DNS spoofing attacks

---

## **3. Frameworks & Technologies**

- **DNS Resolution** — Domain Name System name-to-IP translation process
- **Hosts File Mechanism** — Local DNS cache that overrides network queries
- **DNS Spoofing** — Redirecting DNS requests to malicious IP addresses
- **Endpoint Protection** — UAC, file integrity monitoring, DNS monitoring
- **Attack Methodology** — Local access exploitation for credential harvesting

---

## **4. Lab Environment**

**Operating System:** Windows 10 / 11
**Administrator Access:** Required
**Tools Used:**
- Notepad (Run as Administrator)
- Web Browser (Chrome/Edge/Firefox)
- Command Prompt
- Ping utility for DNS verification

**Attack Method:** Local hosts file modification (requires administrator privileges)

---

## **5. Procedures & Results**

**Step 1: Verify Normal Website Access**
- Opened browser and accessed www.google.com → Loaded Google homepage correctly
- Accessed www.msn.com → Loaded MSN homepage correctly
- Verified DNS resolution working normally

**Step 2: Access Websites via IP Address**
- Navigated to http://172.217.1.228 (Google's IP) → Verified Google page loaded
- Navigated to http://204.79.197.203 (MSN's IP) → Verified MSN page loaded
- Confirmed IP-to-domain resolution accuracy

**Step 3: Modify Hosts File**
- Opened Notepad as Administrator
- Navigated to: `C:\Windows\System32\drivers\etc\hosts`
- Changed file filter from "Text Documents (.txt)" to "All Files (.*)"
- Added spoofed entry: `204.79.197.203    www.google.com`
- Saved file with administrator privileges

**Step 4: Test DNS Redirection**
- Opened Command Prompt
- Executed: `ping www.google.com`
- **Result:** Ping resolved to 204.79.197.203 (MSN's IP) instead of Google's IP
- Confirmed hosts file override successful
- Accessed www.google.com in browser → Loaded MSN homepage instead

**Step 5: Restore Original Configuration**
- Removed spoofed entry from hosts file
- Saved changes
- Verified Google.com resolved to correct IP address
- Confirmed attack reversed

---

## **6. Attack Analysis**

**DNS Resolution Order (Windows Priority):**
1. Local hosts file (highest priority)
2. Browser DNS cache
3. OS DNS cache
4. Network DNS resolver (ISP/corporate)

**Attack Success Factors:**
- Hosts file checked before network DNS queries
- Single entry redirects all traffic for domain
- No user notification of redirection
- Works for both IP access and hostname access

**Attack Impact:**
- User unknowingly visits unintended website
- Credentials can be harvested from spoofed login pages
- Malware distributed from fake sites
- SSL certificates don't prevent hosts file spoofing (IP-based bypass)

---

## **7. Vulnerability Assessment**

| Vulnerability | Severity | Impact |
|---------------|----------|--------|
| Hosts file accessible with admin rights | **HIGH** | Attacker can redirect all domain traffic |
| No user notification of redirection | **HIGH** | User unaware of DNS spoofing |
| Browser displays spoofed site normally | **CRITICAL** | User trusts content as legitimate |
| Multiple domains redirectable | **HIGH** | Widespread attack surface |
| No integrity monitoring (default) | **MEDIUM** | Modification undetected without monitoring |

---

## **8. Attack Scenarios**

**Scenario 1: Credential Harvesting**
- Attacker redirects `www.bankofamerica.com` to fake login page
- User enters credentials thinking accessing legitimate bank
- Credentials stolen; account compromised

**Scenario 2: Malware Distribution**
- Attacker redirects `www.adobe.com` to malware-hosting server
- User downloads "software update" containing malware
- System compromised; data exfiltrated

**Scenario 3: Phishing Campaign**
- Attacker redirects `www.office365.com` to phishing page
- User "verifies" credentials after "session timeout"
- Enterprise credentials stolen; lateral movement enabled

---

## **9. Defense Mechanisms**

**Endpoint Protection:**
- **User Access Control (UAC)** — Requires confirmation for admin file modifications
- **File Integrity Monitoring (FIM)** — Detects hosts file changes in real-time
- **DNS Monitoring** — Alerts on unusual DNS resolution patterns
- **DNSSEC** — Cryptographic validation of DNS responses (network-level)

**Hosts File Hardening:**
- Set hosts file read-only attributes (requires bypass for modification)
- Enable Windows Defender against known malware
- Monitor administrative privilege usage
- Regular hosts file audits and baselines

**User Awareness:**
- Verify SSL certificates match expected website
- Check URL bar for correct domain (not just IP)
- Use HTTPS to prevent MITM interception
- Enable DNS-over-HTTPS (DoH) to prevent redirection
- Monitor for unexpected site behavior or login prompts

---

## **10. Key Takeaways**

- **Local DNS priority matters:** Hosts file checked before network DNS; highest priority resolution
- **Admin access required:** Attack requires local system access or malware with elevated privileges
- **Trust is dangerous:** Users trust sites loaded via familiar URLs without verifying legitimacy
- **Multiple attack vectors:** Credential theft, malware distribution, and phishing all possible
- **SSL insufficient:** HTTPS certificates don't prevent hosts file spoofing (IP-based connection)
- **Endpoint protection essential:** UAC, FIM, and DNS monitoring critical for prevention
- **Defense-in-depth required:** Single security layer insufficient; multiple controls needed

---

## **11. Conclusion**

This hosts file attack lab successfully demonstrated local DNS spoofing methodology and its potential for malicious exploitation. By redirecting www.google.com traffic to MSN's IP address, the exercise illustrated how attackers can manipulate domain resolution without network-level access or ISP compromise.

The attack requires administrator privileges, making it most effective via malware deployment or local access. However, its impact is severe: users can be redirected to phishing pages, malware repositories, or credential harvesting sites while believing they access legitimate services.

Defense strategies include endpoint protection (UAC, FIM, DNS monitoring), cryptographic validation (DNSSEC, DoH), and user awareness training. Organizations should implement file integrity monitoring on critical system files and monitor administrative privilege usage to detect and prevent hosts file modifications.

---

## **12. Artifacts & Deliverables**

- **Hosts File Backup:** Original unmodified hosts file copy
- **Modified Hosts File:** Spoofed entry example (archived safely)
- **DNS Resolution Screenshots:** Before/after ping results showing redirection
- **Browser Screenshots:** MSN page loaded when accessing Google URL
- **Command Output:** `ping www.google.com` showing 204.79.197.203 resolution

---
