## 1. A server is down. How will you troubleshoot it?
First, I would confirm whether the server is actually down by trying to ping it or SSH into it. If I cannot connect, I would check whether the issue is network-related or server-related.</br>
I would log in and check the server status.</br>
**Then I would verify basic things such as:**</br>
- Server uptime and whether it rebooted unexpectedly.
- CPU, memory, and disk utilization using commands like top, free -h, and df -h.
- Network connectivity using ip a, ip route, and ping.
- Running services using systemctl status.
- System logs in /var/log/messages, /var/log/syslog, or journalctl to identify errors.

## 2. If a Disk is full , How will you troubleshoot ?
If the Disk is Full, first I will check which disk is full or nearby full by using the command df -hT.
- Then I will navigate to that mount point.
- Then I will check for the big files and using the command du -sh * | sort -nr
- If the files are related to Application then I will request the Application team for cleanup and remove unwanted files.
- And if the files are related to server we do the cleanup , we remove the unwanted files after tacking approval.
- If the cleanup is not sufficient then we will have to increase the disk size for that we need change request with all the details.