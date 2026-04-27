| Timestamp (IST) | Event                                                       | Data Source         | MITRE Technique                 | Meaning                                                                 |
| --------------- | ----------------------------------------------------------- | ------------------- | ------------------------------- | ----------------------------------------------------------------------- |
| 21:12           | WINWORD.EXE opened a document                               | DeviceProcessEvents | T1204 — User Execution          | Initial access likely via malicious document (user-triggered execution) |
| 21:14           | PowerShell executed encoded command                         | DeviceProcessEvents | T1059.001 — PowerShell          | Execution of obfuscated payload indicating malware delivery             |
| 21:15           | Outbound connection to external IP (185.224.128.77)         | DeviceNetworkEvents | T1105 — Ingress Tool Transfer   | Payload retrieval or C2 communication established                       |
| 21:52           | net.exe view /domain executed                               | DeviceProcessEvents | T1087 — Account Discovery       | Attacker performing internal reconnaissance to map environment          |
| 21:58           | vssadmin delete shadows /all /quiet executed                | DeviceProcessEvents | T1490 — Inhibit System Recovery | Shadow copies deleted to prevent system/file recovery                   |
| 22:05           | wbadmin delete catalog -quiet executed                      | DeviceProcessEvents | T1490 — Inhibit System Recovery | Backup catalog removed to disable backup restoration capability         |
| 22:08           | bcdedit /set {default} recoveryenabled No executed          | DeviceProcessEvents | T1490 — Inhibit System Recovery | System recovery options disabled at boot level                          |
| 22:14           | Multiple alerts correlated into single incident in Sentinel | Microsoft Sentinel  | N/A                             | Detection of coordinated ransomware precursor activity on single host   |

