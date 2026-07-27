\# 🔐 Cybersecurity Home Lab



A personal cybersecurity home lab where I practice real hacking techniques 

and learn how to detect them — built entirely on a personal computer using 

free and open-source tools.



\---



\## 🤔 What is this project?



Think of this lab as a safe, controlled environment where I can:

\- \*\*Attack\*\* a deliberately vulnerable computer

\- \*\*Watch\*\* those attacks get detected by a security monitoring tool

\- \*\*Understand\*\* how real-world cyber attacks work — and how to stop them



Everything runs on my personal computer using virtual machines (VMs) — 

basically computers running inside my computer.



\---



\## 🖥️ The Lab Setup



I have 3 virtual machines all connected on the same private network:

┌─────────────────────────────────────────────────────┐

│ My Computer (Host) 

│ │

│ ┌──────────────┐ attacks ┌──────────────────┐ 

│ │ Kali Linux │ ────────► │ Metasploitable │ 

│ │ (Attacker) │              │ (Victim) │ 

│ │ 10.0.2.15  │              │ 10.0.2.3 │ 

│ └──────────────┘ └──────────────────┘ 

│ │ logs |

│ ▼ │

│ ┌─────────────────┐ │

│ │ Wazuh SIEM 

│ │ (Monitor) 

│ │ 10.0.2.4 

│ └─────────────────┘ │

└─────────────────────────────────────────────────────┘

| VM | What it is | Role |

|---|---|---|

| 🔴 Kali Linux | A hacker's operating system | The attacker |

| 🟡 Metasploitable 2 | A deliberately broken Linux system | The victim |

| 🟢 Wazuh SIEM | A security monitoring dashboard | The detective |



\---



\## ⚔️ Attacks Performed



\### Attack 1 — Network Reconnaissance (Nmap)

\*\*What I did:\*\* Scanned the victim machine to discover open ports and services



\*\*Why it matters:\*\* This is step 1 of any real attack — 

understanding what's running on a target before exploiting it



\*\*Tool:\*\* nmap | \*\*MITRE:\*\* T1046



📸 See: \[phase2-attacks/01-nmap-kali-output.png](phase2-attacks/01-nmap-kali-output.png)



\---



\### Attack 2 — Samba Exploitation (Metasploit)

\*\*What I did:\*\* Exploited a 2007 vulnerability in the Samba file sharing 

service to get a root shell — complete control of the victim machine



\*\*Why it matters:\*\* Unpatched software is one of the most common 

ways attackers get into real systems



\*\*CVE:\*\* CVE-2007-2447 | \*\*CVSS:\*\* 10.0 (Critical) | \*\*Tool:\*\* Metasploit | \*\*MITRE:\*\* T1190



📸 See: \[phase2-attacks/02-samba-root-shell.png](phase2-attacks/02-samba-root-shell.png)



\---



\### Attack 3 — FTP Brute Force (Hydra)

\*\*What I did:\*\* Automatically tried thousands of passwords against 

the FTP service until finding the correct one (msfadmin:msfadmin)



\*\*Why it matters:\*\* Weak and default passwords are still one of the 

most common security failures in real organizations



\*\*Tool:\*\* Hydra | \*\*MITRE:\*\* T1110.001



📸 See: \[phase2-attacks/03-hydra-cracked.png](phase2-attacks/03-hydra-cracked.png)



\---



\## 🛡️ Detection with Wazuh SIEM



All attacks performed in this lab were monitored using \*\*Wazuh SIEM\*\*, which collected logs from the victim machine and generated alerts based on predefined detection rules.



\- \*\*Nmap Reconnaissance:\*\* Wazuh detected network scanning activity and generated an anomaly detection alert (\*\*Rule 510\*\*).

\- \*\*Samba Exploitation:\*\* Successful privilege escalation to the root user was detected, triggering a \*\*Sudo to ROOT\*\* alert (\*\*Rule 5402\*\*).

\- \*\*Hydra Brute Force:\*\* Multiple authentication attempts were identified as a brute-force attack through \*\*PAM login events\*\* (\*\*Rule 5501\*\*).



These detections demonstrate how a SIEM can identify different stages of an attack—from reconnaissance to exploitation and credential-based attacks.

📸 See: \[phase3-detection/01-nmap-wazuh-alert.png](phase3-detection/01-nmap-wazuh-alert.png)



\---



\## 📁 Repository Structure

Cysec\_homelab/

│

├── README.md ← You are here

│

├── phase1-setup/

│ └── notes.md ← Lab setup, networking, config

│

├── phase2-attacks/

│ ├── notes.md ← Attack index and findings

│ ├── 01-nmap-recon.md ← Nmap writeup

│ ├── 02-samba-exploit.md ← Samba CVE writeup

│ ├── 03-hydra-bruteforce.md ← Hydra brute force writeup

│ └── screenshots/ ← Attack screenshots

│

└── phase3-detection/

├── notes.md ← Detection log and analysis

└── screenshots/ ← Wazuh alert screenshots

---



\## 🔧 Tools Used



| Tool | What it does |

|---|---|

| VirtualBox | Runs virtual machines on my PC |

| Kali Linux | Attacker OS with built-in security tools |

| Metasploitable 2 | Intentionally vulnerable practice target |

| Wazuh v4.14.5 | SIEM — collects logs and generates security alerts |

| nmap | Network scanner — discovers hosts and open ports |

| Metasploit | Exploitation framework — automates known CVE attacks |

| Hydra | Password cracker — brute forces login services |



\---



\## 🚀 What's Coming Next



\- \[ ] Active Directory lab (Windows Server 2019 + Windows 10)

\- \[ ] Kerberoasting and Pass-the-Hash attacks

\- \[ ] BloodHound AD enumeration

\- \[ ] Full MITRE ATT\&CK coverage documentation



\---



\## 🎯 Why I Built This



I'm building toward a SOC/Blue Team role in cybersecurity. 

This lab lets me understand attacks from both sides — 

offensive (how attackers think) and defensive (how to detect and stop them).



> \*"To defend a system, you need to understand how it's attacked."\*



\---



\## 👤 About Me



Anubhab | Cybersecurity Enthusiast | Building toward SOC/Blue Team

🔗 \[LinkedIn](https://www.linkedin.com/in/anubhab-das-663477344/)



