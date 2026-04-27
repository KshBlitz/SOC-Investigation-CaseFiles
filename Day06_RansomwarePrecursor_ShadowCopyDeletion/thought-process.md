### Investigation Thought Process

1. **Initial hypothesis:**
   Multiple recovery-disabling commands on a single host suggested potential ransomware staging rather than isolated admin activity.

2. **First validation step:**
   Checked file activity on the affected endpoint to determine if encryption or mass file modification had already started, as this would confirm active ransomware execution.

3. **Key observation:**
   No abnormal spike in file creation, renaming, or modification was observed, indicating the attack had not progressed to encryption phase.

4. **Pivot decision:**
   Shifted focus to process lineage and network activity to trace initial access, revealing a PowerShell encoded command triggered by a Word document and outbound connection to a known malicious IP.

5. **Final conclusion:**
   Confirmed a compromised endpoint and user account with clear ransomware precursor behavior; attacker intent was validated through systematic disabling of recovery mechanisms, but impact was prevented as execution was halted before encryption. 
