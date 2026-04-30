### Investigation Thought Process

1. **Initial hypothesis:**
   The alert suggested possible command-and-control (C2) beaconing due to repeated outbound HTTPS connections to a single external IP, indicating potential automated communication from a compromised host.

2. **First validation step:**
   I first examined raw network logs (DeviceNetworkEvents) to verify whether the traffic pattern was truly periodic rather than normal developer API activity, since developer endpoints can generate high outbound traffic .

3. **Key observation:**
   The connections occurred at highly consistent ~60-second intervals with minimal variance, which is not typical for human-driven or application-driven traffic, confirming likely beaconing behavior.

4. **Pivot decision:**
   I pivoted to process-level telemetry (DeviceProcessEvents) to identify the source process, focusing on whether a legitimate application or a scripting engine was responsible for the traffic.

5. **Final conclusion:**
   The activity was confirmed as malicious C2 communication driven by obfuscated PowerShell execution, with evidence of command retrieval (payload spike at 18:42 IST), indicating active attacker control despite no lateral movement or data exfiltration observed .
