
### 🔍 Useful Commands

- `ls`: List directory contents
- `file`: Determine file type
- `less`: View file contents (paged, scrollable)

---

### 🗂️ More Fun with `ls`

- List current directory:
  ```shell
  ls


* List specific directories:

  ```shell
  ls /usr
  ls ~ /usr
  ```
* Long format with details:

  ```shell
  ls -l
  ```
* Combine options:

  ```shell
  ls -lt --reverse
  ```

---

#### ⚙️ Command Structure

* Most commands follow:

  ```
  command -options arguments
  ```
* Short options: single dash, e.g. `-l`
* Long options: double dash, e.g. `--reverse`
* Options can be combined: `ls -lt`

---

#### 🧩 Common `ls` Options

| Short | Long             | Description                                                       |
| ----- | ---------------- | ----------------------------------------------------------------- |
| -a    | --all            | List all files, including hidden ones (starting with `.`)         |
| -A    | --almost-all     | Like -a, but omits `.` (current) and `..` (parent)                |
| -d    | --directory      | List directory itself, not contents (combine with -l for details) |
| -F    | --classify       | Append indicator character (`/` for dir, `*` for exec, etc.)      |
| -h    | --human-readable | Human-readable file sizes (e.g. 1K, 234M)                         |
| -l    |                  | Long format                                                       |
| -r    | --reverse        | Reverse the order of results                                      |
| -S    |                  | Sort by file size                                                 |
| -t    |                  | Sort by modification time                                         |

---

#### 📝 `ls -l` Output Fields

| Field            | Meaning                                            |
| ---------------- | -------------------------------------------------- |
| -rw-r--r--       | Permissions (`-`=file, `d`=directory, `l`=symlink) |
| 1                | Number of hard links                               |
| root             | Owner                                              |
| root             | Group                                              |
| 32059            | Size in bytes                                      |
| 2017-04-03 11:05 | Last modification date/time                        |
| oo-cd-cover.odf  | Filename                                           |

---

### 🗃️ Checking File Type with `file`

* Usage:

  ```shell
  file filename
  ```
* Example:

  ```shell
  file picture.jpg
  ```

  Output: `picture.jpg: JPEG image data, JFIF standard 1.01`

---

### 📖 Viewing File Contents with `less`

* Usage:

  ```shell
  less filename
  ```
* Example:

  ```shell
  less /etc/passwd
  ```
* Exit less: press `q`

#### 🕹️ Common `less` Hotkeys

| Key                 | Action                  |
| ------------------- | ----------------------- |
| Page Up / `b`       | Scroll back one page    |
| Page Down / `Space` | Scroll forward one page |
| ↑ / ↓               | Scroll up/down one line |
| G                   | Go to end of file       |
| 1G or g             | Go to beginning of file |
| `/text`             | Search for `text`       |
| n                   | Next search result      |
| h                   | Help screen             |
| q                   | Quit                    |

---

### 📁 Linux Filesystem Tour

| Directory        | Description                                           |
| ---------------- | ----------------------------------------------------- |
| `/`              | Root directory; everything starts here                |
| `/bin`           | Essential system binaries                             |
| `/boot`          | Linux kernel, bootloader configs                      |
| `/dev`           | Device files; “everything is a file” includes devices |
| `/etc`           | System-wide configuration files                       |
| `/home`          | User home directories                                 |
| `/lib`           | Shared libraries                                      |
| `/lost+found`    | Recovered files after filesystem errors               |
| `/media`         | Mount points for removable media (USB, CD, etc.)      |
| `/mnt`           | Temporary mount points                                |
| `/opt`           | Optional/additional software                          |
| `/proc`          | Virtual filesystem; kernel and process information    |
| `/root`          | Home directory for root user                          |
| `/sbin`          | System binaries (admin tasks, usually for root)       |
| `/tmp`           | Temporary files (often wiped on reboot)               |
| `/usr`           | User utilities and applications                       |
| `/usr/bin`       | Most user commands and programs                       |
| `/usr/lib`       | Libraries for `/usr/bin` programs                     |
| `/usr/local`     | Locally installed software                            |
| `/usr/sbin`      | More system administration programs                   |
| `/usr/share`     | Shared data, docs, icons, etc.                        |
| `/usr/share/doc` | Documentation for installed packages                  |
| `/var`           | Variable data, logs, mail, databases, etc.            |
| `/var/log`       | System log files                                      |

---

### 🔗 Symbolic and Hard Links

* **Symbolic link (symlink):**
  File that points to another file; useful for managing versions.
  Example listing:

  ```
  lrwxrwxrwx 1 root root 11 2018-08-11 07:34 libc.so.6 -> libc-2.6.so
  ```
* **Hard link:**
  Another name for a file; more on this in the next chapter.

---

### 📝 In Short

This chapter was mostly about exploring the Linux file system and getting comfortable with core commands like `ls`, `file`, and `less`.
It was a bit tricky to quickly remember all the `ls` options and fully understand what each field in the long format output means.
I found it interesting how Linux directories are so open for exploration, and how so many important files are just plain text that I can read with `less`.
The explanation about symbolic links made sense, but I feel like I’ll need more practice to really get how and when to use them.
The overview of system directories was actually fun — now I know where to look for logs, configs, or binaries.

---

