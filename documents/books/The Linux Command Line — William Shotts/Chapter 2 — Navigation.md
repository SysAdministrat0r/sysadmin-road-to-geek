````markdown
### 🌳 File System Structure

- Linux uses a **hierarchical directory structure** (a single, tree-like system starting from `/`, the root).
- Unlike Windows, all storage devices are mounted into this single file system tree.
- The **root directory** `/` contains all other files and directories.

---

### 📂 Current Working Directory

- The directory I am currently “in” is called the **current working directory**.
- To display it:
  ```shell
  pwd
````

*Example output:*

```
/home/me
```

* When I open a terminal, my starting directory is my **home directory**.

---

### 📋 Listing Directory Contents

* To see what’s in the current directory:

  ```shell
  ls
  ```

  *Example output:*

  ```
  Desktop  Documents  Music  Pictures  Public  Templates  Videos
  ```
* `ls` can also be used with other directories:

  ```shell
  ls /usr/bin
  ```

---

### 🔀 Changing Directories

* To move to another directory:

  ```shell
  cd /path/to/dir
  ```
* Two types of paths:

  * **Absolute path**: starts with `/`, always from root.

    ```shell
    cd /usr/bin
    ```
  * **Relative path**: from the current location.

    ```shell
    cd ..
    cd ./bin
    cd bin   # (the ./ is implied)
    ```

#### **Special notations**

* `.` = current directory
* `..` = parent directory

---

### 🏷️ Important Facts About Filenames

* Files beginning with a `.` are **hidden** (`ls -a` shows them).
* Filenames and commands are **case-sensitive**: `File1` ≠ `file1`
* Avoid spaces and punctuation in filenames; prefer underscores (`_`), dashes (`-`), or periods (`.`).
* Linux doesn't rely on file extensions to determine file type (but some apps do).

---

### ⚡ Useful `cd` Shortcuts

| Shortcut       | What it does                                          |
| -------------- | ----------------------------------------------------- |
| `cd`           | Go to my home directory                               |
| `cd -`         | Go to previous working directory                      |
| `cd ~username` | Go to another user's home directory (e.g., `cd ~bob`) |

---

### 📝 In Short

This chapter explained how the shell treats the directory structure of the system.
The main focus was on absolute and relative pathnames and the basic commands to move around the structure.
I noticed it can be tricky to remember all the path shortcuts at first, but the logic becomes clear after some practice.
It was interesting to learn how all drives are part of one big tree and not separated by letters, like in Windows.

---