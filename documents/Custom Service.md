# 🛠️ How to Create Your Own Custom Service in Linux

> Reference:  
> [Creating a Custom Service in Linux (Akhilesh Patel, LinkedIn)](https://www.linkedin.com/pulse/creating-custom-service-linux-akhilesh-patel/)

This guide walks you through creating and managing your own custom Linux service using **systemd**.  
Services let you automate scripts and tasks to run in the background, at boot, or on demand—just like "real" Linux daemons.

---

## 🚩 Step-by-Step: Create Your Own Systemd Service

### **Step 1: Write Your Script**

Create the script or program you want to run as a service.  
Example: `my_service.sh`

```bash
#!/bin/bash
while true; do
    echo "Service is running at $(date)" >> /var/log/my_service.log
    sleep 60
done
````

> *Make sure your script does what you want in the background. Test it manually first!*

---

### **Step 2: Move the Script to a System Directory**

Move your script to a directory for user scripts (e.g., `/usr/local/bin`):

```bash
sudo mv my_service.sh /usr/local/bin/
sudo chmod +x /usr/local/bin/my_service.sh
```

---

### **Step 3: Create the Service File**

Create a `.service` unit file in `/etc/systemd/system/`. Example: `my_service.service`

```bash
sudo nano /etc/systemd/system/my_service.service
```

Paste the following:

```ini
[Unit]
Description=My Custom Service
After=network.target

[Service]
ExecStart=/usr/local/bin/my_service.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

**Field meanings:**

* `Description`: Service description.
* `After`: Starts after network services (customize as needed).
* `ExecStart`: Command to launch your script.
* `Restart`: Always restart if the service stops.
* `WantedBy`: Ensures service runs in standard multi-user mode.

---

### **Step 4: Reload Systemd**

Reload systemd so it sees your new service:

```bash
sudo systemctl daemon-reload
```

---

### **Step 5: Enable and Start the Service**

Enable service to start at boot, and start it now:

```bash
sudo systemctl enable my_service
sudo systemctl start my_service
```

---

### **Step 6: Check Service Status**

Check that your service is running and see logs:

```bash
sudo systemctl status my_service
```

To view logs (if any):

```bash
journalctl -u my_service
```

---

## 💡 Why Use Linux Services?

Linux services (daemons) are a core OS feature that provide:

* **Automation:** Run background tasks without user input.
* **Boot Initialization:** Essential processes start as soon as the system boots.
* **Reliability:** Services can auto-restart on failure.
* **Resource Management:** Limit CPU/memory usage.
* **Networking:** Manage network connections, servers, DNS, DHCP, etc.
* **Security:** Run with limited privileges to reduce attack risk.
* **Customization:** Automate backups, monitoring, hardware control, and more.
* **Remote Management:** Control services over SSH or other remote tools.
* **Logging & Monitoring:** Track behavior and troubleshoot issues.
* **Scalability:** Easily handle increased workloads.
* **Modularity:** Enable, disable, or swap services without breaking the system.
* **Third-party Software:** Many apps require services for core functions.

> *In summary: Managing services is a key sysadmin skill for automation, stability, and reliability!*

---


```
```
