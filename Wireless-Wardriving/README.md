# Wireless Wardriving

![Lab Report](https://img.shields.io/badge/Status-Completed-brightgreen)
![Framework](https://img.shields.io/badge/Framework-Wireless%20Security-blue)
![Tools](https://img.shields.io/badge/Tools-Fing%20App-orange)
![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-yellow)
![Duration](https://img.shields.io/badge/Duration-Single%20Session-lightblue)

---

## **1. Lab Title**

> Wardriving Security Assessment: Wireless Network Reconnaissance and Vulnerability Analysis

---

## **2. Purpose and Objectives**

Demonstrate wardriving methodology to identify and analyze nearby wireless networks, assess security posture, and provide hardening recommendations. This exercise highlights how attackers gather wireless network intelligence and the importance of proper security configuration.

**Key Learning Outcomes:**
- Identify wireless networks using passive scanning tools
- Assess wireless security protocols (WPA2, WPA3, open networks)
- Analyze network vulnerabilities and exposure risks
- Develop security recommendations for wireless hardening
- Understand reconnaissance techniques used in network attacks

---

## **3. Frameworks & Technologies**

- **Wireless Security Standards** — WPA2-Enterprise, WPA2-PSK, open networks
- **Passive Network Scanning** — Non-intrusive reconnaissance via Fing app
- **IEEE 802.11 Standards** — 802.11ax (Wi-Fi 6) frequency and channel analysis
- **Network Enumeration** — SSID identification, security classification, signal strength
- **Wireless Hardening** — WPA3 encryption, MAC filtering, firmware updates

---

## **4. Tools & Methodology**

**Device:** iPhone 13
**Scanning Tool:** Fing (passive network discovery app)
**Location:** Personal Home Network
**Scan Date/Time:** March 19, 2025 @ 11:26 PM
**Scan Type:** Passive wireless network enumeration

**Methodology:**
- Launched Fing app on iPhone 13
- Performed automatic network scan
- Documented SSID, security status, frequency, and protocols
- Analyzed results for vulnerability assessment
- Developed security recommendations

---

## **5. Network Scan Results**

**Network 1: ATTwCZhFYs**
- Security Status: 1/5 Secure
- Encryption: WPA2-PSK (implied)
- Frequency: 5 GHz
- Standard: 802.11ac or newer
- Vulnerability: Weak naming convention (default/partial); potentially default credentials

**Network 2: mdaguest**
- Security Status: Unsecured (open network)
- Encryption: None
- Frequency: 5 GHz
- Standard: Wi-Fi 6 (802.11ax)
- Vulnerability: **CRITICAL** — No authentication required; all traffic unencrypted

**Network 3: mda mobile**
- Security Status: 1/5 Secure
- Encryption: WPA2-Enterprise
- Frequency: 5 GHz
- Standard: 802.11ax
- Vulnerability: Enterprise encryption weak; potential credential exposure risk

---

## **6. Detailed Analysis: mda mobile Network**

**SSID:** mda mobile
**Security Classification:** 1/5 Secure (Low)
**Encryption Protocol:** WPA2-Enterprise
**Frequency Band:** 5 GHz
**WiFi Standard:** 802.11ax (Wi-Fi 6)
**Estimated Signal Strength:** Strong (detected clearly from home scan)

**Vulnerability Assessment:**

*Encryption Strength:* WPA2-Enterprise provides stronger authentication than WPA2-PSK but remains vulnerable to:
- Credential harvesting via phishing
- Certificate-based attacks if RADIUS server not properly configured
- Downgrade attacks to WPA if not properly enforced

*SSID Exposure:* "mda mobile" is descriptive and reveals organization type (mobile/telecom), potentially identifying high-value target

*5 GHz Frequency:* Shorter range but less congestion; reduces external eavesdropping but still vulnerable within proximity

*Signal Strength:* Detectable from home location indicates adequate transmission power; increases attack surface area

---

## **7. Security Recommendations**

**For mda mobile Network:**

1. **Upgrade to WPA3 Encryption**
   - Implement WPA3-Enterprise for strongest enterprise security
   - Protects against brute-force attacks via Simultaneous Authentication of Equals (SAE)
   - Recommended: WPA3-Enterprise with 192-bit encryption for sensitive networks

2. **Change Default/Generic SSID**
   - Avoid descriptive names revealing organization (e.g., "mda mobile")
   - Use non-meaningful identifier without company reference
   - Example: "SECURE_NET_5G" instead of "mda mobile"

3. **Disable Wi-Fi Protected Setup (WPS)**
   - WPS vulnerable to brute-force PIN attacks
   - Disable via router admin interface
   - Takes <4 hours to crack with offline attack

4. **Implement MAC Address Filtering**
   - Whitelist only authorized devices
   - Configure router to reject unknown MAC addresses
   - Provides additional access control layer

5. **Enable Strong RADIUS Authentication (Enterprise)**
   - Configure secure RADIUS server with certificate validation
   - Use strong pre-shared key (PSK) for backup
   - Implement certificate pinning to prevent MITM attacks

6. **Regular Firmware Updates**
   - Check manufacturer for latest security patches monthly
   - Enable automatic firmware updates if available
   - Address known CVEs in WiFi drivers and protocols

7. **Disable WPA2 Compatibility Mode**
   - Force WPA3-only if all devices support it
   - Prevents downgrade attacks to older standards
   - Improves encryption consistency

8. **Reduce Transmit Power**
   - Lower signal strength to minimize external visibility
   - Limits range to intended coverage area
   - Reduces attack surface from neighboring locations

---

## **8. General Wardriving Findings**

**Exposure Level: HIGH**

- **3 networks detected** in single home location scan
- **1 network completely unsecured** (mdaguest — open network)
- **2 networks with weak security** (rated 1/5 Secure)
- **0 networks with strong security** (no 4-5/5 ratings observed)

**Attack Vectors Identified:**

1. **Passive Network Discovery** — All networks broadcast SSID; easy target identification
2. **Open Network Access** — mdaguest requires no credentials; complete data exposure
3. **Enterprise Vulnerability** — mda mobile WPA2-Enterprise not properly hardened
4. **Signal Strength** — 5 GHz networks transmitting with strong signal; wide detection range

---

## **9. Risk Assessment by Network**

| Network | Risk Level | Primary Threat | Exploitation Time |
|---------|-----------|-----------------|-----------------|
| mdaguest | **CRITICAL** | Man-in-the-Middle (MITM) | Immediate |
| mda mobile | **HIGH** | Credential Harvesting | Minutes-Hours |
| ATTwCZhFYs | **MEDIUM** | Brute-force, Default Creds | Hours-Days |

---

## **10. Key Takeaways**

- **Wardriving effectiveness:** Passive scanning tools (Fing) require no special permissions yet reveal significant network data
- **Default security insufficient:** WPA2 alone (without WPA3 upgrade) leaves networks vulnerable to modern attacks
- **Open networks critical:** Even guest networks should require minimal authentication; none is unacceptable
- **SSID matters:** Descriptive names reveal organization type and valuable target information
- **Enterprise ≠ Secure:** WPA2-Enterprise without proper RADIUS configuration provides false sense of security
- **Signal strength = Attack surface:** Strong transmit power increases detection range and attack feasibility
- **Regular updates essential:** Firmware patches address discovered vulnerabilities; outdated routers accumulate exploitable flaws

---

## **11. Conclusion**

This wardriving lab successfully demonstrated wireless network reconnaissance methodology and vulnerability assessment. By scanning a personal home environment, three wireless networks were identified with varying security postures, ranging from completely unsecured (mdaguest) to enterprise-encrypted (mda mobile).

Analysis revealed critical security gaps: the absence of WPA3 encryption, descriptive SSIDs, potential WPS vulnerabilities, and insufficient hardening mechanisms. Recommendations focused on upgrading encryption standards, implementing access controls, and regular firmware maintenance.

The exercise highlighted how easily attackers gather wireless network intelligence using publicly available tools and passive scanning techniques. Organizations and individuals should prioritize wireless security configuration, regular updates, and defense-in-depth principles to prevent unauthorized access and data exposure.

---

## **12. Artifacts & Deliverables**

- **Fing Scan Results:** Network enumeration report with 3+ networks identified
- **Security Assessment:** Detailed analysis of mda mobile network vulnerabilities
- **Recommendation Document:** Step-by-step hardening procedures for each identified network
- **Risk Scoring Spreadsheet:** Comparative risk analysis by network
- **Screenshots:** Fing app scan results (SSID, security status, frequency)

---

## **13. Disclaimer**

This wardriving lab was conducted on personal home networks with authorization. All scanning performed passively without connection attempts, credential attacks, or data interception. Wardriving on networks without explicit permission is illegal in most jurisdictions. This exercise is for educational purposes only.

---

**Lab Completed:** March 19, 2025 | **Scan Duration:** ~15 minutes | **Assessed Networks:** 3
