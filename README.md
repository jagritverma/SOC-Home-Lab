#  SOC Home Lab — Wazuh SIEM with Real Attack Simulations

##  Project Overview
Built a fully functional Security Operations Center (SOC) home lab using Wazuh SIEM to monitor a Windows 11 endpoint, detect real attacks, and analyze security events — replicating a real enterprise SOC environment.

---

##  Lab Architecture

<img width="1322" height="827" alt="architecture" src="https://github.com/user-attachments/assets/6642f5b3-5d71-4a3b-8535-e181acf4bdbb" />


---

##  Tools & Technologies

| Tool | Purpose |
|------|---------|
| Wazuh 4.7.5 | SIEM — Log collection, alerting, dashboards |
| Ubuntu 22.04 | Wazuh Server OS |
| Windows 11 | Monitored endpoint (Wazuh Agent) |
| Kali Linux | Attack simulation |
| VirtualBox | Virtualization platform |
| Nmap | Network reconnaissance |
| Hydra | Brute force simulation |
| EICAR | Malware detection testing |

---

##  Wazuh Components Deployed

| Component | Role |
|-----------|------|
| Wazuh Indexer | Log storage (OpenSearch) |
| Wazuh Manager | Log analysis & alerting |
| Wazuh Dashboard | Web UI visualization |
| Wazuh Agent | Endpoint log collection |
| Filebeat | Log shipping to Indexer |

---

##  Attack Simulations & Detections

###  Attack 1 — Network Reconnaissance (Nmap)
- **Tool:** Nmap 7.95
- **Command:** `nmap -sS -sV -O 192.168.56.111`
- **MITRE ATT&CK:** T1046 — Network Service Discovery
- **Findings:** 14 open ports including SMB (445), RPC (135), VMware (902/912)
- **Wazuh Detection:** Windows application error event (Rule 60602, Level 9)

---

###  Attack 2 — SSH Brute Force
- **Tool:** Hydra v9.6 with RockYou wordlist (14M passwords)
- **Command:** `hydra -l ubuntu -P rockyou.txt ssh://10.0.2.4 -t 4`
- **MITRE ATT&CK:** T1110 — Brute Force, T1110.001 — Password Guessing
- **Wazuh Detection:**
  - Rule 5760 (Level 5) — Authentication failed
  - Rule 2502 (Level 10) — User missed password more than once
  - Rule 5758 (Level 8) — Maximum authentication attempts exceeded
- **Compliance Triggered:** PCI-DSS 10.2.4, GDPR IV.32.2, HIPAA 164.312.b, NIST 800-53 AC.7

---

###  Attack 3 — Malware Detection (EICAR)
- **Tool:** EICAR Standard Test File
- **MITRE ATT&CK:** T1587.001 — Develop Capabilities: Malware
- **Wazuh Detection:**
  - Registry Value Integrity Checksum Changed (Rule 750, Level 5)
  - Registry Key Integrity Checksum Changed (Rule 594, Level 5)
  - Windows Defender quarantine activity captured

---

###  Attack 4 — DNS Hijacking Simulation (Hosts File)
- **Method:** Modified Windows hosts file to redirect domain
- **MITRE ATT&CK:** T1565.001 — Data Manipulation: Stored Data
- **Wazuh Detection:** File Integrity Monitoring alert on hosts file change

---

##  Security Configuration Assessment

Ran CIS Microsoft Windows 11 Enterprise Benchmark v1.0.0:

| Metric | Result |
|--------|--------|
| Passed | 126 checks |
| Failed | 261 checks |
| Score  | 32% |

> 261 misconfigurations identified for remediation.

---

##  MITRE ATT&CK Coverage

| Technique | ID | Detection |
|-----------|-----|-----------|
| Network Service Discovery | T1046 |  Detected |
| Brute Force | T1110 | Detected |
| Password Guessing | T1110.001 |  Detected |
| Malware | T1587.001 | Detected |
| Stored Data Manipulation | T1565.001 |  Detected |

---

##  Key Findings

- Successfully deployed enterprise-grade SIEM in home lab
- Monitored 900+ security events in real time
- Detected all 4 simulated attacks with zero false negatives
- Identified 261 Windows security misconfigurations via CIS benchmark
- Mapped all detections to MITRE ATT&CK framework
- Correlated alerts with PCI-DSS, GDPR, HIPAA, NIST compliance frameworks

---

##  Skills Demonstrated

- SIEM deployment and configuration (Wazuh)
- Log analysis and alert triage
- Attack simulation and detection
- Network configuration (NAT, Host-only, Bridged)
- Linux administration (Ubuntu Server)
- Windows endpoint monitoring
- MITRE ATT&CK framework mapping
- Compliance framework understanding

---

##  Screenshots
<img width="300" height="150" alt="Screenshot 2026-04-10 170426" src="https://github.com/user-attachments/assets/9d551e7d-f492-4d44-b203-b3677f469d37" />

<img width="300" height="150" alt="Screenshot 2026-04-11 145501" src="https://github.com/user-attachments/assets/efe1946b-07e3-4864-b918-6a3e6d843f2f" />
<img width="300" height="150" alt="Screenshot 2026-04-05 151152" src="https://github.com/user-attachments/assets/4fd60089-caa8-41ac-8462-401e505f2f37" />
<img width="300" height="150" alt="Screenshot 2026-04-05 155508" src="https://github.com/user-attachments/assets/e272f31b-eed2-400c-823f-fd3e5a29a25a" />
<img width="300" height="150" alt="Screenshot 2026-04-11 161915" src="https://github.com/user-attachments/assets/ae71c855-7989-45a9-b556-955183afa0f4" />
<img width="300" height="150" alt="Screenshot 2026-04-11 145849" src="https://github.com/user-attachments/assets/2069a897-80dd-4bab-b40c-09f2a761c4ac" />

---

## 🔗 References
- [Wazuh Documentation](https://documentation.wazuh.com)
- [MITRE ATT&CK Framework](https://attack.mitre.org)
- [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks)

