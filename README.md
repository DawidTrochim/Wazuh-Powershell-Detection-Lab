# 🛡️ Wazuh SIEM Lab – PowerShell Detection & Visualisation

## 📌 Overview

This project demonstrates the implementation of a SIEM detection pipeline using **Wazuh**, **Sysmon**, and **Kibana** to monitor and detect suspicious PowerShell activity on Windows endpoints.

The lab simulates real-world attack techniques such as:
- Encoded PowerShell execution
- File downloads via PowerShell
- Command shell abuse
- Process spawning anomalies

All events are ingested into Wazuh and visualised using custom dashboards.

---

## 🎯 Scenario

A client requested improved visibility into suspicious PowerShell activity across their environment, specifically:

- Detection of obfuscated (encoded) commands  
- Identification of PowerShell-based downloads  
- Monitoring of abnormal process execution patterns  
- Clear visualisation of alerts for SOC analysts  

To meet this requirement, a Wazuh-based SIEM solution was deployed with Sysmon telemetry and custom detection rules.

---

## 🛠️ Tech Stack

- **Wazuh SIEM (Docker deployment)**
- **Sysmon (Windows endpoint logging)**
- **Kibana (visualisation)**
- **Windows 11 test endpoint**

---

## 🔍 Detection Use Cases

### 1. Encoded PowerShell Execution
- Rule ID: `100100`
- Detects Base64 encoded commands (`-enc`)
- MITRE: `T1059.001`

---

### 2. PowerShell Download Activity
- Rule ID: `100102`
- Detects use of `Invoke-WebRequest`
- MITRE: `T1105`

---

### 3. PowerShell Process Spawning
- Rule ID: `92027`
- Detects PowerShell spawning another PowerShell instance
- MITRE: `T1059.001`

---

### 4. Command Shell Execution
- Rule ID: `92032`
- Detects cmd-based execution (e.g. `whoami`)
- MITRE:
  - `T1059.003`
  - `T1087`

---

## ⚙️ Implementation Steps

### 1. Sysmon Deployment

Sysmon was installed on the Windows endpoint to capture:
- Process creation
- Network connections
- Command-line activity

#### 📸 Sysmon running in Event Viewer
![Sysmon Event Viewer](sysmon_eventviewer.png)

---

### 2. Generating Test Activity

Simulated attack behaviour:

- Encoded PowerShell execution
- PowerShell web requests
- Command shell usage

#### 📸 Triggering PowerShell activity
![Triggering PowerShell](triggering_sysmon_log_powershell.png)

#### 📸 Encoded PowerShell execution
![Encoded PowerShell](sysmon_triggering_encoded_powershell.png)

---

### 3. Log Collection in Wazuh

Sysmon logs were forwarded into Wazuh via OSSEC configuration.

#### 📸 Sysmon logs visible in Wazuh
![Sysmon in Wazuh](sysmon_visible_in_wazuh.png)

#### 📸 Configuration for ingestion
![OSSEC Config](implementing_sysmon_events_into_ossec.png)

---

### 4. Detection Rules

Custom and built-in rules were applied to detect suspicious behaviour.

#### 📸 Editing local rules
![Local Rules](editing_localrules_to_include_sysmon_rule.png)

---

### 5. Alert Generation

Alerts were successfully triggered and logged in Wazuh.

#### 📸 Alerts appearing in Wazuh
![Wazuh Alerts](sysmon_rule_appearing_in_wazuhalerts.png)

---

## 🚨 Detection Examples

### Encoded PowerShell Detection
![Encoded Command Detection](sysmon_encoded_command_detected_wazuh.png)

---

### Download Activity Detection
![Download Detection](rule.id_100102_working.png)

---

### PowerShell Execution Detection
![PowerShell Execution](rule.id_92027_working_builtin_powershell_execution.png)

---

### Command Shell Detection
![CMD Execution](rule.id_92032_cmd_spawning_powershell.png)

---

## 📊 Visualisation (Kibana)

Custom dashboards were created to provide SOC visibility:

- Alert frequency over time  
- Rule-based breakdown of activity  
- Agent-level monitoring  

Example:
- PowerShell alerts table
- Timeline of rule triggers

---

## 🧠 Key Learnings

- Implemented end-to-end SIEM pipeline (log → detection → visualisation)
- Developed understanding of:
  - Sysmon telemetry
  - Wazuh rule engine
  - MITRE ATT&CK mapping
- Gained practical experience simulating attacker techniques

---

## 💼 CV Summary

Built a Wazuh-based SIEM lab integrating Sysmon telemetry to detect and visualise PowerShell-based attack techniques. Implemented custom detection rules, validated alerts, and created Kibana dashboards to support SOC monitoring and analysis.

---

## 📌 MITRE ATT&CK Mapping

| Technique | Description |
|----------|------------|
| T1059.001 | PowerShell execution |
| T1105 | Ingress tool transfer |
| T1059.003 | Command shell |
| T1087 | Account discovery |

---
