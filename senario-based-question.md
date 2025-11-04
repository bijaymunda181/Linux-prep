## 🔹 Scenario 1: Disk Space Issue

You receive an alert that the root partition / on a production server is 100% full.

👉 What exact steps will you take to find out the cause and fix the issue — without rebooting the system?

## 🔹 Scenario 2: Service Down – “502 Bad Gateway”

You get a call that a website hosted on an Nginx server is showing a “502 Bad Gateway” error.
You log in and see that Nginx service is running, but the website still doesn’t load.

👉 What will you check step by step to identify and fix the issue?

## Scenario 3: High CPU Usage

You get an alert that a Linux server is running very slow, and CPU utilization is near 100%.

👉 As a Linux administrator, how will you identify which process is causing the issue and fix it step by step — without rebooting the system?

## Scenario 4: Filesystem / Partition Not Mounting on Reboot

You created a new partition /dev/sdb1 on a production server, formatted it, and mounted it to /mnt/data. It works fine immediately after mounting.

But after a reboot, the partition is not mounted automatically.

👉 What steps will you take to fix this issue so that it mounts automatically on every boot?

(Explain commands, files, and reasoning like a Linux admin.)

## Scenario 5: Permission Denied on a File

A developer reports that they cannot write to a log file /var/log/app/app.log, even though the file exists. You check and the permissions seem fine for the user.

👉 What steps will you take to troubleshoot and fix this issue?

## Scenario 6: SSH Access Problem

You’re trying to SSH into a remote Linux server, but the connection fails with an error like:

“Permission denied” or “Connection timed out.”

You confirm that network connectivity is fine, and the sshd service is running on the target server.

👉 As a Linux administrator, what will you check step by step to identify and fix this SSH login issue?

## Scenario 7: Slow Boot Issue

A Linux server takes a very long time to boot up — several minutes before reaching the login prompt.

👉 As a Linux administrator, what steps will you take to find out what’s causing the slow boot and how will you fix it?

## 🔹 Scenario 8: Sudo Not Working for a User

A user named devops reports that they cannot run any command with sudo.
When they try, it says:

devops is not in the sudoers file. This incident will be reported.

👉 As a Linux administrator, what exact steps will you take to fix this problem safely?

## Scenario 9: Cron Job Not Working

A cron job is scheduled for user devops to run a script /home/devops/backup.sh every day at midnight.

The cron entry looks like this:

0 0 * * * /home/devops/backup.sh


But the script did not run as expected.

👉 As a Linux administrator, how will you troubleshoot and fix this cron job issue step by step?

## 🧠 Scenario 10:

A file used by a running application was accidentally deleted from the system.
Even though it’s deleted, the application is still running fine.
How will you recover or handle this situation?
</br>
🧩 Scenario Explanation:

When a file is deleted in Linux, it is removed from the directory structure, but if a process is still using it (open file handle), the data remains in memory or disk (until the process ends).

That’s why the application still runs fine — it still has the file open in memory, even though you can’t see it on disk.

✅ Step-by-Step Recovery
1️⃣ Identify the process that had the file open

Use the lsof command:

lsof | grep deleted


🔹 This lists all files that are marked as deleted but still held open by a running process.
Example output:

nginx   1523   root  4r   REG   8,1  1048576  12345 /var/log/nginx/access.log (deleted)

2️⃣ Check process details

To see more info about the process:

ps -p 1523 -o pid,cmd

3️⃣ Copy the file back from /proc

Each running process has its open files stored in /proc/<PID>/fd/.

In this case:

cp /proc/1523/fd/4 /var/log/nginx/access.log


✅ This command recovers the deleted file while the process is still running.

4️⃣ Verify

Check if the file content is restored:

ls -l /var/log/nginx/access.log

5️⃣ Prevent future issues

Always rotate or truncate logs instead of deleting them directly.
Example:

> /var/log/nginx/access.log


(This clears the file content without deleting the file.)

💡 In short
Step	Command	Purpose
1	`lsof	grep deleted`
2	cp /proc/<PID>/fd/<FD> /path/to/file	Recover the deleted file
3	> filename	Truncate safely instead of deleting

## ✅ Section 1: Static And Dynamic Connections
 ## 1. Your SSH session disconnects when you down one interface. Why?

Because SSH is using that interface as the default route.
When the interface goes down, route disappears → SSH loses connection.

✅ Key concept: Internet/SSH traffic flows through the interface with the default gateway.

## 2. Two NICs: ens33 = DHCP, ens34 = Static

If ens33 has default route and you down ens34, what happens?

Nothing. SSH still stays connected.

Because traffic was not using ens34 in the first place.

## 3. "Internet not working after static IP configuration" — possible reasons

Gateway missing or wrong

DNS missing or wrong

Wrong subnet mask

IP conflict in network

✅ Remember: Static IP = you must define IP + Gateway + DNS

## 4. Static IP configured, but still getting DHCP address. Why?

Because DHCP connection profile (or autoconnect) is still active.

Fix:

nmcli con down "DHCP-connection"
nmcli con up "static-connection"


Or disable autoconnect on DHCP:

nmcli con mod "DHCP-connection" connection.autoconnect no

## 5. Server uses static IP but network team changes gateway. What happens?

Server becomes isolated from other networks (including Internet).

Static IP won’t auto-update gateway → Manual update needed.



