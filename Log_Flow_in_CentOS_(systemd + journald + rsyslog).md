## ✅ Log Flow in CentOS (systemd + journald + rsyslog)
┌──────────────┐
│ Applications │  print logs (stdout/stderr, syslog calls)
└──────┬───────┘
│
▼
┌──────────────┐      Reads from kernel ring buffer
│   journald   │ <─── (/proc/kmsg / /dev/kmsg)
└──────┬───────┘
│ Forwards logs via socket (/run/systemd/journal/syslog)
▼
┌──────────────┐
│   rsyslog    │   (pulls logs from journald)
└──────┬───────┘
│
▼
Writes to log files
( /var/log/messages
/var/log/secure
/var/log/cron
/var/log/maillog
...)
