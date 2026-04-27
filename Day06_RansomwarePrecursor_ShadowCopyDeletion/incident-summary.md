### Incident Summary

A ransomware precursor attack was identified on endpoint MT-ENG-WS-047 involving execution of destructive system recovery commands (vssadmin, wbadmin, bcdedit) following initial access via a malicious document and PowerShell payload. The activity targeted system recovery mechanisms to prevent restoration prior to encryption. Investigation confirmed the device and user account (j.patil) were compromised, with outbound communication to a known malicious IP. No file encryption, lateral movement, or data exfiltration was observed. Key findings indicate a staged ransomware deployment halted before impact. The incident was contained through rapid detection and escalation. 

**Recommended Actions:**

* Enforce macro execution restrictions and user awareness training
* Deploy behavioral correlation detection rules for ransomware precursors
* Conduct environment-wide threat hunting for similar PowerShell activity
