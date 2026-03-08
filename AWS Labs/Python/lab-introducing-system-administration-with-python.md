# Introducing System Administration with Python 🐍

## Lab Overview 🎯

Linux allows administrators to perform many system tasks directly from the terminal using **Bash commands**. Python provides modules that make it possible to execute these commands programmatically.

In this lab, I explored how Python can interact with the operating system to perform administrative tasks by running Bash commands.

The main focus of this lab is learning how to use Python modules such as **`os`** and **`subprocess`** to execute commands from a Python script.

---

## Objectives 📌

In this lab, I learned how to:

* Use **`os.system()`** to run a Bash command
* Use **`subprocess.run()`** to execute Bash commands
* Pass arguments to commands using Python lists
* Retrieve **system information**
* Retrieve **active process information**

---

## Technologies Used 💻

* **Python**
* **Linux**
* **AWS Cloud9 IDE**
* **Bash Commands**

---

# Exercises

## Exercise 1️⃣: Running Bash Commands with `os.system()`

The `os` module allows Python to interact with the operating system. In this exercise, I used **`os.system()`** to execute the `ls` command and list the contents of the current directory.

```python
import os

os.system("ls")
```

**Example Output**

```
sys-admin.py README.md
```

---

## Exercise 2️⃣: Running Commands with `subprocess.run()`

The `subprocess` module provides a more powerful way to run commands and manage processes.

```python
import subprocess

subprocess.run(["ls"])
```
<img width="1906" height="915" alt="Screenshot 2026-03-09 001122" src="https://github.com/user-attachments/assets/91386698-abb7-48e1-936c-e88ebd427eb3" />

**Example Output**

```
sys-admin.py sys-admin_2.py README.md
```

---

## Exercise 3️⃣: Using Command Arguments

Commands can accept additional arguments by passing them as list items.

Example using **long listing format**:

```python
subprocess.run(["ls", "-l"])
```
<img width="1903" height="907" alt="Screenshot 2026-03-09 001141" src="https://github.com/user-attachments/assets/db4207d1-884d-4572-9595-5a0528d889a2" />

**Example Output**

```
total 12
-rw-r--r-- 1 ec2-user ec2-user  55 Apr 16 20:20 sys-admin.py
-rw-r--r-- 1 ec2-user ec2-user 343 Apr 16 19:07 sys-admin_2.py
-rw-r--r-- 1 ec2-user ec2-user 569 Apr  6 02:17 README.md
```

---

## Exercise 4️⃣: Listing Information for a Specific File

You can also provide a specific file name as an argument.

```python
subprocess.run(["ls", "-l", "README.md"])
```
<img width="1900" height="164" alt="Screenshot 2026-03-09 001425" src="https://github.com/user-attachments/assets/b09f0713-7851-4112-bda6-13c9d8e9069f" />

**Example Output**

```
-rw-r--r-- 1 ec2-user ec2-user 569 Apr 6 02:17 README.md
```

---

## Exercise 5️⃣: Retrieving System Information

The `uname` command provides details about the operating system.

```python
command = "uname"
commandArgument = "-a"

print(f"Gathering system information with command: {command} {commandArgument}")
subprocess.run([command, commandArgument])
```

**Example Output**

```
Gathering system information with command: uname -a
Linux ip-172-31-29-181 x86_64 GNU/Linux
```
<img width="1900" height="175" alt="gathering " src="https://github.com/user-attachments/assets/5a135ceb-be15-437e-81ef-bf4b19bb0026" />

---

## Exercise 6️⃣: Retrieving Active Process Information

The `ps` command displays currently running processes on the system.

```python
command = "ps"
commandArgument = "-x"

print(f"Gathering active process information with command: {command} {commandArgument}")
subprocess.run([command, commandArgument])
```

**Example Output**

```
Gathering active process information with command: ps -x
PID TTY      STAT   TIME COMMAND
18976 pts/459 S+    0:00 python3 sys-admin.py
18977 pts/459 R+    0:00 ps -x
```
<img width="1900" height="702" alt="ps" src="https://github.com/user-attachments/assets/6c7a5042-17a5-48d9-99a0-31854866a111" />

---

## Key Takeaways 🚀

* Python can be used for **system administration tasks**.
* The **`os` module** allows simple command execution.
* The **`subprocess` module** provides greater control over processes.
* Bash commands can be integrated into Python scripts to automate administrative operations.

---

✔️ Successfully executed multiple **Linux system commands using Python**.

---
