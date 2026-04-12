### Investigation Thought Process

1. **Initial hypothesis:**
   The alert pattern (multiple failed logons from a single external IP targeting privileged accounts) strongly suggested a **password spraying / brute force attempt** rather than normal user error. The inclusion of **privileged roles (Global Admin / Privileged Role Admin)** elevated the risk — attackers typically prioritize these accounts for maximum impact.

2. **First validation step:**
   The immediate question was: *“Did any of these attempts succeed?”*
   This was checked first in **Microsoft Sentinel SigninLogs** because:

* A brute force attempt without success is reconnaissance
* A single success converts it into a confirmed compromise

So the first validation focused on:

* Successful logins (`ResultType == 0`)
* Same source IP
* Same targeted accounts
* Time proximity to failed attempts

3. **Key observation:**
   The investigation showed:

* High volume of failed attempts within a short window
* **No successful authentication events** from the attacking IP
* No MFA approvals or anomalous session creation
* No follow-on activity (no token issuance, no resource access)

This ruled out immediate account compromise. Additionally:

* Accounts showed **no deviation in baseline behavior post-attempt**
* No sign of attacker pivoting to other access vectors (e.g., legacy auth, non-interactive sign-ins)

4. **Pivot decision:**
   Since no success was observed, the investigation pivoted from *compromise validation* to *intent assessment*.
   Key questions became:

* Is this targeted or random spraying?
* Are privileged accounts specifically being enumerated?
* Is this part of a broader reconnaissance phase?

Correlation confirmed:

* Same IP targeting **only high-value privileged accounts**
* Tight timing window → automated tooling
* No spread across normal user accounts → not random

This indicated **intentional targeting rather than generic noise**

5. **Final conclusion:**
   This activity was confirmed as a **targeted brute force reconnaissance attempt (MITRE T1110)** with clear attacker intent to identify valid credentials for privileged accounts.

However:

* No successful authentication
* No MFA bypass
* No post-authentication activity

Therefore:

* **No compromise occurred**
* **Threat classified as True Positive (attempted attack, blocked at authentication layer)**

The incident demonstrated **early-stage adversary reconnaissance against critical identities**, reinforcing the need for monitoring privileged account targeting patterns rather than relying solely on successful login detection. 
