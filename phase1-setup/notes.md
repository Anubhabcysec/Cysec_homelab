**# Phase 1 — Building the Lab**



*Why I built this?*



Before you can defend a system, you need to understand how it gets 

attacked. This lab gives me a safe, controlled environment to practice 

real attack techniques and learn how defenders detect them — all running 

on my personal computer for free.



\---



*What I built?*



Three virtual machines, all connected on the same private network, 

each playing a different role:



|       VM         |    Role   |  IP Address  |

\-----------------------------------------------

| Kali Linux 2025.3 | The attacker | 10.0.2.15 |

| Metasploitable 2 | The victim | 10.0.2.3 |

| Wazuh v4.14.5 | The detective | 10.0.2.4 |



**Kali Linux** is a security-focused operating system that comes 

pre-loaded with hundreds of hacking and analysis tools. This is 

what I use to launch attacks.



**Metasploitable 2** is a Linux system that was deliberately built 

to be vulnerable — it runs outdated software with known CVEs, 

weak passwords, and misconfigured services. It's essentially a 

practice dummy for learning exploitation safely.



**Wazuh** is a free, open-source SIEM (Security Information and 

Event Management) tool used by real SOC teams. It collects logs 

from monitored machines, detects suspicious activity, and generates 

alerts — exactly like what a security analyst would use at work.



\---



**The Network :>**



All three VMs are connected on a private NAT Network inside 

VirtualBox called "Cyberlab" (10.0.2.0/24). This means:



\- They can all communicate with each other

\- They are completely isolated from the real internet

\- Attack traffic stays contained inside the lab



Wazuh also has a second network adapter (host-only) so I can 

access its web dashboard from my Windows host browser at 

https://192.168.56.101



\---



**Hardware :>**



\- Host machine: Windows 11, 24GB RAM

\- Hypervisor: Oracle VirtualBox



| VM | RAM Allocated | CPUs |

\-----------------------------

| Kali Linux | 3GB | 2 |

| Metasploitable 2 | 1GB | 1 |

| Wazuh SIEM | 6GB | 3 |

**| Total used | 10GB | 6 |**



\---



**Challenges I faced during setup --**



This wasn't plug and play. Here's what actually went wrong 

and how I fixed it — because this is where the real learning happened:



**1. NAT vs NAT Network confusion**

VirtualBox has two options that sound identical — "NAT" and 

"NAT Network". Plain NAT gives each VM its own isolated connection. 

NAT Network puts all VMs on the same shared network. I had both 

VMs on plain NAT, which meant they were completely invisible to 

each other even though they had similar IPs. Switching to NAT 

Network (Cyberlab) fixed it instantly.



**2. DHCP IP collision**

When both Kali and Metasploitable booted at the same time, the 

DHCP server assigned them the same IP address. Solved by releasing 

and renewing Metasploitable's IP so each VM got a unique address.



**3. Wazuh dashboard unreachable from host browser**

The Wazuh dashboard runs on the internal lab network (10.0.2.x) 

which my Windows host can't reach directly. Fixed by adding a 

second network adapter to the Wazuh VM set to "Host-only" mode — 

this gave it a second IP (192.168.56.101) that my host browser 

could reach.



**4. Metasploitable VMDK UUID mismatch**

After taking a snapshot, VirtualBox's internal registry UUID 

didn't match the VMDK file's UUID, causing an "Aborted" error 

on startup. Fixed using VBoxManage to reset the UUID back to 

what the registry expected.



**5. Wazuh running out of RAM**

With all three VMs running simultaneously, Wazuh only had 928MB 

free — not enough to start its services. Fixed by increasing 

Wazuh's RAM allocation from 5GB to 6GB.



\---



**Wazuh Agent Setup**



After getting the dashboard working, I registered Kali Linux 

as a monitored agent inside Wazuh:



\- Agent name: Kali-attacker

\- Agent ID: 001

\- Status: Active

\- This means every suspicious action on Kali gets logged 

&#x20; and sent to the Wazuh dashboard in real time



\---



**What I learned from just the setup :-->**



Honestly, the setup phase taught me as much as the attacks did:



\- The difference between NAT, NAT Network, and Host-only 

&#x20; networking — and when to use each

\- How DHCP works and what happens when two machines get the 

&#x20; same IP

\- How SIEM agents work — they run as a background service 

&#x20; on the monitored machine and forward logs to the central server

\- How VirtualBox manages disk UUIDs and why moving files 

&#x20; breaks registrations

\- Why RAM planning matters when running multiple VMs — 

&#x20; services silently fail when memory runs out



None of this was in a tutorial. It came from hitting errors 

and figuring out why.

