Investigation Thought Process
Initial hypothesis:
A phishing-based credential compromise was suspected due to the combination of a malicious attachment alert and a successful login from an unusual geographic location shortly after user interaction.
First validation step:
Authentication logs were reviewed first to confirm whether the login was anomalous. This helps distinguish between legitimate user behavior (e.g., travel) and unauthorized access.
Key observation:
The login originated from Romania with no prior history, used an unknown device, and had no preceding failed attempts, while MFA was marked as satisfied — indicating likely credential capture or session/token replay rather than brute force.
Pivot decision:
The investigation pivoted to post-login activity to determine attacker intent, followed by validation of the phishing vector through email and attachment logs to confirm the initial access path.
Final conclusion:
The sequence of phishing email → macro execution → credential capture → foreign login → inbox rule creation confirmed a successful account takeover with persistence established for potential data exfiltration.