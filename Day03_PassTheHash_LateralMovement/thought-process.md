### Investigation Thought Process

1. **Initial hypothesis:**
   The alert suggested potential Pass-the-Hash activity, indicating that a compromised credential was being reused for lateral movement via NTLM.

2. **First validation step:**
   I verified authentication logs to confirm whether a single account (rahul.s) was authenticating to multiple hosts from one source device within a short time window.

3. **Key observation:**
   Multiple successful NTLM authentications were observed from a single workstation to different servers in a controlled, sequential pattern—no failures or noise, ruling out brute force or normal user behavior.

4. **Pivot decision:**
   I pivoted to endpoint telemetry on the source device to identify how credentials were obtained, specifically checking for LSASS access or credential dumping activity.

5. **Final conclusion:**
   Credential dumping via `rundll32.exe` and `comsvcs.dll` confirmed compromise, and subsequent NTLM authentications validated Pass-the-Hash lateral movement, indicating clear attacker intent and staged execution. 
