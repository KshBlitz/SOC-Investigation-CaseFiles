| IOC                                           | Type       | Source              | Enrichment Insight                                                                       | Confidence |
| --------------------------------------------- | ---------- | ------------------- | ---------------------------------------------------------------------------------------- | ---------- |
| 52.184.217.91                                 | IP Address | DeviceNetworkEvents | AbuseIPDB reports 92% malicious confidence; associated with botnet/C2 infrastructure     | High       |
| powershell.exe (obfuscated command execution) | Process    | DeviceProcessEvents | Encoded/obfuscated PowerShell used for hidden execution and C2 communication loop        | High       |
| SHA256 (PowerShell process instance)          | File Hash  | DeviceProcessEvents | Flagged by 18 security vendors on VirusTotal, indicating known malicious behavior        | High       |
| DEV-LAPTOP-023                                | Device     | DeviceNetworkEvents | Single endpoint showing sustained beaconing behavior over 4 hours, confirmed compromised | High       |
