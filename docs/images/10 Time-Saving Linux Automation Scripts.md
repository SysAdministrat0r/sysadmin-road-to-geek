# 🚀 10 Time-Saving Linux Automation Scripts

> **Reference:**  
> [10 Time-Saving Linux Automation Scripts Every User Should Know](https://mihirpopat.medium.com/10-time-saving-linux-automation-scripts-every-user-should-know-927ae43a5053)  
>
> A handy collection of essential automation scripts to streamline daily Linux tasks. Copy, tweak, and schedule these scripts as you like!

---

## 1. Automated Backup Script

**What it does:**  
Automatically creates a backup of your home directory to an external drive or remote server.

```bash
#!/bin/bash

# Source directory to backup
SOURCE="/home/yourusername/"
# Backup destination
DESTINATION="/backup/location/"

# Run rsync to create a backup
rsync -avh --delete $SOURCE $DESTINATION

echo "Backup completed successfully at $(date)"
````

**How to schedule with cron:**

```bash
crontab -e
0 2 * * * /path/to/backup-script.sh
```

*(Runs daily at 2:00 AM)*

---

## 2. Automatic System Updates

**What it does:**
Automatically updates all system packages.

```bash
#!/bin/bash

# Update and upgrade system packages
sudo apt update && sudo apt upgrade -y

echo "System updated successfully at $(date)"
```

**How to schedule with cron:**

```bash
0 4 * * 1 /path/to/update-script.sh
```

*(Runs every Monday at 4:00 AM)*

---

## 3. File Cleanup Script

**What it does:**
Cleans up temporary directories to free disk space.

```bash
#!/bin/bash

# Directories to clean
CLEANUP_DIRS=("/tmp" "/var/tmp")

for DIR in "${CLEANUP_DIRS[@]}"
do
    rm -rf $DIR/*
    echo "Cleaned $DIR"
done

echo "Cleanup completed at $(date)"
```

**How to schedule with cron:**

```bash
0 1 * * * /path/to/cleanup-script.sh
```

*(Runs daily at 1:00 AM)*

---

## 4. Automated Log Rotation

**What it does:**
Compresses and archives log files older than 7 days.

```bash
#!/bin/bash

# Log directory to rotate
LOG_DIR="/var/log/myapp/"
find $LOG_DIR -type f -mtime +7 -exec gzip {} \;

echo "Logs rotated successfully at $(date)"
```

---

## 5. Automated File Sync

**What it does:**
Keeps two directories in sync.

```bash
#!/bin/bash

# Source and destination directories
rsync -avh /source/directory/ /destination/directory/

echo "File sync completed at $(date)"
```

---

## 6. Scheduled Reboot Script

**What it does:**
Automatically reboots your server or PC on schedule.

```bash
#!/bin/bash

# Reboot the system
sudo reboot
```

**How to schedule with cron:**

```bash
0 3 * * 7 /path/to/reboot-script.sh
```

*(Runs every Sunday at 3:00 AM)*

---

## 7. Automatic Disk Usage Alert

**What it does:**
Checks disk usage and sends an email alert if usage exceeds a threshold.

```bash
#!/bin/bash

# Disk usage threshold in percent
THRESHOLD=80
DISK_USAGE=$(df / | grep / | awk '{print $5}' | sed 's/%//')

if [ "$DISK_USAGE" -gt "$THRESHOLD" ]; then
    echo "Disk usage is above $THRESHOLD%. Current usage: $DISK_USAGE%" | mail -s "Disk Usage Alert" your_email@example.com
fi
```

**How to schedule with cron:**

```bash
0 * * * * /path/to/disk-usage-alert.sh
```

*(Runs every hour)*

---

## 8. Automatic Network Monitoring

**What it does:**
Monitors internet connectivity and logs outages.

```bash
#!/bin/bash

# Ping Google to check connectivity
PING_RESULT=$(ping -c 1 google.com | grep "64 bytes" | wc -l)

if [ "$PING_RESULT" -eq 0 ]; then
    echo "Network down at $(date)" >> /var/log/network-monitor.log
fi
```

---

## 9. Automated User Notification

**What it does:**
Sends daily reminder messages to users.

```bash
#!/bin/bash

# Notification message
MESSAGE="Reminder: Submit your weekly report!"

echo $MESSAGE | wall
```

**How to schedule with cron:**

```bash
0 9 * * 1-5 /path/to/user-notification.sh
```

*(Runs every weekday at 9:00 AM)*

---

## 10. System Health Check

**What it does:**
Performs a quick system health check and reports key stats.

```bash
#!/bin/bash

echo "System Health Check - $(date)"

# Show disk usage
echo "Disk Usage:"
df -h

# Show memory usage
echo "Memory Usage:"
free -m

# Show top 5 processes by memory usage
echo "Top Processes:"
ps aux --sort=-%mem | head -5
```

---

## ⚡️ How to Use & Schedule

1. **Save the script:**
   Create a `.sh` file (e.g., `backup.sh`) and add the script content.
2. **Make executable:**
   `chmod +x script-name.sh`
3. **Schedule with cron:**
   `crontab -e` and add the cron line as shown above for each script.

---

*Tip: Store these scripts in your `~/bin` or `/usr/local/bin` for quick access, and always test scripts on non-critical systems first!*

```
```
