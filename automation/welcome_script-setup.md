# Custom System Summary Script (Bash) for Linux

---

## What Does This Script Do?

- Prints a short welcome message and current date/time (Riga time zone).
- Shows disk usage for the root filesystem.
- Displays current CPU load averages.
- Displays memory usage (total and used).
- Checks how many system updates are available (for apt-based systems).
- Formats output for quick, readable system status at a glance.

---

## Example Script

```bash
#!/bin/bash

# -------- CUSTOM SYSTEM SUMMARY --------
echo "----------------------------"
echo "Welcome, Big Dog"
echo -n "Date & Time (Riga): "
TZ="Europe/Riga" date +"%Y-%m-%d %H:%M:%S"
echo

echo "Disk Usage:"
df -h / | awk 'NR==1 || NR==2 {print $1, $2, $3, $4, $5, $6}'
echo

echo "CPU Load:"
uptime | awk -F'load average:' '{print "Load average:" $2}'
echo

echo "Memory Usage:"
free -h | awk 'NR==1 || NR==2'
echo

echo -n "Available Updates: "
if command -v apt &>/dev/null; then
    updates=$(apt list --upgradable 2>/dev/null | grep -v "Listing" | wc -l)
    if [ "$updates" -eq 0 ]; then
        echo "System up to date."
    else
        echo "$updates package(s) can be updated!"
    fi
fi
echo "----------------------------"

##  How to Use

1. **Save the script:**  
   Example filename: `system_summary.sh`

2. **Make it executable:**
    ```bash
    chmod +x system_summary.sh
    ```

3. **Run the script:**
    ```bash
    ./system_summary.sh
    ```


##  Tips

- **Auto-run at SSH login:**  
  Add this script to your `.bash_profile` or `.bashrc` to display the summary every time you log in via SSH.
- **Different Linux distros:**  
  Adjust the package manager commands if you are not using `apt` (e.g., use `dnf` or `yum` for CentOS/Fedora).
- **Timezone:**  
  Change the timezone variable if you want local time for a different city (`TZ="Europe/Riga"`).
