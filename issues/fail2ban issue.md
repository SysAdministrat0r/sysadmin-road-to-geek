# Fail2ban Error: Duplicate Option

**Problem:**  
Fail2ban service failed to start. The logs showed an error like:  
`option 'bantime' in section 'DEFAULT' already exists`

**Solution:**  
- Opened `/etc/fail2ban/jail.local`
- Found and removed the duplicate `bantime` (or other repeated) lines in the `[DEFAULT]` section
- Saved the file
- Restarted fail2ban:
  ```bash
  sudo systemctl restart fail2ban
