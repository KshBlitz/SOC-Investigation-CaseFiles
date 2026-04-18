### Incident Summary

A departing employee account (rahul.verma) conducted abnormal high-volume downloads from SharePoint Online outside business hours. The activity targeted sensitive legal data, including “Confidential — Client Privileged” documents related to ongoing litigation and M&A cases. Approximately 487 files (2.31GB) were downloaded within 28 minutes using a valid account and an unmanaged device.

No evidence of external sharing or uploads was observed within monitored Microsoft 365 services. However, due to the use of an unmanaged endpoint, potential data exfiltration outside visibility cannot be ruled out.

Key findings confirm this as an insider threat scenario leveraging legitimate access shortly after resignation submission. The behavior was anomalous compared to the user’s baseline.

**Recommended Actions:**

* Disable user account and revoke all active sessions immediately
* Enforce Conditional Access to block unmanaged device access
* Implement DLP controls to restrict downloads of sensitive data 
