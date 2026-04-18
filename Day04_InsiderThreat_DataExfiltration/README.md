# Day 4 — Insider Threat Data Exfiltration

**Incident ID:** INC-20260416-004<br>
**Date:** 16 April 2026<br>
**Severity:** High<br>
**Type:** Insider Threat — Data Exfiltration<br>
**Client Industry:** Legal

---

## What Happened

A departing employee used valid credentials to access SharePoint Online and download a large volume of sensitive legal documents. The activity targeted confidential client data including M&A and litigation files. The data was downloaded to an unmanaged device outside business hours.

---

## How It Was Detected

The incident was triggered by a Microsoft Sentinel analytics rule detecting high-volume SharePoint downloads based on Purview DLP signals.

---

## Investigation Summary

**L1:** Identified abnormal after-hours activity with 487 file downloads (2.31GB) and confirmed no prior similar behavior.

**L2:** Validated legitimate login, ruled out external compromise, confirmed targeted access to sensitive data, and identified unmanaged device usage with no external sharing detected.

**L3:** Improved detection rule by adding contextual signals (after-hours activity and user risk) to enable earlier detection.

---

## Attack Timeline

| Timestamp (IST) | Event                               | Data Source               | MITRE Technique                            |
| --------------- | ----------------------------------- | ------------------------- | ------------------------------------------ |
| 23:17           | User authenticated to SharePoint    | SigninLogs                | T1078 — Valid Accounts                     |
| 23:18–23:45     | Bulk download of 487 files (2.31GB) | OfficeActivity            | T1213 — Data from Information Repositories |
| 23:45           | Download activity stopped           | OfficeActivity            | T1213 — Data from Information Repositories |
| 23:46           | Sentinel DLP alert triggered        | OfficeActivity / Sentinel | T1213 — Data from Information Repositories |
| 23:55           | Incident escalated to L2            | Sentinel                  | —                                          |
| 00:25           | Insider threat confirmed            | Analyst Investigation     | T1078 — Valid Accounts                     |

---

## MITRE ATT&CK

* T1213 — Data from Information Repositories
* T1078 — Valid Accounts

---

## IOCs

| IOC                                                         | Type         | Source         | Enrichment Result                                                                      |
| ----------------------------------------------------------- | ------------ | -------------- | -------------------------------------------------------------------------------------- |
| [rahul.verma@legaledge.in](mailto:rahul.verma@legaledge.in) | User Account | OfficeActivity | Internal employee with resignation status performing abnormal data access              |
| Unmanaged Browser Session                                   | Device       | SigninLogs     | Non-compliant device with no endpoint visibility, enabling potential data exfiltration |

---

## Containment Actions

* Disabled user account and revoked all active sessions
* Invalidated SharePoint access tokens
* Initiated Purview eDiscovery and audit
* Notified HR and Legal teams
* Began enforcement of Conditional Access for managed devices
* Reviewed and strengthened DLP policies

---

## Key Takeaway

High-volume thresholds alone are insufficient—insider threats require context-aware detection using behavior and user risk signals.

---

## Tools & Data Sources Used

Microsoft Sentinel, OfficeActivity, SigninLogs, Microsoft Purview, Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender for Identity
