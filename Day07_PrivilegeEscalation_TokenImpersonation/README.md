# Day 7 — Privilege Escalation via Token Impersonation

**Incident ID:** INC-20260425-007<br>
**Date:** 25 April 2026<br>
**Severity:** High<br>
**Type:** Privilege Escalation (Access Token Manipulation)<br>
**Client Industry:** BFSI (Banking, Financial Services, Insurance)

---

## What Happened

An attacker with access to a standard user workstation performed privilege escalation by duplicating a privileged access token from LSASS. This allowed them to spawn a process with elevated rights without using credentials, targeting a banking endpoint.

---

## How It Was Detected

A Microsoft Sentinel analytics rule titled “Suspicious LSASS Access via Unusual Parent Process” triggered on abnormal LSASS access initiated by svchost.exe with token-related command-line indicators.

---

## Investigation Summary

**L1:** Identified abnormal LSASS access from svchost.exe with token duplication indicators and escalated due to high risk.

**L2:** Confirmed privilege escalation via SecurityEvent logs (Event ID 4672), traced activity to an unknown executable from temp directory, and validated token impersonation success.

**L3:** Improved detection rule by shifting from command-line keyword reliance to behavioral detection of LSASS access from non-system processes.

---

## Attack Timeline

| Timestamp (IST) | Event                                                    | Data Source         | MITRE Technique            |
| --------------- | -------------------------------------------------------- | ------------------- | -------------------------- |
| 07:41:22        | Unknown executable launched from temp directory          | DeviceProcessEvents | T1059 (Execution)          |
| 09:17:52        | svchost.exe spawns process with token manipulation flags | DeviceProcessEvents | T1134 (Token Manipulation) |
| 09:18:07        | LSASS access initiated                                   | DeviceProcessEvents | T1003 (Credential Access)  |
| 09:19:12        | Special privileges assigned to user                      | SecurityEvent       | T1134                      |
| 09:23:00        | L1 escalation                                            | Sentinel            | —                          |

---

## MITRE ATT&CK

* T1059 — Execution
* T1134 — Access Token Manipulation
* T1003 — OS Credential Dumping

---

## IOCs

| IOC                               | Type    | Source              | Enrichment Result               |
| --------------------------------- | ------- | ------------------- | ------------------------------- |
| FSB-WKS-447                       | Host    | DeviceProcessEvents | Internal asset                  |
| rahul.singh                       | User    | SecurityEvent       | Standard user                   |
| svchost.exe (abnormal invocation) | Process | DeviceProcessEvents | Legit binary, suspicious usage  |
| Unknown.exe (temp path)           | File    | DeviceProcessEvents | No signature, not in VirusTotal |

---

## Containment Actions

* Isolated endpoint FSB-WKS-447 via Defender for Endpoint
* Forced password reset and session invalidation for user
* Revoked all tokens via Azure AD
* Removed and quarantined suspicious executable
* Initiated environment-wide threat hunt

---

## Key Takeaway

Behavior-based detection of LSASS access is critical, as attackers can evade keyword-based rules during privilege escalation.

---

## Tools & Data Sources Used

Microsoft Sentinel, Microsoft Defender for Endpoint, Azure AD, SecurityEvent logs, DeviceProcessEvents, VirusTotal 
