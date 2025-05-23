# How to Clean System Cache Automatically (systemd timer)

## 1. Create the script

Create the script file:

```bash
sudo nano /usr/local/bin/clean_system.sh
````

Paste this script:

```bash
#!/bin/bash
# Script to clean system cache and temporary files, with a summary of cache cleared.

get_cache_size() {
    cache_kb=$(grep ^Cached: /proc/meminfo | awk '{print $2}')
    echo $((cache_kb / 1024))
}

start_cache=$(get_cache_size)
echo "Cache before cleanup: ${start_cache} MB"

echo "Clearing RAM cache..."
sudo sync
echo 1 | sudo tee /proc/sys/vm/drop_caches > /dev/null

echo "Removing temporary files..."
sudo rm -rf /tmp/*
sudo rm -rf /var/tmp/*

echo "Removing apt cache packages..."
sudo apt-get autoremove -y
sudo apt-get autoclean -y

end_cache=$(get_cache_size)
removed_cache=$((start_cache - end_cache))

echo "Cache cleared: $removed_cache MB"
echo "Cleanup complete."
```

Make it executable:

```bash
sudo chmod +x /usr/local/bin/clean_system.sh
```

---

## 2. Create a systemd service

```bash
sudo nano /etc/systemd/system/clean_system.service
```

Paste:

```
[Unit]
Description=Clean system cache and temp files
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/clean_system.sh
StandardOutput=append:/var/log/clean_system.log
StandardError=append:/var/log/clean_system.log
User=root
```

Save and exit.

---

## 3. Create a systemd timer

```bash
sudo nano /etc/systemd/system/clean_system.timer
```

Paste:

```
[Unit]
Description=Run clean_system.sh every hour

[Timer]
OnCalendar=hourly
Persistent=true

[Install]
WantedBy=timers.target
```

Save and exit.

---

## 4. Reload systemd, enable and start the timer

```bash
sudo systemctl daemon-reload
sudo systemctl enable clean_system.timer
sudo systemctl enable clean_system.service
sudo systemctl start clean_system.timer
```

---

## 5. Check status and logs

* To see if the timer is active:

  ```bash
  systemctl list-timers --all | grep clean_system
  ```
* To check the cleanup log:

  ```bash
  tail -n 50 /var/log/clean_system.log
  ```

---

This setup will **automatically clean your system every hour** and log the results to `/var/log/clean_system.log`.
