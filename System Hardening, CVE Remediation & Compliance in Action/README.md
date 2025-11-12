# 🧰 System Hardening, CVE Remediation & Compliance in Action 🔐

## Overview
This project demonstrates a **Risk Mitigation & Information Security Framework** implementation focused on **system hardening, vulnerability remediation, and ISO/IEC 27002 compliance alignment**.  
The goal was to enhance Acme Corporation’s Windows Server environment through proactive patching, secure configuration, and reduction of the attack surface.

---

## 🧩 Key Objectives
- Identify and remediate known vulnerabilities affecting enterprise systems.  
- Apply technical hardening to critical Windows components and domain services.  
- Align remediation activities with ISO/IEC 27002 security controls.  
- Reinforce the connection between **policy compliance** and **technical enforcement**.

---

## ⚙️ Vulnerability Remediation & Patch Management
- Addressed missing security updates including **CVE-2017-0143 (SMB Remote Code Execution)**, a critical flaw exploited by **WannaCry**.  
- Enabled **automatic Windows Update** and centralized patch management for continuous protection.  
- Validated patch installation through system logs and version checks to ensure integrity.  

> **Key takeaway:** Consistent patching and validation are foundational to maintaining enterprise-grade cyber hygiene.

---

## 🧹 System & Service Hardening
- Disabled unnecessary network services such as **Microsoft FTP (Ports 21–22)** to reduce the domain controller’s exposed surface.  
- Removed unauthorized **third-party remote management tools** to prevent lateral movement and privilege escalation.  
- Verified service states and port closures using `netstat -an` and the **Services MMC console**.  

> **Result:** Reduced potential attack vectors and enforced least-service principle across the environment.

---

## 📜 ISO/IEC 27002 Compliance Mapping
| ISO/IEC 27002 Control | Implementation Example |
|------------------------|------------------------|
| **Technical Vulnerability Management** | Applied patch management to remediate CVE-2017-0143 and other missing updates |
| **Configuration Management** | Disabled unused services, enforced secure baselines |
| **Secure Disposal & Reuse of Equipment** | Ensured removal of unauthorized tools before reuse |
| **Information Security Policy Enforcement** | Aligned password and system policies with organizational standards |

> Aligning remediation efforts with ISO standards ensures traceable compliance and governance integration.

---

## 🧠 Lessons Learned
- Effective **risk mitigation** requires both policy and implementation discipline.  
- Continuous **vulnerability scanning**, **configuration management**, and **automated patching** are key to long-term resilience.  
- Compliance frameworks like **ISO/IEC 27002** provide structure, but it’s the hands-on enforcement that sustains real security posture.

---

## 🏁 Summary
This project showcases how to transform information security policies into technical reality—bridging governance, compliance, and practical hardening to build a secure, standards-aligned Windows infrastructure.

---

**#CyberSecurity #CVE #SystemHardening #ISO27002 #PatchManagement #RiskMitigation #WindowsServer #Compliance #InfoSec**
