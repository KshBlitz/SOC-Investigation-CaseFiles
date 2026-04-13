Incident Summary

A phishing attack targeted a MediCore Hospital employee through a malicious Excel attachment containing a macro that executed PowerShell and redirected the user to a credential harvesting page. The attacker successfully captured valid credentials and performed a login from a foreign IP (Romania), resulting in confirmed account compromise.

Post-authentication activity revealed mailbox access and creation of an inbox forwarding rule to an external email address, indicating attempted data exfiltration and persistence. No evidence of large-scale data exfiltration or lateral movement was observed.

The incident was contained by disabling the compromised account, revoking sessions, removing malicious rules, and blocking attacker infrastructure.

Recommended Actions:

Enforce stricter Conditional Access policies for high-risk geolocations
Deploy pre-auth detection for malicious attachment execution
Conduct targeted phishing awareness training for users