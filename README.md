# Cysec\_homelab

Offensive + Defensive home lab with Kali, Metasploitable 2, and Wazuh SIEM

# Cybersecurity Home Lab



A hands-on offensive + defensive security lab built on VirtualBox to practice real attack techniques and monitor them with a SIEM — documenting the full attack → detect → respond cycle.



\---



\## Lab Architecture



| VM | Role | IP |

|---|---|---|

| Kali Linux 2025.3 | Attacker | 10.0.2.15 |

| Metasploitable 2 | Vulnerable Target | 10.0.2.3 |

| Wazuh v4.14.5 | SIEM / Monitor | 10.0.2.4 |



All VMs connected via VirtualBox NAT Network (Cyberlab - 10.0.2.0/24).

Wazuh dashboard accessible from host via host-only adapter (192.168.56.101).



\---



\## Tools Used



\- \*\*VirtualBox\*\* — hypervisor

\- \*\*Kali Linux\*\* — attacker machine (nmap, metasploit, hydra, john)

\- \*\*Metasploitable 2\*\* — intentionally vulnerable target

\- \*\*Wazuh SIEM\*\* — log collection, alert detection, MITRE ATT\&CK mapping



\---



\## Phases



\### Phase 1 — Lab Setup ✅

\- Deployed 3 VMs on isolated NAT Network

\- Configured Wazuh SIEM with Kali agent (active)

\- Verified VM-to-VM connectivity



\### Phase 2 — Attack + Detection (In Progress)

\- \[ ] Nmap reconnaissance → Wazuh alert

\- \[ ] vsftpd 2.3.4 backdoor exploitation

\- \[ ] Metasploit meterpreter session

\- \[ ] Hydra brute force attack

\- \[ ] Full MITRE ATT\&CK mapping



\### Phase 3 — Active Directory Lab (Planned)

\- \[ ] Windows Server 2019 Domain Controller

\- \[ ] Windows 10 domain-joined workstation

\- \[ ] Kerberoasting, Pass-the-Hash, BloodHound enumeration



\---



\## Documentation Structure



Each attack is documented with:

\- Attack steps and commands used

\- Screenshots of exploitation

\- Wazuh alerts triggered

\- MITRE ATT\&CK technique mapping

\- Defensive mitigation notes



\---



\## Purpose



Building toward a SOC/Blue Team role by practicing both offensive techniques and defensive detection in a controlled environment.

