\# Phase 2 — Attacks



\## Attack Index

| # | Attack | Tool | Result | Screenshot |

|---|---|---|---|---|

| 01 | Nmap Reconnaissance | nmap | ✅ Network mapped | 01-nmap-kali-output.png |

| 02 | Samba Exploitation | Metasploit | ✅ Root shell obtained | 02-samba-root-shell.png |

| 03 | FTP Brute Force | Hydra | ✅ Password cracked | 03-hydra-cracked.png |



\## MITRE ATT\&CK Coverage

| # | Technique | ID | Tactic |

|---|---|---|---|

| 01 | Network Service Discovery | T1046 | Reconnaissance |

| 02 | Exploit Public-Facing Application | T1190 | Initial Access |

| 03 | Brute Force: Password Guessing | T1110.001 | Credential Access |



\## Target

\- IP: 10.0.2.3 (Metasploitable 2)

\- Attacker: 10.0.2.15 (Kali Linux 2025.3)



\## Key Findings

\- Samba 3.0.20 running with CVE-2007-2447 — unauthenticated root shell

\- FTP running with default credentials msfadmin:msfadmin

\- No account lockout policy on any service

\- Multiple critical services exposed on network

