# Cyber Kill Chain

The **Cyber Kill Chain** is a framework developed by Lockheed Martin that breaks down a cyber attack into a sequence of stages, showing how an attacker moves from initial planning to achieving their goal.  
It’s mainly used in cybersecurity to understand, detect, and stop attacks at different stages before they succeed.

---

## The 7 Stages of the Cyber Kill Chain

### 1. Reconnaissance
- **Description:** The attacker gathers information about the target (e.g., IP ranges, employee names, exposed services).  
- **Goal:** Identify weaknesses to exploit.  
- **Example:** Using tools like Shodan or OSINT techniques to find vulnerable systems.

### 2. Weaponization
- **Description:** The attacker creates a malicious payload (e.g., malware, exploit code) based on what they learned in reconnaissance.  
- **Goal:** Prepare a weapon tailored to the target’s vulnerabilities.  
- **Example:** Crafting a malicious PDF that exploits a known software flaw.

### 3. Delivery
- **Description:** The attacker sends the malicious payload to the target.  
- **Goal:** Get the weapon in the victim’s environment.  
- **Example:** Phishing emails, malicious USB drives, watering hole websites.

### 4. Exploitation
- **Description:** The malicious payload is triggered, exploiting a vulnerability in the system.  
- **Goal:** Gain initial access.  
- **Example:** Malware exploiting outdated software to run code on the victim’s computer.

### 5. Installation
- **Description:** The attacker installs malware or backdoors for persistent access.  
- **Goal:** Ensure they can return to the system later.  
- **Example:** Installing a remote access trojan (RAT).

### 6. Command and Control (C2)
- **Description:** The compromised system connects to the attacker’s server for instructions.  
- **Goal:** Maintain communication with infected devices.  
- **Example:** Using encrypted channels to send stolen data or receive commands.

### 7. Actions on Objectives
- **Description:** The attacker executes their final goal — stealing data, destroying systems, or spying.  
- **Goal:** Complete their mission.  
- **Example:** Exfiltrating sensitive company files or encrypting data for ransom.

---

## Why It’s Useful
- **Detection:** Spotting the attack early (e.g., during reconnaissance or delivery) can stop it before major damage.
- **Response Planning:** Helps security teams know where to focus defenses.
- **Threat Intelligence:** Shows how attackers operate and where to build countermeasures.
