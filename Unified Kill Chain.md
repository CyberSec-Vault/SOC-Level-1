# Unified Kill Chain (UKC) – Complete Phases Reference

The **Unified Kill Chain (UKC)** is an extended cyber attack framework that combines the original Lockheed Martin **Cyber Kill Chain** with the **MITRE ATT&CK** framework.  
It covers **both external intrusion** and **post-compromise** activities, making it useful for detecting, analyzing, and stopping modern cyber attacks — including insider threats.

The UKC breaks an attack into multiple sequential phases.  
Attackers may not follow the order strictly, and some phases can be repeated or skipped depending on the goal.

---

## **Phase 1 – Reconnaissance** (MITRE Tactic TA0043)
**Purpose:** Gather information about the target to plan the attack.  
**Methods:**
- Passive scanning (OSINT, social media, leaked data)
- Active scanning (network probing, port scanning)
**Examples:**
- Mapping network topology
- Finding contact lists for phishing
- Identifying exposed services or vulnerable systems

---

## **Phase 2 – Weaponization** (MITRE Tactic TA0001)
**Purpose:** Prepare the tools and infrastructure needed for the attack.  
**Examples:**
- Setting up Command & Control (C2) servers
- Creating payloads (malware, exploits, phishing pages)
- Configuring systems to catch reverse shells

---

## **Phase 3 – Social Engineering** (MITRE Tactic TA0001)
**Purpose:** Manipulate human behavior to gain access or information.  
**Examples:**
- Sending phishing emails with malicious attachments
- Creating fake login portals
- Impersonating a technician to gain physical access

---

## **Phase 4 – Exploitation** (MITRE Tactic TA0002)
**Purpose:** Exploit vulnerabilities to execute malicious code or commands.  
**Examples:**
- Uploading a reverse shell
- Exploiting a web application vulnerability
- Abusing misconfigured automated scripts

---

## **Phase 5 – Persistence** (MITRE Tactic TA0003)
**Purpose:** Maintain access to the compromised system.  
**Examples:**
- Creating scheduled tasks or services
- Registering the host in a C2 network
- Installing backdoors that trigger on certain events

---

## **Phase 6 – Defence Evasion** (MITRE Tactic TA0005)
**Purpose:** Avoid detection by security measures.  
**Examples:**
- Disabling antivirus or endpoint protection
- Evading web application firewalls (WAF)
- Bypassing intrusion detection systems (IDS)

---

## **Phase 7 – Command & Control (C2)** (MITRE Tactic TA0011)
**Purpose:** Establish a communication channel between attacker and victim system.  
**Examples:**
- Sending stolen data over encrypted channels
- Receiving attacker instructions
- Using compromised systems as pivot points

---

## **Phase 8 – Pivoting** (MITRE Tactic TA0008)
**Purpose:** Use the compromised system as a staging ground to reach deeper into the network.  
**Examples:**
- Tunneling into internal systems
- Using the compromised host to distribute malware

---

## **Phase 9 – Discovery** (MITRE Tactic TA0007)
**Purpose:** Learn about the environment for further exploitation.  
**Examples:**
- Enumerating user accounts and permissions
- Identifying installed software and configurations
- Checking network shares and directories

---

## **Phase 10 – Privilege Escalation** (MITRE Tactic TA0004)
**Purpose:** Gain higher-level access.  
**Targets:**
- SYSTEM / ROOT
- Local Administrator
- Admin-like user accounts
- Users with specific privileged functions

---

## **Phase 11 – Execution** (MITRE Tactic TA0002)
**Purpose:** Run malicious code or payloads to achieve objectives.  
**Examples:**
- Deploying remote trojans
- Running scripts from the C2 server
- Scheduling malicious tasks

---

## **Phase 12 – Credential Access** (MITRE Tactic TA0006)
**Purpose:** Steal usernames and passwords for stealthier access.  
**Examples:**
- Keylogging
- Credential dumping
- Extracting stored browser passwords

---

## **Phase 13 – Lateral Movement** (MITRE Tactic TA0008)
**Purpose:** Move across systems to expand compromise.  
**Techniques:**
- Remote desktop access
- Pass-the-hash or pass-the-ticket attacks
- Using stolen credentials to access additional systems

---

## **Phase 14 – Collection** (MITRE Tactic TA0009)
**Purpose:** Gather valuable data before exfiltration.  
**Targets:**
- Files and directories
- Emails
- Browser data
- Audio and video files

---

## **Phase 15 – Exfiltration** (MITRE Tactic TA0010)
**Purpose:** Steal and transmit collected data outside the target network.  
**Notes:**
- Often encrypted and compressed to avoid detection
- C2 channels/tunnels established earlier are typically used

---

## **Phase 16 – Impact** (MITRE Tactic TA0040)
**Purpose:** Disrupt availability, integrity, or confidentiality of systems and data.  
**Examples:**
- Ransomware encryption
- Website defacement
- Disk wipes and DoS attacks

---

## **Phase 17 – Objectives**
**Purpose:** Achieve the ultimate strategic goal of the attack.  
**Examples:**
- **Financial gain:** Ransomware, payment fraud
- **Reputation damage:** Public release of sensitive data
- **Operational disruption:** Halting business operations

---

## **Why UKC is Important**
- **Comprehensive coverage:** Goes beyond initial intrusion to include post-compromise activity.
- **Improved detection:** Identifies attacks at multiple stages, increasing chances to stop them early.
- **Better defense planning:** Maps defensive measures to each phase.
- **Incident response aid:** Helps security teams analyze and understand attacker behavior.

---

## **Visual Summary**
Reconnaissance → Weaponization → Social Engineering → Exploitation → Persistence → Defence Evasion → C2 → Pivoting → Discovery → Privilege Escalation → Execution → Credential Access → Lateral Movement → Collection → Exfiltration → Impact → Objectives
