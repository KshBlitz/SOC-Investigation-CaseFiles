Here is the standardized README generated from your document :

---

# Day 2 — Phishing Email Leading to Credential Theft

**Incident ID:** INC-20260413-002<br>
**Date:** 13 April 2026<br>
**Severity:** Critical<br>
**Type:** Phishing → Credential Theft → Account Takeover<br>
**Client Industry:** Healthcare

---

## What Happened

An attacker sent a phishing email with a malicious Excel macro to a hospital employee, tricking the user into entering credentials on a fake login page. The attacker used those credentials to access the user’s Microsoft 365 account and establish persistence via an inbox forwarding rule.

---

## How It Was Detected

The incident was detected in Microsoft Sentinel through a correlation rule combining Defender for Office 365 malware detection with a suspicious Azure AD login from a foreign IP.

---

## Investigation Summary

**L1:** Priya validated the phishing email in Defender for Office 365, confirmed malicious macro behavior, and identified a suspicious login from Romania with MFA marked as satisfied.

**L2:** Rohan confirmed credential compromise, identified inbox forwarding rule creation and mailbox access activity, and correlated all events into a full attack timeline.

**L3:** Nisha improved detection by adding pre-compromise logic correlating malicious attachments with PowerShell execution instead of waiting for a successful login.

---

## Attack Timeline

| Timestamp (IST) | Event                                          | Data Source         | MITRE Technique |
| --------------- | ---------------------------------------------- | ------------------- | --------------- |
| 21:52           | Phishing email delivered with macro attachment | EmailEvents         | T1566.001       |
| 21:54           | User opens attachment, macro executes          | EmailAttachmentInfo | T1059.001       |
| 22:14           | Successful login from Romania IP               | SigninLogs          | T1078           |
| 22:16           | Inbox forwarding rule created                  | OfficeActivity      | T1114.003       |
| 22:17           | Mailbox data accessed                          | OfficeActivity      | T1114           |

---

## MITRE ATT&CK

* T1566.001 — Spearphishing Attachment
* T1059.001 — PowerShell Execution
* T1078 — Valid Accounts
* T1114.003 — Email Forwarding Rule
* T1114 — Email Collection

---

## IOCs

| IOC                                                                             | Type      | Source              | Enrichment Result              |
| ------------------------------------------------------------------------------- | --------- | ------------------- | ------------------------------ |
| 185.193.88.47                                                                   | IP        | SigninLogs          | AbuseIPDB score 92 (malicious) |
| medicore-support.co                                                             | Domain    | EmailEvents         | WHOIS: 6 days old              |
| 8f3c9e5c2d4a...                                                                 | File Hash | EmailAttachmentInfo | VirusTotal: 38 detections      |
| [anita.sharma.secure@protonmail.com](mailto:anita.sharma.secure@protonmail.com) | Email     | OfficeActivity      | External exfiltration address  |

---

## Containment Actions

* Disable compromised user account and revoke sessions
* Reset credentials and enforce MFA re-registration
* Remove malicious inbox forwarding rule
* Block attacker IP via Conditional Access
* Add malicious domain to tenant block list
* Perform endpoint scan via Defender for Endpoint
* Review mailbox access logs for exposure
* Notify compliance team for potential data risk

---

## Key Takeaway

Detection after login is too late — early correlation of malicious attachment execution can prevent account takeover.

---

## Tools & Data Sources Used

Microsoft Sentinel, Microsoft Defender for Office 365, SigninLogs, EmailEvents, EmailAttachmentInfo, OfficeActivity, DeviceProcessEvents, VirusTotal, AbuseIPDB, WHOIS

---
