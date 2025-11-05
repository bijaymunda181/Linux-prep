## User Management
1. How do you create a new user in Linux with a home directory and default shell as /bin/bash?

2. How can you change the username of an existing user in your system?

3. Suppose you want to delete a user along with their home directory — which command will you use?

4. How do you lock and unlock a user account in Linux?

5. A user’s home directory is full, and you need to move it to a new location — how would you do that?

6. How can you check the UID, GID, and group memberships of a particular user?

7. What’s the difference between /etc/passwd and /etc/shadow files?

8. How do you set a password expiration policy for a user so they must change it every 30 days?

9. How can you check when a user last changed their password?

10. If a user forgets their password, how do you reset it safely without deleting the account?

## Group Management
1️⃣ How do you create a new group named devops?

2️⃣ How can you rename an existing group from devops to adminteam?

3️⃣ A user bijay needs to be added to the group adminteam — how do you do it?

4️⃣ How do you remove the user bijay from the group adminteam?

5️⃣ How can you change the group ID (GID) of a group named developers to 1050?

6️⃣ Which file contains information about groups in Linux?

7️⃣ How do you check which groups a user bijay belongs to?

8️⃣ How do you set the group ownership of a file named project.txt to devops?

9️⃣ What’s the difference between a primary group and a secondary group?

🔟 How can you create a new user and make sure their primary group is developers?

## Process management
1️⃣ How do you check all currently running processes in your system?

2️⃣ How do you find the process ID (PID) of a specific service, for example sshd?

3️⃣ What command will you use to terminate a process by PID?

4️⃣ What is the difference between kill, killall, and pkill commands?

5️⃣ How can you see processes of a specific user, for example bijay?

6️⃣ How do you check the top resource-consuming processes in real time?

7️⃣ How can you send a process to the background and bring it back to the foreground?

8️⃣ What’s the difference between a zombie process and an orphan process?

9️⃣ How can you change the priority (nice value) of a running process?

🔟 A process with PID 5678 is stuck — how can you forcefully kill it?

## Disk Management
1️⃣ How do you check the list of all disks and partitions available on your Linux system?

2️⃣ How can you create a new partition on a disk (for example, /dev/sdb)?

3️⃣ After creating a new partition, how do you format it with the ext4 filesystem?

4️⃣ How do you mount a partition (e.g., /dev/sdb1) permanently to /data directory?

5️⃣ How do you check disk space usage for all mounted filesystems?

6️⃣ How can you see which directory is using the most space in /var?

7️⃣ How do you extend a partition or logical volume when it’s running out of space?

8️⃣ How do you check inode usage on your filesystem?

9️⃣ What command is used to check and repair filesystem errors?

🔟 How do you unmount a filesystem safely before making changes or removing a disk?

## Package Management 
1. What is the difference between rpm and yum commands in RHEL/CentOS?

2. How can you check if a package is already installed on your system?

3. How do you find which package provides a specific file (for example, /usr/bin/ls)?

4. What’s the difference between yum install and yum localinstall?

5. How do you list all installed packages and filter by a specific keyword?

6. What command do you use to remove a package and its dependencies?

7. How does dnf differ from yum?

8. If your system cannot access the internet, how would you install packages using a local repository?

9. What’s the use of the /etc/yum.repos.d/ directory?

10. How do you clean the yum cache, and why would you do that?
 
## ✅ Section 1: Static And Dynamic Connections
## 1. Command to check which interface is used for internet routing?
ip route


Look for:

default via <gateway> dev <interface>

## 2. DHCP server down — who gets affected? Static or Dynamic?

Only Dynamic (DHCP) clients.

Static IP devices continue working.

## 3. Set static IP using nmcli
nmcli con add con-name static-ens34 ifname ens34 type ethernet ipv4.method manual ipv4.address 192.168.1.50/24 ipv4.gateway 192.168.1.1 ipv4.dns 8.8.8.8
nmcli con up static-ens34

## 4. Switch back from static to DHCP
nmcli con mod ens34 ipv4.method auto
nmcli con up ens34

## 5. Check active connection vs connected device

Active connection profiles:

nmcli con show --active


Device level status:

nmcli device status

## 6. Can one NIC have both static and DHCP IP?

Yes. A single NIC can have multiple IPs, but:

Only one default gateway is used

Not recommended without advanced routing setup

Command:

nmcli con add con-name secondary-ip ifname ens34 type ethernet ipv4.address 192.168.1.60/24


## 7. What decides which interface is used for routing?

Routing table metrics (priority).

Command:

ip route


Lower metric = higher priority.

## 8. Remove DNS from static configuration — internet gone? Why?

Yes — you can reach IPs but not domain names.

Example:

ping 8.8.8.8 ✅
ping google.com ❌


DNS resolves domain → IP.

## Cronjob
## 🔥 Question 1 : What is crontab and why is it used?


Cron (crond) is a background service used in Linux to schedule recurring tasks.
Crontab (cron table) is a file/command used to create and manage those scheduled jobs.

## 🔥 Question 2: Where are user cron jobs stored in Linux?
User crontab files are stored in:

/var/spool/cron/


(or on some systems)

/var/spool/cron/crontabs/

Example for user bijay:

/var/spool/cron/bijay


/etc/crontab is the system-wide cron file, not the user crontab.

## 🔥 Question 3: What is the difference between crontab -e and editing /etc/crontab?
crontab -e is used to create user-specific cron jobs. The jobs are stored in /var/spool/cron/<username>.

Editing /etc/crontab is for system-wide cron jobs and requires specifying the user who will run the job.

Example difference:

User crontab (crontab -e):

30 2 * * * /scripts/backup.sh


System crontab (/etc/crontab):

30 2 * * * root /scripts/backup.sh

## 🔥 Question 4: How do you list cron jobs for a specific user?
The command crontab -l -u username (or short form crontab -lu username) is used to list cron jobs of a specific user.

## 🔥 Question 5: How do you remove all cron jobs for the current user?
To remove all cron jobs for the current user:

crontab -r
