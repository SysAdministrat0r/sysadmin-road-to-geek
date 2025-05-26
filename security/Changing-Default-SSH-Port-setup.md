# Changing Default SSH Port (22 → 25022) on Debian

## Why?
Changing the default SSH port adds a basic layer of security and reduces automated attacks.

---

## Step-by-Step Guide

1. **Edit SSH config:**
    ```bash
    sudo nano /etc/ssh/sshd_config
    ```
    - Find the line `#Port 22`
    - Uncomment it (remove `#`)
    - Change `22` to your desired port, e.g. `25022`:
        ```
        Port 25022
        ```

2. **Allow the new port in UFW (firewall):**
    ```bash
    sudo ufw allow 25022
    ```

3. **Restart the SSH daemon:**
    ```bash
    sudo systemctl restart sshd
    ```

4. **Do NOT close your current SSH session**  
   Before disconnecting, **open a new SSH window** and test the new port:
    ```bash
    ssh -p 25022 user@your_server_ip
    ```
   This way, if you made a mistake, you won't lose access.

5. **(Optional) Remove old SSH port from UFW:**
    ```bash
    sudo ufw delete allow 22
    ```


---

**Changing the SSH port is a simple but effective way to reduce unwanted login attempts.**
