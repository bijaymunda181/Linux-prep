## 1. A server is down. How will you troubleshoot it?
First, I would confirm whether the server is actually down by trying to ping it or SSH into it. If I cannot connect, I would check whether the issue is network-related or server-related.</br>
I would log in and check the server status.</br>
**Then I would verify basic things such as:**</br>
- Server uptime and whether it rebooted unexpectedly.
- CPU, memory, and disk utilization using commands like top, free -h, and df -h.
- Network connectivity using ip a, ip route, and ping.
- Running services using systemctl status.
- System logs in /var/log/messages, /var/log/syslog, or journalctl to identify errors.