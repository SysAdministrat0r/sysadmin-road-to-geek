#!/bin/bash

#  CUSTOM WELCOME MESSAGE

echo ""
echo "┌─────────────────────────────────────────────┐"
echo "│       🐧 Welcome back, Kirill 🐾            │"
echo "└─────────────────────────────────────────────┘"
echo ""

# Date & Time in Riga
echo -e "📅 Date       : \e[1;36m$(TZ='Europe/Riga' date '+%A, %d %B %Y %H:%M:%S')\e[0m"

# Hostname and IP
hostname=$(hostname)
ip=$(hostname -I | awk '{print $1}')
echo -e "🖥️ Hostname    : \e[1;36m$hostname ($ip)\e[0m"

# Uptime
uptime_now=$(uptime -p)
echo -e "⏳ Uptime     : \e[1;36m$uptime_now\e[0m"

# Disk usage of root
disk_usage=$(df -h / | awk 'NR==2 {print $5 " used of " $2}')
echo -e "💾 Disk       : \e[1;36m$disk_usage\e[0m"

# Memory usage

mem_used=$(free -h | awk '/Mem:/ {print $3 " used of " $2}')
echo -e "🧠 Memory     : \e[1;36m$mem_used\e[0m"

# Load average
load=$(uptime | awk -F'load average:' '{print $2}' | sed 's/^ //')
echo -e "🔥 Load Avg   : \e[1;36m$load\e[0m"

# Available updates (APT-based)
if command -v apt &>/dev/null; then
    updates=$(apt list --upgradable 2>/dev/null | grep -v "Listing" | wc -l)
    if [[ "$updates" -eq 0 ]]; then
        echo -e "✅ Updates    : \e[1;32mSystem up to date\e[0m"
    else
        echo -e "⬆️ Updates    : \e[1;33m$updates package(s) available\e[0m"
    fi
fi

echo ""
echo "Have a productive day, commander 🧠"
echo ""
