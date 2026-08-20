# Network Reconnaissance using Nmap

## 🎯 Project Overview
This project demonstrates foundational network reconnaissance and vulnerability assessment skills using **Nmap (Network Mapper)**. The goal was to map a local network, identify active hosts, enumerate services, and detect potential security misconfigurations, simulating the initial phases of a professional penetration test.

## 🛠️ Tools & Environment
*   **Tool:** Nmap v7.99 (Network Mapper) + Nmap Scripting Engine (NSE)
*   **Host OS:** Windows 11
*   **Target Environment:** Isolated Home Network Lab (`192.168.1.0/24`)

## 🔍 Methodology
The assessment was conducted systematically to map the attack surface:
1. **Host Discovery:** `nmap -sn 192.168.1.0/24` (Identified 8 active hosts)
2. **TCP Service Detection:** `nmap -sV -p- 192.168.1.1` (Scanned all 65,535 ports)
3. **OS Fingerprinting:** `nmap -O 192.168.1.1` (Identified outdated Linux kernel)
4. **UDP Scanning:** `nmap -sU -p 53,67,68,137,1900 192.168.1.1` (Verified secure UDP posture)
5. **NSE Scripting:** `nmap -sV --script vuln,auth,default 192.168.1.1` (Automated vulnerability checks)

## 🚩 Key Findings
*   🔴 **CRITICAL:** Telnet (Port 23) is enabled on the primary edge router, exposing administrative access to cleartext credential interception.
*   🟠 **HIGH:** The router is running an outdated Linux Kernel (3.10 - 4.11), susceptible to known, unpatched CVEs.
*   🟡 **MEDIUM:** The router's HTTPS service uses a non-standard 10-year SSL certificate validity period, indicating poor cryptographic hygiene.
*   🟢 **POSITIVE:** Dangerous UDP services like UPnP (Port 1900) and NetBIOS (Port 137) were securely closed.

## 🛡️ Remediation Recommendations
1. Immediately disable Telnet on the router and enforce SSH for command-line access.
2. Request a firmware update from the ISP to patch kernel-level vulnerabilities, or replace the hardware if unsupported.
3. Enforce HTTPS-only access for the router's web administration panel.

## 📂 Repository Contents
*   `Network_Reconnaissance_Report.pdf`: A formal, professional penetration testing report detailing the findings, evidence, and remediation steps.
*   `scan_outputs/`: Raw text files containing the Nmap scan results for verification and transparency.

---
*⚠️ **Disclaimer:** This project was conducted strictly on my own personal, isolated home network for educational and portfolio-building purposes. No external or unauthorized systems were scanned.*
