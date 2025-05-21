# Fail2Ban: Basic Setup & SSH Protection

Fail2Ban is a log-parsing application that protects Linux systems from various types of attacks, particularly those targeting services that interact with the internet, like SSH. The primary goal of Fail2Ban is to monitor log files for suspicious activity and dynamically modify firewall rules to block IP addresses of hosts exhibiting malicious behavior.

---

## Update the System

```bash
apt update -y
apt upgrade -y
````

---

## Install Fail2ban

```bash
apt install fail2ban
```

---

## Install and Configure Firewall

Install UFW:

```bash
apt install ufw
```

Enable UFW:

```bash
ufw enable
```

Allow SSH:

```bash
ufw allow 22
```

Reload UFW:

```bash
ufw reload
```

---

## Configure Fail2ban for SSH

Copy default config:

```bash
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

Open `jail.local` in editor:

```bash
nano /etc/fail2ban/jail.local
```

Find the `[sshd]` section and set:

```ini
[sshd]
enabled  = true
port     = ssh
filter   = sshd
logpath  = /var/log/auth.log
maxretry = 3
```

**Configuration Settings:**

* `enabled`: Set to true to enable the rule.
* `port`: The port where your SSH service is running (default is ssh = 22).
* `filter`: The filter to be used (`sshd`).
* `logpath`: Path to the SSH log file.
* `maxretry`: Number of failures before an IP is banned.

Save and close the file.

---

## Restart Fail2ban

```bash
systemctl restart fail2ban
```

---

## Verify Fail2ban Status

```bash
systemctl status fail2ban
```

**Sample Output:**

```
root@vps:~# systemctl status fail2ban
● fail2ban.service - Fail2Ban Service
     Loaded: loaded (/lib/systemd/system/fail2ban.service; enabled; preset: enabled)
     Active: active (running) since Fri 2023-11-10 22:05:03 UTC; 40min ago
       Docs: man:fail2ban(1)
   Main PID: 15873 (fail2ban-server)
      Tasks: 5 (limit: 4644)
     Memory: 14.0M
        CPU: 503ms
     CGroup: /system.slice/fail2ban.service
             └─15873 /usr/bin/python3 /usr/bin/fail2ban-server -xf start
```

---

## Check Jail Status

```bash
fail2ban-client status sshd
```

---

## Manual Ban/Unban

Unban an IP:

```bash
fail2ban-client set sshd unbanip <IP_ADDRESS>
```

Ban an IP:

```bash
fail2ban-client set sshd banip <IP_ADDRESS>
```

If banned, trying to log in will show:

```
root@vps:~# ssh root@<Your_IP_Address>
ssh: connect to host <Your_IP_Address> port 22: Connection refused
```
