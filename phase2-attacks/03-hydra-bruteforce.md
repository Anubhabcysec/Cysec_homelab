\# Attack 03 — Hydra FTP Brute Force



\## CVE/Weakness

CWE-521 — Weak Password Requirements

No account lockout policy on FTP service



\## Attack

\- Tool: Hydra v9.6

\- Service: FTP (port 21)

\- Target: 10.0.2.3 (Metasploitable 2)

\- Wordlist: Custom + rockyou.txt

\- Result: Password cracked ✅

\- Credential found: msfadmin:msfadmin



\## Command Used

hydra -l msfadmin -P \~/lab/custom-pass.txt 10.0.2.3 ftp -t 4 -V



\## MITRE ATT\&CK

\- Tactic: Credential Access

\- Technique: T1110.001 — Brute Force: Password Guessing



\## Remediation

1\. Enforce strong password policy

2\. Implement account lockout after 3-5 failed attempts

3\. Disable FTP — use SFTP instead

4\. Monitor failed login attempts in SIEM

5\. Use multi-factor authentication



\## Key Observation

Default credentials (msfadmin:msfadmin) found on attempt 4 of 8

Real attack would use rockyou.txt (14M passwords)

