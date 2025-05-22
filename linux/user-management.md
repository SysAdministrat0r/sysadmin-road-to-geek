#  Linux User Management – Basic Commands

---

##  1. Create a New User

```bash
sudo adduser <username>
````

* You will be prompted to enter a password and provide optional info (Full Name, etc.).
* This also creates the user's home directory and sets default shell and group.

---

##  2. View User Info

### Basic account details (UID, GID, groups):

```bash
id <username>
```

### Full account entry from `/etc/passwd`:

```bash
cat /etc/passwd | grep <username>
```

Output includes:

* Username
* UID (User ID)
* GID (Group ID)
* Home directory
* Default shell

---

##  3. Group Management

### Show all groups the user belongs to:

```bash
groups <username>
```

### Add a user to a group:

```bash
sudo usermod -a -G <groupname> <username>
```

> `-a` means "append", `-G` is used to specify the group(s). Without `-a`, the user is removed from all other groups.

### Remove a user from a group:

```bash
sudo deluser <username> <groupname>
```

---

##  4. Passwords and Switching Users

### Change a user’s password:

```bash
sudo passwd <username>
```

### Switch to another user:

```bash
su <username>
```

---

##  File Permissions

### Change file/folder permissions:

```bash
chmod [permissions] [filename]
```

Example:

```bash
chmod 755 script.sh
```

* `755`: Owner can read/write/execute; others can read/execute.
* Use `chmod +x` to make a script executable.

---
