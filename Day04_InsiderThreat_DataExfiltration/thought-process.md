### Investigation Thought Process

1. **Initial hypothesis:**
   High-volume SharePoint downloads could indicate either legitimate late-night work or potential insider data exfiltration using valid credentials.

2. **First validation step:**
   Checked authentication logs (SigninLogs) to confirm whether access was legitimate. The login appeared normal (no anomalous location, valid session), suggesting no external account compromise.

3. **Key observation:**
   User performed 487 downloads (2.31GB) in ~28 minutes, all targeting “Confidential — Client Privileged” data, with no prior history of similar behavior and occurring after business hours.

4. **Pivot decision:**
   Investigated for external sharing/upload activity in OfficeActivity to confirm exfiltration path. No activity found, leading to pivot toward endpoint visibility and device context.

5. **Final conclusion:**
   No signs of account compromise; activity used legitimate access. Targeted data selection, timing (post-resignation, after-hours), and volume confirmed intentional insider data staging for exfiltration via unmanaged device. 
