# Splunk SOC Detection Engineering Lab

Enterprise-grade SOC Detection Engineering project built using Splunk Enterprise. This lab simulates real-world attack scenarios including SQL Injection, XSS, brute force attacks, account takeover via OTC abuse, vulnerability scanning, and web exploitation attempts using Cloudflare, SSH, and Apache telemetry.

This project demonstrates hands-on expertise in detection engineering, threat hunting, incident investigation, and SIEM operational workflows.

---

# Project Objectives

This lab was designed to simulate a real Security Operations Center (SOC) environment with focus on:

- Detection engineering
- Threat detection and alerting
- Incident investigation workflows
- Attack pattern analysis
- SIEM dashboard engineering
- Threat hunting and attacker profiling

---

# Environment Architecture

Log Sources:

- Cloudflare WAF Logs
- Linux SSH Authentication Logs
- Apache Web Server Logs

SIEM Platform:

- Splunk Enterprise

Detection Types Implemented:

- SQL Injection detection
- Cross-Site Scripting (XSS) detection
- Brute force detection (SSH and Web)
- Account takeover detection via OTC abuse
- Vulnerability scanner detection
- Admin panel access detection
- LFI (Local File Inclusion) detection
- Bot and automation detection

---

# Repository Structure

splunk-soc-detection-engineering-lab/
│
├── dashboards/
│ ├── cloudflare_dashboard.xml
│ ├── ssh_dashboard.xml
│ ├── apache_dashboard.xml
│
├── detections/
│ ├── sql_injection_detection.spl
│ ├── brute_force_detection.spl
│ ├── xss_detection.spl
│ ├── account_takeover_detection.spl
│
├── alerts/
│ ├── brute_force_alert.md
│
├── datasets/
│ ├── cloudflare_logs.json
│ ├── ssh_logs.json
│ ├── apache_logs.json
│
└── incident-response/
├── investigation-guide.md

yaml
Copy code

---

# Detection Engineering Methodology

Detection logic was built using behavioral analysis and attack pattern recognition rather than relying solely on static signatures.

Key detection strategies include:

• High-frequency authentication failures  
• Attack payload pattern matching  
• Abnormal request behavior analysis  
• Attack score correlation  
• Geographic anomaly detection  
• Automation tool fingerprinting (sqlmap, masscan, curl, bots)  
• Suspicious endpoint targeting  

---

# Example Detection: SQL Injection

Detection Logic:

```spl
index=cloudflare_logs
| search ClientRequestURI="*UNION SELECT*" OR ClientRequestURI="*' OR '1'='1*"
| stats count by ClientIP, ClientRequestURI, UserAgent
| where count > 2
Detection identifies automated SQL injection attempts and repeated exploitation attempts.

Example Detection: SSH Brute Force
spl
Copy code
index=ssh_logs "Failed password"
| stats count by src_ip, user
| where count > 10
Detects brute force authentication attempts against SSH service.

Dashboards Implemented
Cloudflare Security Monitoring Dashboard

Capabilities:

Active attack monitoring

Top attacker identification

Attack timeline analysis

Vulnerability scanner detection

SQL injection and XSS monitoring

Risk scoring visualization

SSH Threat Monitoring Dashboard

Capabilities:

Brute force attack detection

Failed login analysis

Geographic attack mapping

Username targeting analysis

Apache Web Monitoring Dashboard

Capabilities:

Web attack pattern detection

Suspicious endpoint monitoring

Bot activity detection

Traffic anomaly visualization

Incident Investigation Workflow
Detection → Alert → Investigation → Attribution → Response

Example Investigation Steps:

Identify suspicious IP

Analyze request patterns

Check attack payload signatures

Review authentication behavior

Correlate across log sources

Determine attack intent

Trigger incident response

Attack Scenarios Simulated
This lab simulates real attacker techniques including:

SQL Injection using sqlmap

pgsql
Copy code
/api/users?id=1 UNION SELECT password FROM users
Cross-Site Scripting (XSS)

javascript
Copy code
/search?q=<script>alert(1)</script>
Credential brute force

nginx
Copy code
Multiple failed SSH authentication attempts
Admin panel discovery

bash
Copy code
/admin
/wp-login.php
/config.php
Vulnerability scanning

makefile
Copy code
User-Agent: masscan
User-Agent: sqlmap
Account takeover attempts via OTC abuse

bash
Copy code
/members/api/verify-otc
Threat Intelligence and Attacker Profiling
This lab identifies attacker characteristics including:

Automation tools used

Attack frequency patterns

Targeted endpoints

Attack success and failure patterns

Geographic source analysis

Skills Demonstrated
Detection Engineering

Threat Hunting

SIEM Engineering

Splunk SPL expertise

Incident Investigation

Log Analysis

Attack Pattern Recognition

Security Monitoring

SOC Operations

Threat Analysis

Tools and Technologies Used
Splunk Enterprise

Cloudflare WAF Logs

Linux SSH Logs

Apache Logs

JSON log ingestion

Splunk SPL

