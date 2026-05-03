### Incident Summary

A Business Email Compromise (BEC) attempt was identified targeting the finance department via a spoofed email impersonating the CEO. The attacker used a lookalike domain to send urgent wire transfer requests to multiple finance users during peak transaction hours.

Investigation confirmed the email was externally originated with failed SPF, DKIM, and DMARC checks, and was delivered despite policy gaps. No evidence of CEO account compromise, mailbox rule creation, or suspicious authentication activity was found. Only one user accessed the email, and no financial transaction was executed.

The incident was contained at the pre-impact stage. Malicious infrastructure was identified and blocked, and all targeted users were notified. Findings confirm this was a coordinated impersonation campaign without internal compromise .

**Recommended Actions:**

* Block and monitor lookalike domains and sender infrastructure
* Enforce strict DMARC reject policy and email filtering controls
* Implement enhanced impersonation detection with multi-recipient correlation
