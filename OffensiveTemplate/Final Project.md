Blue Team: Summary of Operations

Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

Network Topology

The following machines were identified on the network:
- Name of VM 1
  - Linux:
  - Vulnerable Machine to be targeted:
  - 192.168.1.110:
- Name of VM 2
  - Linux:
  - Target MAchine:
  - 192.168.1.115:
- Etc.

Description of Targets

The target of this attack was: Target 1 (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

-Excessive HTTP Errors
-HTTP Request Size Monitor
-CPU Usage Monitor

Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

Excessive HTTP Errors

Alert 1 is implemented as follows:
  - Metric: http.response.status_code IS ABOVE 400
  - :Threshold: 5 in the last 5 minutes
  - Vulnerability Mitigated: With alerts, the security team can quickly identify and blacklist suspicious IPs, reinforce password policies, and restrict or close port 22 from certain IPs
  - Reliability: This alert does't generate false positives and it is highly reliable in identifying Brute Force Attacks

HTTP Request Size Monitor

Alert 2 is implemented as follows:
  - Metric: http.request.bytes
  - Threshold: 3500 in last 1 minute
  - Vulnerability Mitigated: This protects against Distributed Denial of Service attacks DDoS
  - Reliability:. This alert does not create a lot of false positives, so it is reliable

CPU Usage Monitor

Alert 3 is implemented as follows:
  - Metric: system.process.cpu.total.pct
  - Threshold: 0.5 in last 5 minutes
  - Vulnerability Mitigated: CPU usage at 50% will trigger a memory dump of stored information when generated
  - Reliability: This alert can generate a lot of false positives as the CPU can spike even when there is no attack, just as it will spike when there is an attack.

_TODO Note: Explain at least 3 alerts. Add more if time allows._

Suggestions for Going Further (Optional)

- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
- Vulnerability 1
  - Patch: Institute a stronger password policy in the user account settings. Update the account password policy in Windows group policy through /etc/security/pwquality.conf & through /etc/security/pwquality.conf in Linux
  - Why It Works: A complexed password makes it impossible for Brute Force Attacks
- Vulnerability 2
  - Patch: With advanced Intrusion Prevention and threat management systems, combined with firewalls, VPN, anti-spam, content filtering, load balancing, and other layers of DDoS defense techniques. Together they enable constant and consistent network protection to prevent a DDoS attack from happening. This includes everything from identifying possible traffic inconsistencies with the highest level of precision in blocking the attack
  - Why It Works:  Given the complexity of DDoS attacks, there’s hardly a way to defend against them without appropriate systems to identify anomalies in traffic and provide instant response. Backed by secure infrastructure and a battle-plan, such systems can minimize the threat.
- Vulnerability 3
  - Patch: Use Host Instrusion Prevention System to identify DOS attack
  - Why It Works: This stops malware by monitoring code behaviors
