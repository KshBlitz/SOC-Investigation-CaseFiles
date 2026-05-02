# Day 9 — Business Email Compromise — CEO Fraud

**Incident ID:** INC-20260430-009<br>
**Date:** 30-Apr-2026<br>
**Severity:** Critical<br>
**Type:** Business Email Compromise (BEC) — CEO Impersonation<br>
**Client Industry:** Finance (International Trade & Export)

---

## What Happened

An attacker impersonated the CEO using a lookalike domain to send urgent wire transfer requests to finance employees. The goal was to exploit trust and urgency during end-of-quarter financial operations to trigger unauthorized payments.

---

## How It Was Detected

The incident was reported by a finance user who found the email suspicious. Microsoft Sentinel simultaneously triggered an alert based on a Defender for Office 365 impersonation detection rule.

---

## Investigation Summary

**L1:** Verified email headers in Defender for Office 365, confirmed SPF/DKIM/DMARC failures, identified lookalike domain, and validated no user action was taken

**L2:** Confirmed multi-recipient targeting, ruled out CEO account compromise via SigninLogs, enriched malicious domain and IP, and validated no mailbox or account abuse occurred

**L3:** Improved detection rule by adding multi-recipient correlation logic to identify coordinated BEC campaigns earlier

---

## Attack Timeline

| Timestamp (IST) | Event                                  | Data Source        | MITRE Technique                |
| --------------- | -------------------------------------- | ------------------ | ------------------------------ |
| 10:38           | Phishing email sent to 3 finance users | EmailEvents        | T1534 — Internal Spearphishing |
| 10:41           | Finance manager opens email            | OfficeActivity     | T1204 — User Execution         |
| 10:42           | Sentinel alert triggered               | Sentinel Analytics | Detection                      |
| 10:43           | User calls SOC                         | External trigger   | —                              |
| 10:45           | L1 escalation to L2                    | Teams              | —                              |
| 10:47           | L2 confirms multi-recipient targeting  | EmailEvents        | —                              |
| 10:49           | L2 verifies no mailbox compromise      | SigninLogs         | —                              |

---

## MITRE ATT&CK

* T1534 — Internal Spearphishing
* T1204 — User Execution

---

## IOCs

| IOC                                                             | Type          | Source       | Enrichment Result                                   |
| --------------------------------------------------------------- | ------------- | ------------ | --------------------------------------------------- |
| gl0baltrade.co                                                  | Domain        | EmailEvents  | Malicious — newly registered, flagged in VirusTotal |
| [rajiv.mehra@gl0baltrade.co](mailto:rajiv.mehra@gl0baltrade.co) | Email Address | EmailEvents  | Spoofed identity                                    |
| 185.243.115.72                                                  | IP Address    | Email header | AbuseIPDB: High-risk (87% confidence)               |

---

## Containment Actions

* Blocked domain gl0baltrade.co in Microsoft Defender for Office 365
* Removed all instances of the email from affected mailboxes
* Blocked sending IP 185.243.115.72 in Exchange Online Protection
* Notified all targeted users and confirmed no action taken
* Reviewed and validated CEO account activity — no compromise detected

---

## Key Takeaway

Human reporting combined with improved detection logic is critical to stopping BEC attacks before financial impact occurs.

---

## Tools & Data Sources Used

Microsoft Sentinel, Microsoft Defender for Office 365, SigninLogs, EmailEvents, OfficeActivity, Microsoft Teams, VirusTotal, AbuseIPDB, WHOIS
