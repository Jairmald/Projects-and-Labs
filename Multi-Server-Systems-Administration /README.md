# Multi-Server-System-Administration

![Lab Report](https://img.shields.io/badge/Status-Completed-brightgreen)
![Framework](https://img.shields.io/badge/Framework-Active%20Directory-blue)
![Tools](https://img.shields.io/badge/Tools-Windows%20Server%202022-orange)
![Difficulty](https://img.shields.io/badge/Difficulty-Advanced-red)
![Duration](https://img.shields.io/badge/Duration-5%20Weeks-lightblue)

---

## **1. Lab Title**

> Systems Administration Computer Cart: Active Directory Domain Configuration and Management

---

## **2. Purpose and Objectives**

Design and implement a complete Active Directory infrastructure including domain controllers, client machines, virtualization, and network services management.

**Key Learning Outcomes:**
- Install and configure Windows Server 2022 with Active Directory
- Manage 400+ users and implement Group Policy Objects
- Deploy virtual machines on Hyper-V
- Configure DHCP, DNS, and network services
- Implement backup and replication strategies

---

## **3. Frameworks & Technologies**

- **Active Directory Domain Services (AD DS)** — Centralized authentication and authorization
- **Group Policy Management** — Centralized policy deployment
- **DHCP/DNS Services** — Network configuration and name resolution
- **Hyper-V Virtualization** — Multi-OS virtual environment
- **Windows Server Backup** — Disaster recovery and replication

---

## **4. Tools Used**

- Windows Server 2022, Windows 10 Pro, Windows 7, Ubuntu Workstation
- Dell Optiplex 3010, Hyper-V Manager, PowerShell ISE
- Active Directory Users & Computers, Group Policy Editor, Server Manager
- Remote Desktop, Windows Server Backup

---

## **5. Key Procedures**

- Installed Windows Server 2022 and Windows 10 with UEFI BIOS configuration
- Created Active Directory domain (COSE.net) with primary DC and RODC
- Scripted and deployed 400+ users into organizational units via PowerShell
- Configured DHCP scope (192.168.1.50-1.100) for automatic IP assignment
- Deployed software via Group Policy Objects to domain machines
- Created 3 virtual machines (Windows 7, Windows 10, Ubuntu) on Hyper-V
- Enabled Remote Desktop and configured password policies
- Implemented full server backups and DC-to-RODC replication
- Configured wireless network (THEGOONIES SSID, 2.4GHz & 5GHz bands)

---

## **6. Results**

✅ Fully functional Active Directory domain with 400+ users
✅ DHCP scope allocating IPs to client machines
✅ Group Policy software deployment working across domain
✅ 3 virtual machines deployed and 2 joined to domain
✅ Remote Desktop access enabled and tested
✅ DC and RODC replication synced with no errors
✅ Full server backups completed for disaster recovery
✅ Wireless network secured and accessible

---

## **7. Challenges & Solutions**

| Challenge | Solution |
|-----------|----------|
| USB ISO not bootable | Recreated as proper bootable USB image |
| PowerShell script file format error | Converted to `.ps1` script in ISE |
| VM installations very slow | Accepted as hardware limitation; allowed extra time |
| Insufficient RAM for multiple VMs | Added additional RAM stick to host |
| Router web interface incompatible | Used Microsoft Edge browser |
| Windows 10 VM wouldn't boot | Used CTRL+ALT+DEL via Actions menu |
| Ubuntu couldn't join domain | Missing ISO files; configured but not joined |
| ICMP firewall blocking pings | Opened ping rules on firewall |

---

## **8. Key Takeaways**

- BIOS configuration (UEFI, no Legacy, no Secure Boot) is foundational for modern deployments
- PowerShell automation scales user management from hours to minutes
- Group Policy Objects centrally manage hundreds of machines efficiently
- Active Directory replication ensures redundancy and fault tolerance
- Proper IP planning (static servers, DHCP for clients) prevents network conflicts
- Backup strategies are essential; full server backups protect against total failure
- Hardware planning is critical; VM density requires adequate RAM
- Documentation prevents repeated mistakes and saves troubleshooting time

---

## **9. Deliverables**

- Complete Active Directory domain infrastructure (COSE.net)
- 400+ user accounts in organizational units
- PowerShell user creation script
- Group Policy Objects (Software Deployment, Password Policy)
- Virtual machine images (Windows 7, Windows 10, Ubuntu)
- Server backups (DC and Hyper-V hosts)
- Network configuration documentation

---

## **10. Conclusion**

This lab successfully demonstrated enterprise-level system administration through hands-on deployment of Active Directory, user management, virtualization, and network services. The infrastructure supports 400+ users with centralized authentication, automated software deployment, and redundant domain controllers. Real-world challenges such as hardware constraints and software compatibility issues reinforced the importance of planning, troubleshooting, and documentation in systems administration.

---

## **Team**

Jair Maldonado | Yankee Renovato | Grant Keiffer | Dawit Tewelde

---

**Lab Completed:** May 1, 2024 | **Duration:** 5 weeks
