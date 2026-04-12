# Day 1 — Brute Force Attack on Azure AD

**Incident ID:** INC-20260101-001<br>
**Date:** 2026-01-01<br>
**Severity:** High<br>
**Type:** Credential Access — Brute Force<br>
**Client Industry:** BFSI (FinSecure Bank)

---

## What Happened

An external attacker attempted a brute force attack against Azure AD by targeting multiple privileged accounts within a short time window. The activity involved repeated failed login attempts from a single IP address, indicating credential guessing against high-value identities.

---

## How It Was Detected

Microsoft Sentinel triggered an alert based on the rule **“Multiple Failed Logon Attempts — Threshold Breached”**, identifying repeated authentication failures across privileged accounts within a 5-minute window.

---

## Investigation Summary

**L1:** Reviewed alert details in Sentinel, confirmed multiple failed login attempts against privileged accounts, and checked for any successful authentications.

**L2:** Analyzed sign-in logs, confirmed no successful compromise but identified consistent attack pattern from a single external IP targeting high-privilege roles.

**L3:** Improved detection rule by lowering threshold and adding filters for privileged account targeting.

---

## Attack Timeline

| Timestamp (IST) | Event                                                                | Data Source             | MITRE Technique |
| --------------- | -------------------------------------------------------------------- | ----------------------- | --------------- |
| 08:40           | Multiple failed login attempts detected across 3 privileged accounts | SigninLogs              | T1110           |
| 08:41           | Alert triggered in Microsoft Sentinel                                | Sentinel Analytics Rule | T1110           |
| 08:45           | L1 triage initiated and escalation sent                              | Sentinel Incident       | T1110           |
| 08:52           | L2 investigation confirmed brute force pattern                       | SigninLogs              | T1110           |

---

## MITRE ATT&CK

* T1110 — Brute Force

---

## IOCs

| IOC                     | Type          | Source     | Enrichment Result                  |
| ----------------------- | ------------- | ---------- | ---------------------------------- |
| External IP (attacker)  | IP Address    | SigninLogs | Flagged as suspicious in AbuseIPDB |
| Targeted Admin Accounts | User Accounts | SigninLogs | Privileged roles confirmed         |

---

## Containment Actions

* Blocked attacker IP via Conditional Access policy
* Enforced account lockout for targeted accounts
* Reviewed MFA enforcement on privileged accounts

---

## Key Takeaway

Brute force attempts targeting privileged accounts require tighter detection thresholds and prioritized monitoring.

---

## Tools & Data Sources Used

Microsoft Sentinel, Azure AD SigninLogs, AbuseIPDB
