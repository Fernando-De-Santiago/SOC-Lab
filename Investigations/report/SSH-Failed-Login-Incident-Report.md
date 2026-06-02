___
## Incident information
- Incident ID: IR01
- Title Failed SSH Authentication Analysis
- Analyst Fernando De Santiago
- Report date: 06/01/2026
- Investigation Period: 05/26/2026 - 06/01/2026
- Severity: Low (Homelab simulation)
- Status: Closed
___
## Executive summary 
This report documents multiple failed SSH login attempts on the Ubuntu server (192.168.56.101) in a controlled lab environment. Authentication logs and system logs were analyzed to identify source IP Addresses, patterns of activity consistent with potential brute-force behavior. All activity was intentionally generated for educational and testing purposes.
___
## Environment

| System          | Ip Address     | Role               |
| --------------- | -------------- | ------------------ |
| Kali linux      | 192.168.56.102 | Attacker           |
| Ubuntu Server   | 192.168.56.101 | Target System      |
| windows machine | 192.168.56.103 | Secondary attacker |
___
## Investigation Timeline

| Date/Time  | Event                                                                   |
| ---------- | ----------------------------------------------------------------------- |
| 05/26/2026 | 2 Failed SSH login attempts for user admin by 192.168.56.102            |
| 05/27/2026 | 3 Failed SSH login attempts for user admin by  192.168.56.1             |
| 05/29/2026 | 5 failed SSH login attempts for user kali  and root from 192.168.56.102 |
| 06/02/2026 | 6 failed SSH login attempts for user admin and suer from 192.168.56.103 |
___
## Evidence Collected
Evidence Source: /var/log/auth.log
Filter used: grep -a "Failed password"
Environment: Ubuntu Server (192.168.56.101)
Data Type: Authentication logs (SSH - /var/log/auth.log)
Logs:
```
2026-05-26T20:06:24.758280+00:00 ubuntuserver sshd-session[12038]: Failed password for admin from 192.168.56.102 port 33926 ssh2
2026-05-26T20:06:29.942973+00:00 ubuntuserver sshd-session[12038]: Failed password for admin from 192.168.56.102 port 33926 ssh2
2026-05-27T22:50:18.336344+00:00 ubuntuserver sshd-session[1789]: Failed password for admin from 192.168.56.1 port 45790 ssh2
2026-05-27T22:50:22.179866+00:00 ubuntuserver sshd-session[1789]: Failed password for admin from 192.168.56.1 port 45790 ssh2
2026-05-27T22:50:26.478492+00:00 ubuntuserver sshd-session[1789]: Failed password for admin from 192.168.56.1 port 45790 ssh2
2026-05-29T00:17:42.466174+00:00 ubuntuserver sshd-session[1711]: Failed password for invalid user kali from 192.168.56.102 port 46390 ssh2
2026-05-29T00:17:45.940510+00:00 ubuntuserver sshd-session[1711]: Failed password for invalid user kali from 192.168.56.102 port 46390 ssh2
2026-05-29T00:17:55.738684+00:00 ubuntuserver sshd-session[1711]: Failed password for invalid user kali from 192.168.56.102 port 46390 ssh2
2026-05-29T00:18:21.533450+00:00 ubuntuserver sshd-session[1713]: Failed password for root from 192.168.56.102 port 36546 ssh2
2026-05-29T00:18:31.387737+00:00 ubuntuserver sshd-session[1713]: Failed password for root from 192.168.56.102 port 36546 ssh2
2026-05-29T00:18:34.361565+00:00 ubuntuserver sshd-session[1713]: Failed password for root from 192.168.56.102 port 36546 ssh2
2026-06-02T00:41:08.850463+00:00 ubuntuserver sshd-session[1871]: Failed password for invalid user suer from 192.168.56.103 port 50109 ssh2
2026-06-02T00:41:12.104372+00:00 ubuntuserver sshd-session[1871]: Failed password for invalid user suer from 192.168.56.103 port 50109 ssh2
2026-06-02T00:41:15.177485+00:00 ubuntuserver sshd-session[1871]: Failed password for invalid user suer from 192.168.56.103 port 50109 ssh2
2026-06-02T00:41:24.450307+00:00 ubuntuserver sshd-session[1873]: Failed password for admin from 192.168.56.103 port 50110 ssh2
2026-06-02T00:41:28.428427+00:00 ubuntuserver sshd-session[1873]: Failed password for admin from 192.168.56.103 port 50110 ssh2
2026-06-02T00:41:32.322146+00:00 ubuntuserver sshd-session[1873]: Failed password for admin from 192.168.56.103 port 50110 ssh2
```
___
### Commands Used
```bash
grep -a "Failed password" /var/log/auth.log > Failed_password_log.txt
```
___
## Analysis
- Multiple failed SSH Authentication attempts were observed.
-  Attempts were made from Kali Linux VM (192.168.56.102) and Windows VM (192.168.56.103).
- Common attack pattern was using different usernames and passwords for the login attempts.

___
## Findings
- Repeated authentication attempts were observed over multiple days
- Common usernames included “admin” and “root”
- Activity aligns with brute-force login behavior in a controlled environment
- No successful authentication or compromise was observed
- Source IPs remained consistent across events, suggesting repeated attempts from the same hosts
___
## Impact
- No evidence of system compromise was identified
- All observed activity was limited to failed authentication attempts
- Activity remained limited to failed login attempts
___
## Recommendation
- Implement rate-limiting for SSH authentication attempts (e.g., Fail2Ban).
- Restrict SSH access to trusted IP ranges where possible.
- Enable logging alerts for repeated authentication failures.
- Monitor authentication logs for brute-force patterns.
___
## Conclusion
The observed behavior is that of a controlled SSH brute-force attack. Two source IP addresses were observed generating repeated failed SSH authentication attempts against the target system. Log analysis confirms repeated failed authentication attempts with no system compromise.
