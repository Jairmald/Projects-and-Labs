# Security Monitoring & SIEM Fundamentals

![Lab Report](https://img.shields.io/badge/Status-Completed-brightgreen)
![Framework](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-blue)
![Tools](https://img.shields.io/badge/Tools-SIEM%2C%20Kibana%2C%20Elasticsearch-orange)
![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-yellow)
![Duration](https://img.shields.io/badge/Duration-120%2B%20minutes-lightblue)

---

## **1. Lab Title**

> Security Monitoring & SIEM Fundamentals: Building Detection Capabilities with the Elastic Stack

---

## **2. Purpose and Objectives**

The objective of this lab is to gain hands-on experience with **SIEM operations, SOC alert triaging, and threat detection** using the Elastic Stack (Kibana & Elasticsearch) to identify and respond to security incidents in enterprise environments.

**Key Learning Outcomes:**
- Build and customize SIEM dashboards from scratch for Windows event log analysis
- Practice data filtering and correlation using Kibana Query Language (KQL)
- Analyze RDP login attempts and group membership changes across 7-year time period
- Simulate SOC Tier 1 triage workflows and escalation processes
- Map detections to MITRE ATT&CK techniques for enhanced threat context
- Identify brute force and lateral movement attack patterns in security logs
- Develop operational procedures for alert classification and severity assessment

---

## **3. Frameworks, Standards, and Methodologies**

- **MITRE ATT&CK:** Comprehensive framework mapping tactics, techniques, and procedures (TTPs) to identify and categorize adversary behaviors across kill chain
- **SOC Tier 1 Triage Methodologies:** Standardized alert classification, severity assessment, and escalation procedures for incident response
- **Defense-in-Depth Principles:** Layered monitoring and detection strategies using multiple event sources and correlation techniques
- **Windows Security Event Logging:** Native OS-level event capture providing visibility into authentication, privilege changes, and system activities
- **Elastic Stack Architecture:** Distributed log aggregation, indexing, and visualization platform for security event analysis

---

## **4. Tools and Technologies**

- **SIEM Platform:** Elastic Stack (Elasticsearch + Kibana)
- **Log Ingestion:** Logstash for Windows event log processing and enrichment
- **Endpoint Monitoring:** 
  - Windows Security Event Logs (Application logs)
  - Windows System Logs
  - RDP/Terminal Services logs
  - Active Directory audit logs
- **Query Language:** Kibana Query Language (KQL) for event filtering and correlation
- **System Environment:** Windows Server / Active Directory domain environment
- **Administrative Tools:** PowerShell for log review and event correlation
- **Data Analysis Period:** January 2018 - December 2025 (7-year historical analysis)

**Technical Stack:**
- Elasticsearch for distributed indexing and search
- Kibana for visualization and dashboard creation
- Logstash pipelines for log parsing and normalization
- Windows Event Log collectors feeding event pipeline

---

## **5. Procedures and Implementation**

<details>
<summary>Click to expand detailed steps</summary>

### **Phase 1: Environment Setup and Log Ingestion**

1. **SIEM Infrastructure Configuration**
   - Deploy Elasticsearch cluster for centralized event indexing
   - Install and configure Kibana for visualization and dashboard creation
   - Set up Logstash pipelines to parse Windows event logs from Application and System sources
   - Configure log forwarding from Windows servers to Logstash collector
   - Validate log ingestion and verify events appearing in Elasticsearch indices
   - Create index patterns in Kibana for windows-logs and security-events
   - Confirm data availability for 2018-2025 timeframe (7-year historical dataset)

2. **Windows Event Log Source Configuration**
   - Enable Windows Application event logging on monitored systems
   - Configure Windows System event logging with appropriate retention policies
   - Verify RDP login event logging is enabled and configured
   - Enable Active Directory group membership change auditing
   - Configure event forwarding to centralized collection point via Windows Event Forwarding (WEF) or local log aggregation
   - Validate event IDs for RDP activity are being captured and sent to Logstash
   - Document event source configuration baseline for compliance

### **Phase 2: Dashboard Development and Customization**

3. **Creating Custom SIEM Dashboard from Scratch**
   - Access Kibana interface and create new dashboard for security monitoring
   - Design dashboard layout with focus on RDP login attempts and group membership changes
   - Create visualization for RDP login attempt activity:
     - Column 1: Timestamp (date/time of attempt)
     - Column 2: Source IP address
     - Column 3: Destination host
     - Column 4: Username
     - Column 5: Status (successful/failed)
     - Add count aggregation to show total RDP attempt volume
   - Create visualization for group membership changes:
     - Column 1: Timestamp (date/time of change)
     - Column 2: User account modified
     - Column 3: Group added/removed from
     - Column 4: Change initiator (admin account)
     - Column 5: Result status
     - Add count aggregation for change frequency analysis
   - Configure time range filters to enable 7-year historical analysis
   - Add drill-down capabilities to pivot from summary to detailed events

4. **Dashboard Visualization Configuration**
   - Set up pie charts showing RDP attempt success/failure distribution
   - Create bar charts displaying RDP attempt volume over time (daily/weekly/monthly aggregations)
   - Build heatmaps correlating source IPs to target hosts for lateral movement detection
   - Configure tables with sorting and filtering capabilities for manual investigation
   - Add count metrics displaying total events, unique source IPs, unique usernames
   - Implement conditional formatting to highlight high-volume or suspicious activity
   - Create annotations for known maintenance windows to reduce false positive investigation time

5. **KQL Query Development and Testing**
   - Write KQL queries to filter RDP login attempts: `event.action:"RDP" AND event.outcome:failed`
   - Create queries for group membership modifications: `event.action:"AddMemberToGroup" OR event.action:"RemoveMemberFromGroup"`
   - Develop correlation queries combining RDP failures with subsequent successful logins on same account
   - Build queries to identify brute force patterns: group RDP failures by username and source IP, alert on threshold
   - Test queries against 2018-2025 dataset to validate accuracy and performance
   - Document query logic and parameters for team reference
   - Optimize queries for dashboard performance and response time

### **Phase 3: Threat Detection and Alert Triage**

6. **Identifying Brute Force Attack Patterns**
   - Define brute force threshold: X failed RDP attempts in Y-minute window from single source IP
   - Use KQL to identify RDP login failures correlated by source IP and timeframe
   - Create detection query: `event.action:"RDP" AND event.outcome:failed | stats count by source.ip, host.name`
   - Analyze volume and timing of failed attempts to identify automated attack tools
   - Cross-reference failed RDP attempts with subsequent successful logins to identify successful compromise
   - Document suspicious source IP ranges and geographic origins
   - Develop exclusion list for known maintenance scripts and legitimate high-volume tools

7. **Detecting Lateral Movement Indicators**
   - Analyze RDP connection chains showing user progression through multiple hosts
   - Build queries identifying unusual RDP connections outside normal business hours
   - Detect rapid RDP connections from single source to multiple destination hosts (horizontal movement)
   - Identify privilege escalation sequences: standard user RDP followed by group membership change to elevated groups
   - Cross-correlate group membership changes with subsequent RDP connection attempts (access provisioning preceding usage)
   - Document lateral movement patterns and timing signatures
   - Create visual representations showing movement paths through network

8. **SOC Tier 1 Alert Triage Workflow**
   - Define alert classification framework:
     - Critical: Active ongoing attack, credential compromise confirmed, data exfiltration indicators
     - High: Multiple failed RDP from external IP followed by successful connection, privilege escalation detected
     - Medium: Unusual RDP activity during off-hours, group membership changes without documentation
     - Low: Isolated failed RDP attempts, routine administrative group changes, expected maintenance activity
   - Establish escalation criteria for each severity level
   - Create triage checklist:
     - Verify alert accuracy (confirm event in raw logs, check for false positives)
     - Determine context (is this expected activity, scheduled maintenance, authorized access?)
     - Assess scope (single host, multiple hosts, department-wide impact?)
     - Identify affected systems and users
     - Document initial investigation findings
     - Determine escalation requirement and target team (IT Ops, System Admins, Incident Response)
   - Document triage decision and route to appropriate team

9. **Alert Escalation Procedures**
   - Route Critical alerts to Incident Response team with 15-minute SLA
   - Escalate High alerts to System Admin team with 1-hour SLA
   - Queue Medium alerts for batch review with 4-hour SLA
   - Log Low alerts for trend analysis and quarterly review
   - Establish feedback loop with escalation recipients for alert tuning
   - Track escalation outcomes to improve classification accuracy
   - Maintain escalation audit trail for compliance and training purposes

### **Phase 4: MITRE ATT&CK Mapping and Threat Context**

10. **Mapping RDP Activity to MITRE ATT&CK Techniques**
    - RDP brute force attempts → **T1110.001 (Brute Force: Password Guessing)** - adversary attempting to compromise accounts through multiple login attempts
    - Successful RDP following brute force → **T1078.002 (Valid Accounts: Domain Accounts)** - attacker using compromised valid credentials for access
    - RDP connections outside business hours → **T1133 (External Remote Services)** - exploitation of remote access services for persistent access
    - RDP lateral movement to sensitive hosts → **T1021.001 (Remote Services: RDP)** - using remote desktop protocol for lateral movement through network
    - Document each detection with MITRE technique reference and tactic category

11. **Mapping Group Membership Changes to MITRE ATT&CK Techniques**
    - Unauthorized group membership additions → **T1098.002 (Account Manipulation: Domain Account)** - modifying user accounts to grant elevated privileges
    - Addition to sensitive groups (Domain Admins, Enterprise Admins) → **T1134.002 (Access Token Manipulation: Create Process with Token)** - escalating privileges through group membership
    - Rapid succession of membership changes → **T1547 (Boot or Logon Autostart Execution)** - potential setup for persistence mechanisms
    - Cross-correlation with RDP activity → **T1550.002 (Use Alternate Authentication Material: Pass the Hash)** - using stolen credentials for lateral movement
    - Document correlation between group changes and subsequent access attempts

12. **Threat Context Documentation**
    - For each detected incident, document:
      - MITRE ATT&CK tactic (e.g., Initial Access, Lateral Movement, Privilege Escalation, Defense Evasion)
      - Associated technique(s) with confidence level
      - Attack chain sequence if multiple techniques detected
      - Potential adversary TTPs based on detected patterns
      - Recommended mitigation or detection enhancement
    - Create threat intelligence reports linking detections to known threat actor profiles
    - Maintai
