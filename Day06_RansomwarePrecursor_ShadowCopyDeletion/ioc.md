| IOC                        | Type         | Source                         | Enrichment Insight                                                                  | Confidence |
| -------------------------- | ------------ | ------------------------------ | ----------------------------------------------------------------------------------- | ---------- |
| 185.224.128.77             | IP Address   | DeviceNetworkEvents            | AbuseIPDB flagged 92% malicious; associated with malware hosting and C2 activity    | High       |
| Encoded PowerShell Command | Command      | DeviceProcessEvents            | Obfuscated download cradle used to fetch malicious payload from external source     | High       |
| MT-ENG-WS-047              | Device       | Endpoint / DeviceProcessEvents | Confirmed compromised host used for ransomware staging activity                     | High       |
| j.patil                    | User Account | Identity / DeviceProcessEvents | Legitimate user account exhibiting anomalous behavior; likely credential compromise | High       |
