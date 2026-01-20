# 🚨 Suspicious PowerShell Command Line Investigation (Microsoft Defender for Endpoint)

## 🛡️📌 Project Overview

This GitHub project documents a **realistic SOC-style incident investigation** based on a **Microsoft Defender for Endpoint alert** triggered by a **Suspicious PowerShell Command Line execution**.
This project focuses on a Suspicious PowerShell Command Line alert. The scenario involves an attacker attempting to bypass execution policies and download a secondary payload (invoice.exe) while remaining hidden from the end-user.
By documenting this incident, I showcase my ability to navigate the Defender for Endpoint portal, interpret the Attack Story, and perform critical remediation actions like device isolation and automated investigations.

This repository is designed for:

- SOC Analysts (L1–L2)
- Blue Team practitioners
- Cybersecurity portfolio demonstrations
- Interview & hands-on learning scenarios

---

## 🛑 Alert Summary
# 🕵️ The Incident: Suspicious PowerShell Execution
# Alert Trigger: Suspicious PowerShell Command Line The Malicious Command:

![image alt](https://github.com/Chrisrajasekar/Suspicious-PowerShell-Command-Line-Investigation/blob/2d408e9fbe08d8caf814cfd1bd439d5ed39202a6/Incident%20Alert.png)


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

   ![image alt](https://github.com/Chrisrajasekar/Suspicious-PowerShell-Command-Line-Investigation/blob/d16293a858cdf3679d62c9b61c49333637911e9b/Attack%20story.png)

The **Attack Story** in Microsoft Defender for Endpoint revealed the following sequence:

- PowerShell launched with obfuscation and execution policy bypass flags  
- Network connection attempt to retrieve an executable payload  
- Payload written to disk using a misleading filename (`invoice.exe`)  
- Immediate execution of the downloaded payload  

---

## 🛠️ Incident Response Actions

### 1️⃣ Identify the Classification

![image alt](https://github.com/Chrisrajasekar/Suspicious-PowerShell-Command-Line-Investigation/blob/d16293a858cdf3679d62c9b61c49333637911e9b/Identify%20the%20classification.png)

- **Confirmed Threat**  
- **Malware Delivery via PowerShell**  
- High-confidence Indicator of Compromise (IOC)  

---

### 2️⃣ Isolate the Device

- Endpoint isolated using **Microsoft Defender for Endpoint**  
- Prevented further lateral movement and command-and-control (C2) communication
  ![image alt](https://github.com/Chrisrajasekar/Suspicious-PowerShell-Command-Line-Investigation/blob/d16293a858cdf3679d62c9b61c49333637911e9b/Isolate%20Device.png)

---

### 3️⃣ Initiate Automated Investigation

- Triggered **Automated Investigation and Response (AIR)**  
- Reviewed investigation graph, evidence, and system verdicts
   ![image alt](https://github.com/Chrisrajasekar/Suspicious-PowerShell-Command-Line-Investigation/blob/d16293a858cdf3679d62c9b61c49333637911e9b/Intiated%20Automated%20investigation.png)

---

### 4️⃣ Run Full Antivirus Scan

- Full antivirus scan initiated

  ![image alt](https://github.com/Chrisrajasekar/Suspicious-PowerShell-Command-Line-Investigation/blob/d16293a858cdf3679d62c9b61c49333637911e9b/Run%20Antivirus%20Scan.png)
---

### 5️⃣ Forensic Investigation – *The “Why”*

Before closing the alert, the following forensic checks were performed:
![image  alt](https://github.com/Chrisrajasekar/Suspicious-PowerShell-Command-Line-Investigation/blob/d16293a858cdf3679d62c9b61c49333637911e9b/Forensic%20Investigation.png)

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
