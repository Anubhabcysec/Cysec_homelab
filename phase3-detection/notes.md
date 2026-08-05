**Phase 3 — Detection \& Monitoring**



*What this phase is about?* 



Running attacks is only half the story. The other half is 

understanding how defenders see those attacks — what shows 

up in logs, what triggers alerts, and what a SOC analyst 

would investigate.



This is where Wazuh comes in.



\---



*What is Wazuh?*



Wazuh is a free, open-source SIEM (Security Information and 

Event Management) platform used by real security teams. It:



\- Collects logs from monitored machines (called agents)

\- Runs rules against those logs to detect suspicious activity

\- Generates alerts with severity levels and descriptions

\- Maps detections to MITRE ATT\&CK framework



In my lab, Kali Linux is registered as a Wazuh agent — 

every command I run, every login, every network connection 

gets logged and sent to the Wazuh server in real time.



\---



*Setup*



| Field | Detail |

|-------|--------|

| Wazuh Version | v4.14.5 OVA |

| Dashboard URL | https://192.168.56.101 |

| Agent | Kali-attacker (ID: 001) |

| Agent Status | Active |

| Agent OS | Kali GNU/Linux 2025.3 |



\---



*How Wazuh alert levels work*



Wazuh assigns every event a severity level from 1-15:



| Level | Meaning |

|---|---|

| 1-3 | Informational — normal system activity |

| 4-6 | Low — worth logging, not urgent |

| 7-9 | Medium — investigate when possible |

| 10-12 | High — investigate soon |

| 13-15 | Critical — immediate response required |



In a real SOC, anything level 7+ gets reviewed. Level 10+ 

pages the on-call analyst.



\---



*Detections from Phase 2 Attacks*



&#x20;       ***Detection 01 — Nmap Reconnaissance***

\- \*\*Wazuh Alert:\*\* Host-based anomaly detection (rootcheck)

\- \*\*Rule ID:\*\* 510

\- \*\*Level:\*\* 7 (Medium)

\- \*\*What Wazuh saw:\*\* Unusual port scanning activity 

&#x20; originating from the Kali agent

\- \*\*Screenshot:\*\* 01-nmap-wazuh-alert.png



\---



&#x20;       ***Detection 02 — Samba Exploitation***

\- \*\*Wazuh Alert:\*\* Successful sudo to ROOT executed

\- \*\*Rule ID:\*\* 5402

\- \*\*Level:\*\* 3 (Informational)

\- \*\*What Wazuh saw:\*\* Privilege escalation to root on 

&#x20; the Kali machine after the reverse shell connected back

\- \*\*Note:\*\* Victim-side detection would require a Wazuh 

&#x20; agent on Metasploitable — which isn't possible due to 

&#x20; its outdated OS



\---



&#x20;       ***Detection 03 — Hydra Brute Force***

\- \*\*Wazuh Alert:\*\* PAM login session events

\- \*\*Rule ID:\*\* 5501

\- \*\*Level:\*\* 3 (Informational)

\- \*\*What Wazuh saw:\*\* Multiple authentication events 

&#x20; from the Kali agent during the brute force attack



\---



&#x20;**MITRE ATT\&CK Coverage :**



| Technique | ID | Detected |

|-----------|----|----------|

| Network Service Discovery | T1046 | ✅ |

| Exploit Public-Facing App | T1190 | ✅ |

| Brute Force: Password Guessing | T1110.001 | ✅ |



\---



**Detection gaps and honest observations**:



Full victim-side detection wasn't possible in this phase 

because Metasploitable 2 runs Ubuntu 8.04 — too old to 

support the modern Wazuh agent. This means Wazuh only 

sees the attacker side (Kali), not the impact on the victim.



In Phase 4, both Windows VMs will have Wazuh agents 

installed — giving complete visibility on both sides of 

every attack. That's where the detection story gets complete.



\---



**What I learned about defensive monitoring:**



\- A SIEM is only as good as its agents — no agent means 

&#x20; no visibility on that machine

\- Alert levels matter — not every event needs immediate 

&#x20; attention, but level 7+ always deserves a look

\- MITRE ATT\&CK mapping turns raw alerts into context — 

&#x20; instead of "suspicious process" you get 

&#x20; "T1190 — Exploit Public-Facing Application"

\- Detection gaps are worth documenting — knowing what 

&#x20; you can't see is as important as knowing what you can

