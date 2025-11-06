## User Management
## 1. How do you create a new user in Linux with a home directory and default shell as /bin/bash?
   useradd -m -s /bin/bash username


## 2. How can you change the username of an existing user in your system?
usermod -l newname oldname


## 3. Suppose you want to delete a user along with their home directory — which command will you use?
userdel -r username

## 4. How do you lock and unlock a user account in Linux?
usermod -L username   # Lock the account  
usermod -U username   # Unlock the account


## 5. A user’s home directory is full, and you need to move it to a new location — how would you do that?
usermod -d /new/home/dir -m username
-m → moves the contents from the old home directory to the new one

## 6. How can you check the UID, GID, and group memberships of a particular user?
id username


## 7. What’s the difference between /etc/passwd and /etc/shadow files?
/etc/passwd → Stores basic user account information, such as:

username:x:UID:GID:comment:home_directory:login_shell


🔹 Readable by all users.
🔹 The x indicates that the password is stored securely in /etc/shadow.

/etc/shadow → Stores secure password details, including:

username:encrypted_password:last_change:min:max:warn:inactive:expire


🔒 Only readable by the root user.

## 8. How do you set a password expiration policy for a user so they must change it every 30 days?
chage -M 30 username


## 9. How can you check when a user last changed their password?
chage -l username


## 10. If a user forgets their password, how do you reset it safely without deleting the account?
passwd username


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

## 🔥 Question 6: A cron job is not running. How will you troubleshoot it?
Troubleshooting steps when a cron job is not running:

1. Check if cron service is running

systemctl status crond


If stopped:

systemctl start crond

2. Check cron logs

For RHEL/CentOS/Alma/Rocky:

cat /var/log/cron


For Ubuntu/Debian:

grep CRON /var/log/syslog

3. Ensure the script has execute permission

chmod +x /path/script.sh

4. Use full path of binaries in script
Example inside the script:

/usr/bin/rsync
/usr/bin/tar

5. Check user permissions / ownership

chown user:user /path/script.sh

6. Check cron syntax

crontab -e

* * * * * /path/script.sh   ✅ valid

7. Redirect output / errors to log file

*/10 * * * * /path/script.sh >> /tmp/script.log 2>&1

## 🔥 Question 7: A script runs manually but does NOT run in cron. What could be the reason, and how do you fix it?
"A script may run manually but fail in cron because cron does not load user PATH variables.
Fix it by using full paths of commands or exporting PATH inside the script."

✅ Additional Valid Causes (your points)

user doesn't have permission to run script

script not executable

ownership issue

Commands to fix:

chmod +x /script.sh
chown bijay:bijay /script.sh

## 🔥 Question 8: You want to run a cron job every minute. Write the cron expression. 
*/1 * * * * /path/to/script will run the job every 1 minute.

## 🔥 Question 9: You want to run a script every day at 02:30 AM.
30 2 * * * /path/to/script

## 🔥 Question 10: A cron script needs environment variables (for example JAVA_HOME),but cron doesn’t read .bash_profile or .bashrc.Where do you set environment variables for cron jobs?
Environment variables for cron jobs can be set in:

1. Inside the script itself (recommended)

2. At the top of the crontab file

✅ Example 1: Export variables inside the script

Edit your script:

#!/bin/bash
JAVA_HOME=/usr/lib/jvm/java-11
PATH=$PATH:$JAVA_HOME/bin

# your script commands
java -version


## 🔥 Question 11: Your cron job needs to run as root. How do you schedule it? 
This way the cron job doesn't depend on user login environment

Add it to the root user’s crontab using:

sudo crontab -e


Then add your cron job there.

✅ This ensures the job runs with root privileges.

## 🔥 Question 12: You want to disable a cron job without deleting it. What do you do?
To disable a cron job without deleting it, you can comment it out by adding a # at the beginning of the line in the crontab.
Example:

 " # 0 5 * * * /path/to/script.sh "


This keeps the job but stops it from running.

## 🔥 Question 13: User bijay should not create cron jobs. How do you block this user from doing so?
To block user bijay from creating cron jobs, add their username to the file /etc/cron.deny:

echo "bijay" | sudo tee -a /etc/cron.deny


✅ This prevents the user from using the crontab command.

## 🔥 Question 14:A job must run on the first day of every month at 5 AM.
0 5 1 * * command

## 🔥 Question 15: A job should run every 15 minutes between 9 AM and 6 PM.
*/15 9-18 * * * command

## Logrotate
## 🔥 Question 1: What is logrotate and why do we use it in Linux?
Logrotate is a Linux utility used to automatically manage log files by rotating, compressing, deleting, or mailing them to prevent log files from consuming too much disk space.

## 🔥 Question 2: Where is the main configuration file of logrotate located in Linux?
/etc/logrotate.conf

## 🔥 Question 3: Where do applications place their individual logrotate configuration files?
/etc/logrotate.d/

## 🔥 Question 4: What does the rotate option do in logrotate?
rotate 5 means logrotate will keep 5 old rotated log files and delete the older ones.

Example:

myapp.log

myapp.log.1

myapp.log.2

myapp.log.3

myapp.log.4

myapp.log.5 ← last one kept

Anything older than this will be removed.

## 🔥 Question 5: What is the difference between size and maxsize options in logrotate?
✅ Difference between size and maxsize in logrotate:

- size:-	Rotate the log only when the log file reaches that size. (Example: size 100M)

- maxsize:-	Rotate the log immediately if it grows larger than this size, even if the scheduled time (daily/weekly) has not arrived.

## 🔥 Question 6: What is copytruncate used for in logrotate?
copytruncate is used when the application cannot be restarted or reloaded during log rotation.

How it works:

1. logrotate copies the current log file to a new rotated file.

2. Then it truncates (empties) the original log file so the application can continue writing to it.

So, instead of renaming the file, it makes a copy and then clears the original.

## 🔥 Question 7: What does the compress option do in logrotate?
compress compresses the rotated log file (usually into .gz) to save disk space.

## 🔥 Question 8: What is the difference between create and copytruncate?
1. create

- After rotating the old log file (by renaming it), logrotate creates a new empty log file with the same name.

- The application starts writing into the new file.

- Usually used when the application can handle file rotation (reopens log file automatically).

2. copytruncate

- Logrotate copies the log contents to a new rotated file and then truncates (empties) the original file.

- Used when the application keeps the log file open and cannot be restarted/reloaded.

So your answer was on the right track ✅

## 🔥 Question 9: Where does logrotate store its state information (i.e., when logs were last rotated)?
✅ Logrotate stores its state information in this file:

/var/lib/logrotate/logrotate.status


This file keeps track of when each log file was last rotated so logrotate knows whether to rotate again or not.


