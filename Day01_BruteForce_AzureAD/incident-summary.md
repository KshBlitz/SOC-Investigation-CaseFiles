### Incident Summary

A brute force attack was detected against Azure AD involving multiple failed login attempts from external IP **185.243.115.23** within a short time window. The attacker targeted three privileged accounts, indicating a focused credential access attempt. Analysis of **SigninLogs** confirmed repeated authentication failures with no successful logins from the source IP or any correlated infrastructure.

No evidence of account compromise, MFA bypass, or post-authentication activity was observed. The activity aligns with password spray/brute force behavior rather than targeted credential theft. The attack was successfully contained at the authentication stage.

Key findings confirm multi-account targeting from a single IP, absence of successful authentication, and no lateral or follow-on activity.

**Recommended Actions:**

* Block the source IP in Conditional Access and monitor for recurrence
* Review and enforce strong password policies for privileged accounts
* Tune detection rules to include multi-account targeting behavior
