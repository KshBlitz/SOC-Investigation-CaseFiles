### Incident Summary

A command-and-control (C2) beaconing activity was detected originating from a developer endpoint within the TechNova environment. The compromised device (DEV-LAPTOP-023) communicated with an external malicious IP over HTTPS at consistent intervals, indicating automated beaconing behavior. The target was a developer workstation with elevated outbound access, increasing exposure risk.

Investigation confirmed the use of obfuscated PowerShell to establish persistent communication and execute commands. No evidence of lateral movement or data exfiltration was identified. The compromise was contained to a single endpoint.

Immediate containment actions were executed, including endpoint isolation, IP blocking, process termination, and credential reset .

**Recommended Actions:**

* Deploy enhanced beaconing detection rules for early-stage activity
* Conduct environment-wide threat hunt for similar patterns
* Strengthen outbound monitoring controls on developer endpoints
