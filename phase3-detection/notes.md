\# Phase 3 — Detection \& Monitoring



\## Wazuh SIEM Setup

\- Version: Wazuh v4.14.5 OVA

\- Dashboard: https://192.168.56.101

\- Agent: Kali-attacker (ID: 001) — Active



\## Detections Log

| # | Attack | Wazuh Alert | Rule ID | Level |

|---|---|---|---|---|

| 01 | Nmap Recon | Host-based anomaly detection | 510 | 7 |

| 02 | Samba Exploit | Successful sudo to ROOT | 5402 | 3 |

| 03 | Hydra Brute Force | PAM login events | 5501 | 3 |



\## MITRE ATT\&CK Coverage

| Technique | ID | Detected |

|---|---|---|

| Network Service Discovery | T1046 | ✅ |

| Exploit Public-Facing App | T1190 | ✅ |

| Brute Force | T1110.001 | ✅ |



\## Detection Gaps

\- Metasploitable has no Wazuh agent — victim-side logs not captured

\- Full detection chain requires agent on target machine

\- Phase 4 Windows VMs will have agents installed for complete coverage



\## Key Observations

\- Wazuh needs minimum 4GB RAM to run stable

\- Agent must be restarted after Wazuh server restart

\- Rule level 7+ = medium severity, investigate immediately

\- Rule level 10+ = high severity, immediate response required

