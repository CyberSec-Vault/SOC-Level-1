# The Diamond Model of Intrusion Analysis

The **Diamond Model of Intrusion Analysis** is a framework used by cybersecurity professionals to describe and analyze intrusions.  
It emphasizes the relationships between four essential elements: **Adversary**, **Infrastructure**, **Capability**, and **Victim**.

---

## 1. Overview

The model is visualized as a diamond shape, with each corner representing one of the four core features.  
The key principle is that **every intrusion contains all four features**, and understanding the relationship between them helps in **attribution, detection, and defense**.


---

## 2. Core Features

### **2.1 Adversary**
- **Definition:** The individual, group, or nation-state conducting the attack.
- **Examples:**  
  - APT groups like APT28 (Fancy Bear) or APT29 (Cozy Bear)  
  - Cybercriminal gangs  
  - Hacktivist collectives
- **Key Attributes:** Motivation, skill level, resources, and known patterns.

---

### **2.2 Infrastructure**
- **Definition:** The physical or virtual assets used by the adversary to deliver, control, or execute the attack.
- **Examples:**  
  - Command-and-control (C2) servers  
  - Phishing websites  
  - Compromised email accounts  
  - VPN exit nodes
- **Key Attributes:** IP addresses, domains, hosting providers, and anonymization methods.

---

### **2.3 Capability**
- **Definition:** The tools, techniques, and procedures (TTPs) the adversary employs to perform the intrusion.
- **Examples:**  
  - Malware families (e.g., TrickBot, Emotet)  
  - Exploit kits (e.g., EternalBlue)  
  - Ransomware strains (e.g., LockBit, Conti)
- **Key Attributes:** Functionality, sophistication, delivery method, and effectiveness.

---

### **2.4 Victim**
- **Definition:** The target of the attack.
- **Examples:**  
  - An organization, government agency, or individual  
  - Specific devices or systems within a network
- **Key Attributes:** Sector, geographic location, vulnerabilities, and security posture.

---

## 3. Supporting Features

The Diamond Model also includes **meta-features** that provide context for the intrusion:

- **Timestamp:** When the intrusion occurred or was detected.
- **Phase:** The stage of the attack lifecycle (often mapped to the Cyber Kill Chain or MITRE ATT&CK).
- **Result:** The outcome of the intrusion (e.g., data exfiltration, service disruption).
- **Direction:** The movement of the attack (e.g., internal → external, lateral movement).

---

## 4. Benefits of Using the Diamond Model

1. **Attribution**
   - By connecting elements (e.g., the same infrastructure used across multiple attacks), analysts can link campaigns to known adversaries.

2. **Threat Hunting**
   - If you know one feature (e.g., malware type), you can pivot to find related infrastructure or victims.

3. **Incident Response**
   - Guides responders on where to focus investigation and containment efforts.

4. **Pattern Recognition**
   - Helps in identifying recurring attack patterns over time.

---

## 5. Example Scenario

**Scenario:**  
- **Adversary:** APT29 (Cozy Bear)  
- **Infrastructure:** C2 server at `secure-update[.]com` (hosted on VPS in Eastern Europe)  
- **Capability:** Custom backdoor malware with encrypted communication channel  
- **Victim:** European energy sector company

**Analysis Flow:**
1. Start with the **Capability** (malware) found during forensic investigation.
2. Identify its **Infrastructure** (C2 server).
3. Match TTPs and infrastructure patterns to the **Adversary**.
4. Document the **Victim** and assess the impact.
5. Pivot to find other victims and campaigns using the same infrastructure or tools.

---

## 6. Visualization

Below is a simplified **Diamond Model diagram** for the above example:

