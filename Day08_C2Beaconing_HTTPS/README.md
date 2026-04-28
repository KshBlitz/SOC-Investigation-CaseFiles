# Day 8 — C2 Beaconing via HTTPS Tunneling

**Incident ID:** INC-20260408-008<br>
**Date:** 08 April 2026<br>
**Severity:** High<br>
**Type:** Command and Control (C2 Beaconing)<br>
**Client Industry:** IT / SaaS

---

## What Happened

A compromised developer workstation established persistent HTTPS communication with an external malicious server using a highly consistent interval pattern. The attacker used this channel to maintain remote access and execute reconnaissance commands while remaining stealthy.

---

## How It Was Detected

Microsoft Sentinel triggered a custom analytics rule detecting consistent outbound HTTPS connections at fixed intervals over several hours, indicating beaconing behavior.

---

## Investigation Summary

**L1:** Priya identified repeated connections to a single external IP with consistent timing and confirmed the IP had a high malicious reputation before escalating

**L2:** Rohan confirmed beaconing behavior, identified PowerShell as the source process, decoded obfuscated commands, and validated active command execution

**L3:** Nisha improved the detection rule by shifting from long-duration volume-based detection to early interval-based behavioral detection

---

## Attack Timeline

| Timestamp (IST) | Event                                              | Data Source         | MITRE Technique |
| --------------- | -------------------------------------------------- | ------------------- | --------------- |
| 17:08           | Initial outbound HTTPS beacon begins               | DeviceNetworkEvents | T1071.001       |
| 17:08–21:11     | Consistent beaconing at ~60 sec interval           | DeviceNetworkEvents | T1071.001       |
| 18:42           | Increased payload size indicating command delivery | DeviceNetworkEvents | T1071.001       |
| 18:42           | PowerShell execution of received instruction       | DeviceProcessEvents | T1059.001       |

---

## MITRE ATT&CK

* T1071.001 — Application Layer Protocol: Web Protocols
* T1059.001 — Command and Scripting Interpreter: PowerShell

---

## IOCs

| IOC                               | Type       | Source              | Enrichment Result                                         |
| --------------------------------- | ---------- | ------------------- | --------------------------------------------------------- |
| 52.184.217.91                     | IP Address | DeviceNetworkEvents | AbuseIPDB: 92% malicious, linked to botnet infrastructure |
| powershell.exe (encoded command)  | Process    | DeviceProcessEvents | Suspicious obfuscated execution pattern                   |
| SHA256 Hash (PowerShell instance) | File Hash  | DeviceProcessEvents | VirusTotal: flagged by 18 security vendors                |

---

## Containment Actions

* Endpoint DEV-LAPTOP-023 isolated via Microsoft Defender for Endpoint
* External IP 52.184.217.91 blocked at firewall and Azure NSG
* IP added to Conditional Access blocked locations list
* Malicious PowerShell processes terminated
* User credentials reset and active sessions revoked
* Full endpoint scan and forensic review initiated

---

## Key Takeaway

Low-volume, highly consistent network traffic patterns are strong indicators of stealthy command-and-control activity and must be detected early through behavioral analysis.

---

## Tools & Data Sources Used

Microsoft Sentinel, Microsoft Defender for Endpoint, CyberChef, AbuseIPDB, VirusTotal, Microsoft Teams, DeviceNetworkEvents, DeviceProcessEvents
