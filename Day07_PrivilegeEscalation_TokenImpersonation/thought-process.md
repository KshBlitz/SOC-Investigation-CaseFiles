### Investigation Thought Process

1. **Initial hypothesis:**
   Alert indicated abnormal LSASS access from a non-standard parent process, suggesting possible credential access or token impersonation rather than benign system activity.

2. **First validation step:**
   Checked SecurityEvent logs for privileged logon events (Event ID 4672) to confirm whether the standard user account gained elevated privileges after the alert.

3. **Key observation:**
   Privileges such as SeDebugPrivilege and SeImpersonatePrivilege were assigned shortly after LSASS access, confirming successful privilege escalation. 

4. **Pivot decision:**
   Shifted focus to process execution history on the host to reconstruct the chain, identifying abnormal svchost behavior and tracing back to an unsigned executable launched from the temp directory.

5. **Final conclusion:**
   The activity was a confirmed token impersonation attack: initial execution → LSASS access → token duplication → privilege escalation, with no evidence of lateral movement or persistence, indicating early-stage compromise successfully contained.
