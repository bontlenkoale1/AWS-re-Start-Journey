# Introduction to an Amazon Linux Amazon Machine Image (AMI) 🐧

## Lab Overview

This lab is designed to reinforce knowledge of basic command line interface functionality and provide a solid foundation for learning new commands and capabilities within the Linux shell. Understanding Linux fundamentals is essential for cloud computing, as many AWS services and EC2 instances run on Linux-based operating systems.

In this lab, I used Secure Shell (SSH) to access an Amazon Linux AMI within the Vocareum lab environment. I then explored the manual pages (`man` command) to understand how to access documentation and help resources directly from the command line.

---

## 🎯 Lab Objectives

After completing this lab, I successfully:

- ✅ **Used SSH** to access an Amazon Linux AMI within Vocareum labs
- ✅ **Understood** the purpose of the `man` command for accessing documentation
- ✅ **Demonstrated** the search feature of the man pages
- ✅ **Examined** man page headers and their significance

---

## 📋 Prerequisites

The lab environment came pre-configured with:
- **Amazon EC2 Command Host** (t3.micro instance in a public subnet) running Amazon Linux AMI
- **Amazon VPC** with necessary networking components
- SSH key pair for secure authentication

---

## 🔧 Step-by-Step Implementation

### **Task 1️⃣: Use SSH to Connect to an Amazon Linux EC2 Instance**

In this task, I connected to the Amazon Linux EC2 instance using SSH. The instructions vary slightly depending on the operating system.

#### **For Windows Users (Using PuTTY)**

1. **Retrieve Connection Details**
   - Selected the **Details** dropdown menu above the instructions
   - Chose **Show** to open the Credentials window
   - Downloaded the **labsuser.ppk** file (saved to Downloads directory)
   - Made note of the **PublicIP** address
   - Closed the Details panel by selecting **X**

2. **Set Up PuTTY**
   - Downloaded and installed PuTTY from [https://www.putty.org/](https://www.putty.org/)
   - Opened `putty.exe`

3. **Configure PuTTY Session**
   - In the **Host Name** field, entered: `ec2-user@<public-ip>` (replacing `<public-ip>` with the copied address)
   - In the left navigation pane, expanded **Connection** → **SSH** → selected **Auth**
   - Clicked **Browse** and navigated to the downloaded `labsuser.ppk` file
   - Returned to **Session** in the left navigation pane
   - Entered a name in the **Saved Sessions** field (e.g., "Amazon Linux Lab")
   - Clicked **Save**
   - Clicked **Open** to start the connection
   - Clicked **Accept** when prompted about the server's host key


#### ✅ Task 1 Summary
I successfully established an SSH connection to the Amazon Linux EC2 instance using the appropriate method for my operating system. This connection provides secure, command-line access to the instance for the remainder of the lab.

---

### **Task 2️⃣: Explore the Linux man Pages**

In this task, I explored the Linux manual pages (man pages)—the built-in documentation system for Linux commands.

#### Steps:

1. **Access the man Pages for the man Command**
   - At the command prompt, I entered:
     ```bash
     man man
     ```
   - This opened the manual pages for the `man` command itself

<img width="1904" height="1019" alt="Screenshot 2026-01-28 172343" src="https://github.com/user-attachments/assets/9cda7481-1c4d-427a-802b-b38e84af33fd" />

2. **Navigate the man Pages**
   - Used the **up and down arrow keys** to scroll through the documentation
   - Observed the structured format of the man pages with various headers
<img width="1919" height="1025" alt="Screenshot 2026-01-28 172212" src="https://github.com/user-attachments/assets/c1639e93-f4e6-434b-b9bd-3439a36147bd" />

3. **Identify Key man Page Headers**

   | Header | Purpose |
   |--------|---------|
   | **NAME** | Displays the command name and brief description |
   | **SYNOPSIS** | Shows the command syntax and available options |
   | **DESCRIPTION** | Provides detailed explanation of the command |
   | **OVERVIEW** | Gives high-level context about the command |
   | **EXAMPLES** | Demonstrates common usage scenarios |
   | **FILES** | Lists files the command uses or references |
   | **OPTIONS** | Details all available command-line options |
   | **SEE ALSO** | Points to related commands and documentation |

6. **Exit the man Pages**
   - Pressed **q** to quit and return to the command prompt

#### ✅ Task 2 Summary
I successfully explored the Linux man pages, learning how to access built-in documentation, navigate through sections, identify key headers, and perform searches. This skill is essential for self-sufficient Linux usage and troubleshooting.

---

## 📊 Commands Learned

| Command | Purpose | Example |
|---------|---------|---------|
| `ssh` | Securely connect to remote server | `ssh -i key.pem user@ip` |
| `man` | Display manual pages for commands | `man man` |
| `q` | Quit/exit man pages | Press `q` |
| `/` | Search within man pages | `/searchterm` |
| `n` | Go to next search result | Press `n` |
| Arrow keys | Navigate up/down in man pages | ↑ ↓ |

---

## 🎓 Lab Summary

In this lab, I successfully:

1. **Connected to an Amazon Linux EC2 instance** using SSH with key-based authentication
2. **Accessed the Linux manual pages** to understand command documentation
3. **Navigated through man pages** using arrow keys and search functionality
4. **Identified key man page headers** including NAME, SYNOPSIS, DESCRIPTION, and EXAMPLES
5. **Learned about man page sections** and their purposes
6. **Practiced searching** within documentation for efficient information retrieval

---

## 🎯 Objectives Achieved

| Objective | Completed |
|-----------|-----------|
| Use SSH to access an Amazon Linux AMI | ✅ |
| Understand the purpose of the `man` command | ✅ |
| Demonstrate the search feature of the man pages | ✅ |
| Examine man page headers | ✅ |

---

## 📝 Key Takeaways

- **SSH** is the standard protocol for secure remote access to Linux instances in the cloud
- **Key-based authentication** provides stronger security than password authentication
- The **man pages** are the definitive source of documentation for Linux commands
- Man pages are **structured with standardized headers** for easy navigation
- **Section numbers** organize documentation by topic (commands, system calls, etc.)
- **Search functionality** (`/`) makes finding specific information efficient
- Being comfortable with command-line documentation is essential for **self-sufficient cloud administration**

---

## 🔗 Additional Resources

- [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)
- [Amazon Machine Images (AMI)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)
- [Connect to Your Linux Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html)
- [Linux man Pages Online](https://man7.org/linux/man-pages/)
- [Status Checks for Your Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-system-instance-status-check.html)
- [Amazon EC2 Service Quotas](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-resource-limits.html)

---
