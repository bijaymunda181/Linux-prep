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

## 3. How will you resolve high CPU utilization ?
**If CPU utilization is high, I will follow these troubleshooting steps:**

1. First, I will verify the CPU utilization using commands such as:

   ```bash
   top
   htop
   vmstat 1
   sar -u 1 5
   ```

2. I will identify the process consuming the most CPU using:

   ```bash
   top
   ps -eo pid,ppid,cmd,%cpu --sort=-%cpu | head
   ```

3. I will check whether the high CPU usage is caused by an application process, a system process, or a scheduled job (cron).

4. If the process belongs to an application, I will coordinate with the Application Team to investigate the issue.

5. If the process is stuck or consuming excessive CPU unnecessarily, I will take the necessary action after approval, such as restarting the service or terminating the process.

6. I will review system logs for any errors:

   ```bash
   journalctl -xe
   dmesg
   ```

7. I will check whether the server is experiencing unusually high traffic or workload.

8. If the CPU usage remains consistently high due to increased business requirements, I will recommend scaling the application or upgrading the server resources through the proper change management process.

9. Finally, I will monitor the server to ensure CPU utilization returns to normal and that all services are functioning correctly.

## 4. How to resolve High Memory Uses ?
**If memory utilization is high, I will follow these troubleshooting steps:**

1. First, I will verify memory usage using:

   ```bash
   free -h
   top
   htop
   vmstat 1
   ```

2. I will identify the processes consuming the most memory:

   ```bash
   ps -eo pid,ppid,cmd,%mem --sort=-%mem | head
   ```

3. I will determine whether the memory usage is caused by an application process, a system process, or a memory leak.

4. If the process belongs to an application, I will coordinate with the Application Team for further investigation.

5. If a service is consuming excessive memory due to a temporary issue, I will restart the service after obtaining the required approval.

6. I will check swap usage:

   ```bash
   free -h
   swapon --show
   ```

   High swap usage may indicate memory pressure.

7. I will review system logs for Out of Memory (OOM) events:

   ```bash
   dmesg | grep -i oom
   journalctl -xe
   ```

8. If memory utilization remains consistently high due to workload growth, I will recommend increasing RAM or scaling the application after following the change management process.

9. Finally, I will continue monitoring the server to ensure memory usage returns to normal and all services are working properly.
