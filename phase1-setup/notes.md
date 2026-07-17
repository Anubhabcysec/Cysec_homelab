\# Phase 1 — Lab Setup



\## Network Architecture

\- VirtualBox NAT Network: "Cyberlab" (10.0.2.0/24)

\- Kali Linux: 10.0.2.15 (attacker)

\- Metasploitable 2: 10.0.2.3 (target)

\- Wazuh SIEM: 10.0.2.4 (monitor)

\- Wazuh dashboard: https://192.168.56.101 (host-only adapter)



\## VM Specifications

| VM | RAM | CPUs |

|---|---|---|

| Kali Linux | 3GB | 2 |

| Metasploitable 2 | 1GB | 1 |

| Wazuh v4.14.5 | 5GB | 3 |



\## Issues Encountered and Fixed

\- DHCP collision: both Kali and Metasploitable got same IP → fixed by renewing DHCP

\- NAT vs NAT Network misconfiguration → VMs couldn't ping each other → fixed by switching to NAT Network

\- Wazuh dashboard unreachable from host → fixed by adding host-only adapter (Adapter 2)

\- Metasploitable VMDK UUID mismatch after snapshot → fixed via VBoxManage sethduuid command



\## Wazuh Agent

\- Kali registered as agent: kali-attacker (ID: 001)

\- Status: Active

\- Version: Wazuh v4.14.5

