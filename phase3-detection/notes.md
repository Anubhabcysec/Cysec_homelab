\# Phase 3 — Detection \& Monitoring



\## Wazuh SIEM Setup

\- Version: Wazuh v4.14.5 OVA

\- Dashboard: https://192.168.56.101

\- Agent: kali-attacker (ID: 001) — Active



\## Detections Log

| # | Attack | Wazuh Alert | Rule ID | Level |

|---|---|---|---|---|

| 01 | Nmap Recon | Port scan detected | 533 | 7 |

| 02 | vsftpd Exploit | Coming soon | - | - |

| 03 | Hydra Brute Force | Coming soon | - | - |



\## MITRE ATT\&CK Coverage

| Technique | ID | Status |

|---|---|---|

| Network Service Discovery | T1046 | ✅ Detected |

| Exploit Public App | T1190 | 🔄 Planned |

| Brute Force | T1110 | 🔄 Planned |



\## Key Observations

\- Wazuh requires minimum 4GB RAM to run stable

\- Agent must be restarted after Wazuh server restart

\- Rule level 7+ = medium severity, worth investigating

