# Day 03 — Pass-the-Hash Lateral Movement

**Incident ID:** INC-20260414-003<br>
**Date:** 14 April 2026<br>
**Severity:** Critical<br>
**Type:** Lateral Movement via Pass-the-Hash<br>
**Client Industry:** BFSI (Banking, Financial Services, and Insurance)

---

## What Happened

An attacker compromised a workstation and extracted credentials via LSASS memory dumping. The stolen NTLM hash was used to authenticate across multiple internal servers. This enabled lateral movement and reconnaissance within the internal network.

---

## How It Was Detected

Microsoft Sentinel triggered a critical alert based on Defender for Identity telemetry detecting multiple NTLM authentications from a single device.

---

## Investigation Summary

**L1:** Identified abnormal NTLM authentication to multiple servers from one device and confirmed successful logons.

**L2:** Validated credential dumping via LSASS and confirmed Pass-the-Hash lateral movement using the compromised account.

**L3:** Improved detection by correlating LSASS access with NTLM activity for earlier identification.

---

## Attack Timeline

| Timestamp (IST) | Event                                          | Data Source                                | MITRE Technique                   |
| --------------- | ---------------------------------------------- | ------------------------------------------ | --------------------------------- |
| 09:40           | PowerShell execution with encoded command      | DeviceProcessEvents                        | T1059.001 — PowerShell            |
| 09:42           | LSASS memory dump via rundll32 and comsvcs.dll | DeviceProcessEvents                        | T1003.001 — OS Credential Dumping |
| 11:17           | NTLM authentication to FS-FILE-02              | IdentityLogonEvents                        | T1550.002 — Pass the Hash         |
| 11:19           | NTLM authentication to FS-APP-01               | IdentityLogonEvents                        | T1550.002 — Pass the Hash         |
| 11:21           | NTLM authentication to FS-DB-03                | IdentityLogonEvents                        | T1550.002 — Pass the Hash         |
| 11:24           | NTLM authentication to FS-REPORT-01            | IdentityLogonEvents                        | T1550.002 — Pass the Hash         |
| 11:26           | Sentinel alert triggered                       | Microsoft Sentinel / Defender for Identity | T1550.002 — Pass the Hash         |

---

## MITRE ATT&CK

* T1059.001 — Command and Scripting Interpreter: PowerShell
* T1003.001 — OS Credential Dumping: LSASS Memory
* T1550.002 — Use Alternate Authentication Material: Pass the Hash

---

## IOCs

| IOC                        | Type    | Source              | Enrichment Result                                 |
| -------------------------- | ------- | ------------------- | ------------------------------------------------- |
| FS-MUM-WS-447              | Host    | IdentityLogonEvents | Source of lateral movement and credential dumping |
| rahul.s                    | User    | IdentityLogonEvents | Compromised account used for NTLM authentication  |
| rundll32.exe + comsvcs.dll | Process | DeviceProcessEvents | Known LSASS dumping technique                     |

---

## Containment Actions

* Isolated compromised endpoint FS-MUM-WS-447
* Reset password and revoked sessions for rahul.s
* Invalidated NTLM sessions across domain
* Scanned affected servers for follow-on activity

---

## Key Takeaway

Credential dumping detection is critical, as relying only on lateral movement patterns delays response.

---

## Tools & Data Sources Used

Microsoft Sentinel, Defender for Identity, Defender for Endpoint, IdentityLogonEvents, DeviceProcessEvents
