# Ransomware Incident Detection - Sigma Rules

##  Scenario Overview

I often stay up to date with recent cybersecurity incidents making waves across public threat feeds and open-source forums. One particular ransomware attack caught my attention — it was dissected in detail by a team of Incident Responders who publicly shared a technical breakdown of the attack chain. 

Inspired by this real-world case, I decided to replicate the scenario in a controlled lab environment and develop Sigma rules that could detect various stages of the attack. This not only helped sharpen my threat detection skills but also created reusable detection logic for similar attacks in enterprise environments.

---

This repository contains custom Sigma rules developed to detect key attacker behaviors from that incident, aiming to enhance our organization's detection and response capabilities moving forward.

---

## Incident Summary

**Attack Chain Breakdown:**

1. **Execution of a malicious HTA payload** via a phishing link.
2. **Abuse of `certutil.exe`** to download the Netcat binary.
3. **Execution of `nc.exe`** to establish a reverse shell.
4. **Enumeration of escalation vectors** using `PowerUp.ps1`.
5. **Abuse of Windows service permissions** to escalate privileges to SYSTEM.
6. **Sensitive data collection** using `7-Zip` archiving.
7. **Exfiltration of data** using `curl.exe`.
8. **Execution of ransomware** appending the `.huntme` extension to encrypted files.

---

## Sigma Rules Developed

| Rule Title                              | Purpose                                                                 |
|----------------------------------------|-------------------------------------------------------------------------|
| `Malicious HTML Application`           | Detects mshta execution triggered via browser-based phishing activity. |
| `Checking the Certutil Download`       | Detects usage of certutil for suspicious binary downloads.             |
| `Finding the Netcat Reverse Shell`     | Detects Netcat reverse shell commands and known Netcat hashes.         |
| `PowerUp.ps1 Enumeration Detected`     | Detects PowerUp.ps1-based privilege enumeration.                       |
| `Suspicious Service Modification`      | Flags potential abuse of service config to escalate privileges.        |
| `7-Zip Sensitive Data Archiving`       | Detects 7z archiving of sensitive paths (e.g., Documents, Desktop).    |
| `cURL Data Exfiltration`               | Detects use of `curl.exe` for outbound POST/PUT operations.            |
| `HuntMe Ransomware Execution`          | Identifies custom ransomware execution by file extension `.huntme`.   |

> All rules are mapped to MITRE ATT&CK where applicable and tuned for Sysmon data.

