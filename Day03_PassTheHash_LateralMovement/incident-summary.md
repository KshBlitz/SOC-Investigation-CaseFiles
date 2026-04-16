### Incident Summary

A Pass-the-Hash attack was detected involving a compromised workstation (FS-MUM-WS-447) and user account (rahul.s), where NTLM authentication was used to access multiple internal servers within a short time window. The attacker leveraged credentials obtained via LSASS memory dumping using `rundll32.exe` and `comsvcs.dll`, enabling lateral movement across four servers.

The targeted assets included internal file, application, database, and reporting servers. Investigation confirmed successful authentication attempts, indicating credential compromise, though no evidence of privilege escalation or data exfiltration was observed.

Key findings include PowerShell-based execution preceding credential dumping and controlled, sequential NTLM authentications. The attack was contained by isolating the affected endpoint and securing the compromised account. 

**Recommended Actions:**

* Disable or restrict NTLM authentication where not required
* Enhance detection for LSASS access and PowerShell abuse
* Conduct credential hygiene and enforce least privilege access
