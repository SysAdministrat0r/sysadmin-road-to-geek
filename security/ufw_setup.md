#  Setting Up UFW on Debian VPS

##  Basic UFW Setup Steps

1. **Install UFW (if not installed):**
    ```bash
    sudo apt update
    sudo apt install ufw
    ```

2. **Allow essential ports (SSH, HTTP, HTTPS):**
    ```bash
    sudo ufw allow ssh
    sudo ufw allow http
    sudo ufw allow https
    ```

3. **Set default policies:**
    ```bash
    sudo ufw default deny incoming
    sudo ufw default allow outgoing
    ```

4. **Enable the firewall:**
    ```bash
    sudo ufw enable
    ```

5. **Check status and active rules:**
    ```bash
    sudo ufw status verbose
    ```

---

##  Example of My Current UFW Rules

```plaintext
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22                         ALLOW IN    Anywhere                  
22/tcp                     ALLOW IN    Anywhere                  
80/tcp                     ALLOW IN    Anywhere                  
443                        ALLOW IN    Anywhere                  
22 (v6)                    ALLOW IN    Anywhere (v6)             
22/tcp (v6)                ALLOW IN    Anywhere (v6)             
80/tcp (v6)                ALLOW IN    Anywhere (v6)             
443 (v6)                   ALLOW IN    Anywhere (v6)             
