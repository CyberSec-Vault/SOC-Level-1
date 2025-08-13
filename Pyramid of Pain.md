# Pyramid of Pain — Complete Guide

**Model author:** David J. Bianco  
**Purpose:** Show which kinds of indicators of compromise (IOCs) cause the most **“pain”** to an adversary when you detect, block, or hunt for them.  
**Key idea:** The higher you go, the harder (and costlier) it is for attackers to adapt—so prioritize detections **higher** up the pyramid.

```
          TTPs (hardest to change)      ← Highest pain
                 Tools
        Network/Host Artifacts
              Domain Names
               IP Addresses
              Hash Values              ← Lowest pain
```

---

## Summary (Plain Terms)
It’s a six-level hierarchy of IOCs. **Hashes/IPs/domains** are easy for attackers to swap, so detections there have short shelf lives. **Artifacts/Tools/TTPs** force adversaries to reconfigure code, rebuild infrastructure, or change habits—this is expensive and error-prone, so those detections inflict more pain.

---

## Snapshot Table

| Level (bottom → top) | What it is | Typical attacker reaction | Defender use | Pain to attacker |
|---|---|---|---|---|
| **Hash Values** | File fingerprints (MD5/SHA1/SHA256) | Recompile/pack → new hash in seconds | Exact blocklists, malware triage | Low |
| **IP Addresses** | Source/destination IPs | Rotate VPS/proxy/CDN → minutes–hours | Short-term blocks, triage, pivoting | Low–Medium |
| **Domain Names** | FQDNs for C2/phishing/staging | Register/rotate/DGA → hours–days | DNS blocks/sinks, telemetry pivots | Medium |
| **Network/Host Artifacts** | Registry keys, mutexes, URIs, file/process patterns, JA3/JA4 | Code/config changes → days | Behavior-leaning rules & hunts | Medium–High |
| **Tools** | Frameworks/utilities (e.g., Cobalt Strike, Sliver, Rubeus) | Replace toolchain, retrain ops → days–weeks | YARA/Sigma/EDR analytics | High |
| **TTPs** | Tactics/Techniques/Procedures (tradecraft) | Change methods & playbooks → weeks+ | Behavior analytics, ATT&CK-mapped detections | Highest |

---

## The Six Levels (Bottom → Top)

### 1) Hash Values (MD5/SHA1/SHA256)
- **What:** Fingerprints of specific files.  
- **Attacker reaction:** Recompile/pack → new hash in seconds.  
- **Use:** Good for exact matches, but brittle and short-lived. Best used for triage and short-term blocking.

### 2) IP Addresses
- **What:** Source/destination IPs used by the adversary.  
- **Attacker reaction:** Rotate proxies/cloud hosts/CDNs → minutes to hours.  
- **Use:** Helpful in short bursts; expires quickly. Treat as *perishable* intel.

### 3) Domain Names
- **What:** FQDNs used for C2, staging, or phishing.  
- **Attacker reaction:** Register new domains, use DGA/fast-flux → hours to days.  
- **Use:** More durable than IPs but still rotatable. Combine with DNS telemetry and WHOIS/hosting pivots.

### 4) Network/Host Artifacts
- **What:** Repeated patterns on the wire or endpoints (e.g., URI paths, mutex names, registry keys, file names, process trees, PowerShell blocks, JA3/JA4 TLS fingerprints).  
- **Attacker reaction:** Requires code/config changes → days.  
- **Use:** Stronger signals; generalizes beyond a single sample; great material for hunts and analytic detections.

### 5) Tools
- **What:** The frameworks/utilities actors rely on (e.g., Cobalt Strike beacons, Sliver, Rubeus, custom loaders).  
- **Attacker reaction:** Replace toolchains, rebuild infra, retrain operators → days to weeks.  
- **Use:** YARA/Sigma detections, EDR behavior analytics, memory scanning, protocol heuristics.

### 6) TTPs (Tactics, Techniques, and Procedures)
- **What:** The actor’s **methods**—how they phish, move laterally, persist, and exfiltrate (map to MITRE ATT&CK).  
- **Attacker reaction:** Change tradecraft/process → costly retooling and practice → weeks+ (and mistakes happen).  
- **Use:** Behavior analytics, anomaly detection, detections mapped to ATT&CK; purple teaming to validate coverage.

---

## Defender Playbook (How to Use the Pyramid)

- **Prioritize higher levels.** Don’t stop at hashes/IPs; invest in behavior detections.  
- **Generalize rules.** Turn one IOC into patterns (paths, headers, command lines, parent–child process chains).  
- **Map to ATT&CK.** Track technique coverage (e.g., T1059 Command Shell, T1003 Credential Dumping, T1021 Remote Services).  
- **Hunt with hypotheses.** “If they live-off-the-land for lateral movement, I should see X, Y, Z in logs.”  
- **Manage IOC decay.** Rotate low-level IOCs often; keep long-lived behavioral detections.  
- **Instrument the kill chain.** Ensure telemetry across email gateway, proxy, EDR, identity/AD, DNS, and cloud control plane.  
- **Measure pain.** Ask: “If we detected/blocked this, how expensive is it for the adversary to adapt?” Prefer the higher-pain option.

---

## Quick Example

You catch a malicious EXE:
- **Low:** Block its **hash** (easy to evade).  
- **Better:** Detect **persistence artifacts** (specific Run key + filename pattern).  
- **Best:** Detect the **TTP**: *“Remote service creation + immediate WMI/WinRM execution + LSASS handle open”* → nails the behavior even if the file and infra change.

---

## Implementation Snippets (Illustrative)

### Sigma (Windows – Suspicious Remote Service Creation)
```yaml
title: Suspicious Remote Service Creation (Behavioral)
id: 7b1b9a44-8f2a-4b8e-9a2d-remote-service
status: experimental
logsource:
  product: windows
  service: system
detection:
  selection:
    EventID: 7045
  suspicious_path:
    ImagePath|contains:
      - "\\*\ADMIN$"
      - "cmd.exe /c sc \\"
      - "psexesvc"
  condition: selection and suspicious_path
level: high
tags:
  - attack.persistence
  - attack.t1543.003
```

### Pseudo EDR Analytic (Process Chain Heuristic)
```text
IF (ParentProcess == wmic.exe OR powershell.exe with Invoke-WmiMethod/Invoke-Command)
AND (ChildProcess == sc.exe OR services.exe creating new service)
AND (Within 120s, lsass.exe is opened with PROCESS_VM_READ by a new process)
THEN raise high-severity alert: "Likely lateral movement with credential access"
```

*(Note: Snippets are simplified for illustration; adapt to your telemetry & schema.)*

---

## TL;DR
- Bottom = cheap for attackers to change → **low pain**.  
- Top = expensive to change habits/workflows → **high pain**.  
- Focus detections and hunts **up the pyramid** to make intrusions costly and short-lived.

---

### Attribution
Pyramid of Pain model by **David J. Bianco**.
