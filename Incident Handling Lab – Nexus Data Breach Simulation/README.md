#  Incident Handling Simulation: Nexus Data Breach

![Lab Report](https://img.shields.io/badge/Status-Completed-brightgreen)
![Framework](https://img.shields.io/badge/Framework-NIST%20800-61%20%7C%20MITRE%20ATT%26CK-blue)
![Tools](https://img.shields.io/badge/Tools-SIEM%2C%20Sysmon%2C%20TheHive%2C%20CyberChef%2C%20VirusTotal-orange)

---

## **1. Lab Title**
> Incident Handling Simulation: Nexus Data Breach Response

---

## **2. Purpose and Objectives**
The objective of this lab is to gain hands-on experience with **incident response, threat hunting, and SOC operations**.  

**Key Learning Outcomes:**
- Apply the **incident response lifecycle** (NIST SP 800-61) in a SOC environment.  
- Conduct **threat hunting and SIEM log analysis** using Wazuh and Sysmon.  
- Investigate **credential compromises and web application vulnerabilities**.  
- Perform **forensic analysis and artifact remediation**.  
- Map attacker techniques to **MITRE ATT&CK** for contextual threat intelligence.

---

## **3. Frameworks, Standards, and Methodologies**
- **NIST SP 800-61:** Provides structured incident handling and response procedures.  
- **MITRE ATT&CK:** Maps tactics, techniques, and procedures (TTPs) for threat analysis.  
- **Defense-in-Depth & RBAC Principles:** Ensures layered security and access control.  
- **Digital Forensics Methodologies:** Memory dump, disk image, and log correlation for evidence collection.

---

## **4. Tools and Technologies**
- **System Environment:** Windows Server 2022, Active Directory  
- **Security Tools:** Wazuh SIEM, Sysmon, TheHive, CyberChef, VirusTotal  
- **Configuration & Automation:** Group Policy Objects (GPO), PowerShell scripts  
- **Utilities:** MD5/Encoding analysis, log correlation, threat intelligence utilities

---

## **5. Procedures and Implementation**
<details>
<summary>Click to expand detailed steps</summary>

1. **Collect logs via Sysmon and integrate with Wazuh SIEM**  
   - Gathered Windows event logs for monitoring system activity and potential threats.

2. **Conduct threat hunting and incident triage**  
   - Verified IoCs including suspicious IP addresses, file hashes, and anomalous network activity.

3. **Investigate credential compromise and portal vulnerabilities**  
   - Analyzed ManageEngine credential breaches and PHP portal exploits for lateral movement and privilege escalation.

4. **Extract and decode threat actor IPs**  
   - Used CyberChef for MD5/encoding analysis and validated IP locations via VirusTotal.

5. **Perform post-incident forensic analysis**  
   - Examined memory dumps, disk images, and correlated logs to identify indicators of compromise.

6. **Remove malicious artifacts and restore systems**  
   - Cleared malware, restored clean system states, and validated configuration integrity.

7. **Map findings to MITRE ATT&CK techniques**  
   - Categorized attacker behaviors to provide context and improve future detection.

8. **Validate incident handling and compliance**  
   - Ensured procedures aligned with NIST SP 800-61 and internal security policies.

</details>

---

## **6. Findings and Results**
- Detected multiple IoCs across endpoints and network traffic.  
- Identified credential compromise and unauthorized privilege escalations.  
- Found GPO-deployed malware and lateral movement within the domain.  
- Successfully remediated artifacts and restored clean system states.  
- Verified threat actor IPs and decoded malicious artifacts.  
- Mapped all detected techniques to MITRE ATT&CK for threat context.  
- SIEM dashboards and alerts validated the effectiveness of monitoring.  
- Post-incident analysis confirmed complete containment and recovery.

---

## **7. Conclusion**
This lab demonstrated practical application of **incident response, threat hunting, and forensic analysis** within a **Windows Server 2022 SOC environment**. By combining **SIEM log correlation, threat intelligence, artifact remediation, and MITRE ATT&CK mapping**, the organization or student can effectively **detect, analyze, contain, and remediate complex cyber incidents** while maintaining compliance with established security frameworks.
