# Creating a Hello, World Program

## Lab Overview
Welcome to Introduction to Programming. For the labs, I will be using the Python programming language.
---


      ___        ______     ____ _                 _  ___  
        / \ \      / / ___|   / ___| | ___  _   _  __| |/ _ \ 
       / _ \ \ /\ / /\___ \  | |   | |/ _ \| | | |/ _` | (_) |
      / ___ \ V  V /  ___) | | |___| | (_) | |_| | (_| |\__, |
     /_/   \_\_/\_/  |____/   \____|_|\___/ \__,_|\__,_|  /_/ 
 ----------------------------------------------------------------- 

## Accessing the AWS Cloud9 IDE

I started my lab environment by going to the top of the instructions and choosing **Start Lab**.

A Start Lab panel opened, displaying the lab status.

I waited until I saw the message `Lab status: ready`, and then closed the Start Lab panel by choosing the **X**.

At the top of the instructions, I chose **AWS**.

The AWS Management Console opened in a new browser tab. The system automatically logged me in.

> **Note:** If a new browser tab doesn't open, a banner or icon at the top of your browser typically indicates that your browser is preventing the site from opening pop-up windows. Choose the banner or icon, and choose **Allow pop ups**.

In the AWS Management Console, I chose **Services** > **Cloud9**. In the Your environments panel, I located the `reStart-python-cloud9` card and chose **Open IDE**.

<img width="1908" height="913" alt="Screenshot 2026-03-04 095710" src="https://github.com/user-attachments/assets/92b22d88-ccaa-48db-b7d2-3356badbb627" />

The AWS Cloud9 environment opened.

> **Note:** If a pop-up window opened with the message `.c9/project.settings have been changed on disk`, I chose **Discard** to ignore it. Likewise, if a dialog window prompted me to **Show third-party content**, I chose **No** to decline.

---

## Creating My Python Exercise File

From the menu bar of the AWS Cloud9 IDE, I chose **File** > **New From Template** > **Python File**.

This action created an untitled file.

I deleted the sample code that was provided in the template file.

I chose **File** > **Save As...**, and provided a suitable name for the exercise file (`hello-world.py`) and saved it under the `/home/ec2-user/environment` directory.

> **Note:** The `.py` is the extension for Python files.

---

## Accessing the Terminal Session

In my AWS Cloud9 IDE, I chose the **+** icon and selected **New Terminal**.

A terminal session opened.

To display the present working directory, I entered `pwd`. This command pointed to `/home/ec2-user/environment`.

In this directory, I was able to locate the file I created in the previous section.

<img width="1903" height="906" alt="Screenshot 2026-03-04 100406" src="https://github.com/user-attachments/assets/ec864b8b-7da8-4876-808a-909adbafa77c" />
---

## Exercise 1: Introducing Python

Python is a high-level, general-purpose programming language. Programming languages are used to write instructions for computers. High-level means that Python commands are written with a combination of English words and special symbols. General-purpose means that Python is used by many people for different types of applications, such as desktop applications and websites.

Python has two major releases in use today, which are known as Python version 2.x and Python version 3.x. For Introduction to Programming, I will use Python version 3.6.x. Backward compatibility means that legacy code continues to work in new versions of the language. Generally, Python remains backward compatible within minor version releases. However, the major versions have syntax incompatibilities between them, such as between Python version 2.x and Python version 3.x.

The [python.org](https://www.python.org) website has installers and general documentation for Python.

Most systems will have one or more versions of Python installed, with Python version 2.7 as the default.

### Checking Python Versions

To confirm the default version of Python that is installed in my lab, in the open terminal tab, I entered:

```bash
python --version
```

To check other available versions of Python, I entered the following commands:

```bash
python2 --version
python3 --version
```

I saw results similar to the following examples:

```
~ $ python --version                                                                      
Python 3.6.12                                                                                    
~ $ python2 --version                                                                     
Python 2.7.18                                                                                    
~ $ python3 --version                                                                     
Python 3.6.12
```

---

## Exercise 2: Writing My First Python Program

When someone learns how to program, it's traditional to start with the Hello, World program. This simple program verifies that you have installed the Python tools correctly.

From the navigation pane of the IDE, I chose the file that I created earlier (`hello-world.py`).

In the file, I entered the following code:

```python
print("Hello, World")
```

<img width="1897" height="906" alt="Screenshot 2026-03-04 100828" src="https://github.com/user-attachments/assets/3fd4706a-8ba1-4637-94e2-ed95614a1ffe" />

To save my file, I chose **File** > **Save**.

Near the top of the IDE window, I chose the **Run** (Play) button.

In the bottom pane of the IDE, I confirmed that the program printed the words **Hello World**.

---

## What I Accomplished

I successfully wrote and executed my first Python program! This simple exercise helped me verify that my Python environment is set up correctly and that I understand the basic workflow of creating, saving, and running Python files in AWS Cloud9.

---

## Key Takeaways

- Python is a high-level, general-purpose programming language
- There are two major Python versions (2.x and 3.x) with syntax differences
- The `print()` function outputs text to the console
- AWS Cloud9 provides an integrated development environment for writing and running Python code
- The traditional Hello, World program is the first step in learning any programming language
```
