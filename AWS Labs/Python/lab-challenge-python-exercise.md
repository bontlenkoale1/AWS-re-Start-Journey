# Prime Number Generator - Python Scripting Exercise 🐍

## Lab Overview 🎯
This lab challenges you to create a Python script that identifies and outputs all prime numbers between 1 and 250. The exercise focuses on fundamental programming concepts including loops, conditional logic, and file operations in Python.
---

## Lab Objectives
By completing this lab, I will:
- Write a Python script to identify prime numbers within a specified range
- Implement file output operations to save results
- Test and verify script execution

## Prerequisites
- Basic understanding of Python programming
- Access to the provided Linux Host EC2 instance
- SSH client (PuTTY for Windows, terminal for macOS/Linux)

## Getting Started

### 1. Launch the Lab Environment
1. Click **Start Lab** at the top of these instructions
2. Wait for "Lab status: ready" message
3. Click the **X** to close the panel

### 2. Retrieve Connection Information
1. Click the **Details** dropdown menu above
2. Click **Show**
3. Copy the **Public IP** address and save it in a text file named `Lab Details.txt`

### 3. Connect to Linux Host

#### For Windows Users:
1. Download the PPK file from the Details panel
2. Open **PuTTY**
3. Configure your session with the public IP and PPK file
4. Connect using username: `ec2-user`
 with your instance's IP address)

## Your Challenge

### Task: Create a Prime Number Generator
Write a Python script that:

**Requirements:**
- Display all prime numbers between 1 and 250
- Store the results in a file named `results.txt`
- Test the script and verify the output

**Implementation Details:**
- Both Python 2 and 3 are available on the Linux Host
- Python 3 is recommended for this exercise
- The script should output prime numbers in a readable format

## My Solution 
I created two files, prime_numbers.py and results.txt(where I would store my results)
# prime_numbers.py

<img width="1898" height="384" alt="Screenshot 2026-03-09 233423" src="https://github.com/user-attachments/assets/34680373-b058-42d9-bbbc-6d0d7e7d56c3" />

```
with open('results.txt', 'w') as file:
    num = 2
    while num <= 250:
        is_prime = True
        i = 2
        while i < num:
            if num % i == 0:
                is_prime = False
                break
            i += 1
        
        if is_prime:
            print(num)
            file.write(str(num) + "\n")
        
        num += 1

print("Done! Check results.txt for the prime numbers.")
```
<img width="1898" height="1013" alt="Screenshot 2026-03-09 233500" src="https://github.com/user-attachments/assets/1dd226ea-3f79-4c29-ad62-652820177b61" />

<img width="1898" height="1018" alt="Screenshot 2026-03-09 233423" src="https://github.com/user-attachments/assets/54b2806e-40c8-4ca0-a996-9a3c82f508bc" />

# results.txt

<img width="1896" height="1016" alt="Screenshot 2026-03-09 233527" src="https://github.com/user-attachments/assets/f42b9e79-dd03-4f05-8aa9-c170e58c12a0" />

```
2
3
5
7
11
13
17
19
23
29
31
37
41
43
47
53
59
61
67
71
73
79
83
89
97
101
103
107
109
113
127
131
137
139
149
151
157
163
167
173
179
181
191
193
197
199
211
223
227
229
233
239
241
```

### Running Your Script

To execute my Python 3 script:

```bash
python3 prime_numbers.py
```

Made my script to be executable by running :

```
chmod u+x prime_numbers.py
```

<img width="1896" height="43" alt="Screenshot 2026-03-09 233604" src="https://github.com/user-attachments/assets/59175795-25f0-411d-a0c6-64abbc7d500e" />

----
## Tips
- A prime number is only divisible by 1 and itself
- 1 is not considered a prime number
- Test your logic with smaller ranges first
- Use a loop to check each number's divisibility
---
