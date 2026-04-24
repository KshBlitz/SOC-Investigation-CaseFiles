# Day 6 — Ransomware Precursor Activity

**Incident ID:** INC-20260421-006<br>
**Date:** 21-Apr-2026<br>
**Severity:** Critical<br>
**Type:** Ransomware Precursor Activity (Pre-Encryption Stage)<br>
**Client Industry:** Manufacturing

---

## What Happened

An attacker executed a multi-stage ransomware precursor attack on an engineering workstation, disabling system recovery mechanisms and backup capabilities. The activity aimed to prepare the environment for future file encryption by removing recovery options and ensuring maximum impact.

---

## How It Was Detected

Microsoft Sentinel triggered multiple alerts for suspicious system recovery modifications, including vssadmin, wbadmin, and bcdedit commands, which were correlated into a high-severity incident.

---

## Investigation Summary

**L1:** Correlated multiple alerts on a single host, confirmed suspicious command execution under a non-privileged user, and escalated to Critical due to ransomware indicators

**L2:** Identified initial infection via malicious Word document leading to PowerShell payload execution and external IP communication; confirmed no encryption occurred yet

**L3:** Improved detection rule to correlate multi-stage ransomware behavior within a time window instead of isolated command alerts

---

## Attack Timeline

| Timestamp (IST) | Event                               | Data Source         | MITRE Technique                 |
| --------------- | ----------------------------------- | ------------------- | ------------------------------- |
| 21:12           | WINWORD.EXE opened document         | DeviceProcessEvents | T1204 — User Execution          |
| 21:14           | PowerShell encoded command executed | DeviceProcessEvents | T1059.001 — PowerShell          |
| 21:15           | External IP connection initiated    | DeviceNetworkEvents | T1105 — Ingress Tool Transfer   |
| 21:52           | net.exe enumeration                 | DeviceProcessEvents | T1087 — Account Discovery       |
| 21:58           | vssadmin delete shadows             | DeviceProcessEvents | T1490 — Inhibit System Recovery |
| 22:05           | wbadmin delete catalog              | DeviceProcessEvents | T1490 — Inhibit System Recovery |
| 22:08           | bcdedit recovery disabled           | DeviceProcessEvents | T1490 — Inhibit System Recovery |

---

## MITRE ATT&CK

* T1204 — User Execution
* T1059.001 — PowerShell
* T1105 — Ingress Tool Transfer
* T1087 — Account Discovery
* T1490 — Inhibit System Recovery

---

## IOCs

| IOC                        | Type    | Source              | Enrichment Result                                |
| -------------------------- | ------- | ------------------- | ------------------------------------------------ |
| 185.224.128.77             | IP      | DeviceNetworkEvents | AbuseIPDB: 92% malicious — known malware hosting |
| Encoded PowerShell payload | Command | DeviceProcessEvents | Obfuscated download cradle                       |
| MT-ENG-WS-047              | Device  | Endpoint            | Compromised host                                 |
| j.patil                    | User    | Identity            | Valid user account, no prior admin behavior      |

---

## Containment Actions

* Isolated device MT-ENG-WS-047 using Microsoft Defender for Endpoint
* Blocked malicious IP 185.224.128.77
* Reset password and revoked sessions for user j.patil
* Initiated full endpoint scan
* Verified backup integrity across environment

---

## Key Takeaway

Ransomware attacks can be stopped before encryption if precursor behaviors like recovery disabling are detected and correlated early.

---

## Tools & Data Sources Used

Microsoft Sentinel, Microsoft Defender for Endpoint, Microsoft Defender for Identity, Microsoft Defender for Office 365, Azure AD, DeviceProcessEvents, DeviceNetworkEvents, DeviceFileEvents, AbuseIPDB, CyberChef 
