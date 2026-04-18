| IOC                                                         | Type         | Source                      | Enrichment Insight                                                                                                                                              | Confidence |
| ----------------------------------------------------------- | ------------ | --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| [rahul.verma@legaledge.in](mailto:rahul.verma@legaledge.in) | User Account | OfficeActivity / SigninLogs | Departing employee (resigned 3 days prior) performing abnormal high-volume sensitive data access outside business hours — strong insider threat indicator       | High       |
| Unmanaged Browser Session                                   | Device       | SigninLogs                  | Activity executed from unmanaged/non-compliant device with no endpoint telemetry, creating a visibility gap and enabling potential undetected data exfiltration | High       |

**Note:**
No external IPs, attacker-controlled domains, or file hashes were identified in the investigation, indicating this is a **pure insider threat scenario leveraging legitimate access** rather than external compromise. 
