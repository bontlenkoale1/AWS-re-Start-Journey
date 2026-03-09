# Preparing to Analyze Insulin with Python 🐍

## Lab Overview 🎯

In information technology, Python works well as the programming language of choice for manipulating strings, sequences, and numbers. Python is especially preferred in scientific computing applications such as physics, chemistry, and biology.

In this lab, I will perform simple sequence manipulations and calculations on human insulin, which is a well-known hormone in the human body that is responsible for regulating sugars.

**In this lab, I will:**
- Retrieve the protein sequence of human insulin from human preproinsulin

---

## Setting Up My Lab Environment ⚙️

### Accessing AWS Cloud9 IDE

1. Started my lab environment by choosing **Start Lab** at the top of the instructions
2. Waited for the message "Lab status: ready" and closed the panel
3. Chose **AWS** at the top of the instructions to open the AWS Management Console
4. Navigated to **Services > Cloud9**
5. Located the **reStart-python-cloud9** card and chose **Open IDE**


<img width="1908" height="913" alt="Screenshot 2026-03-04 095710" src="https://github.com/user-attachments/assets/f3459c97-df44-4a02-a5a1-0ae950439e01" />

### Creating My Python Exercise File

1. From the menu bar: **File > New From Template > Python File**
2. Deleted the sample code from the template file
3. Saved the file as: **File > Save As...** → `analyze-insulin.py` in `/home/ec2-user/environment`

### Opening a Terminal Session

1. Chose the **+** icon and selected **New Terminal**
2. Ran `pwd` to confirm I was in `/home/ec2-user/environment`

<img width="1905" height="902" alt="Screenshot 2026-03-04 100335" src="https://github.com/user-attachments/assets/fda9a798-6584-4d87-9037-78b9f6fbce37" />

---

## Exercise 1️⃣: Retrieving the Protein Sequence of Human Preproinsulin

<img width="1892" height="910" alt="Screenshot 2026-03-04 132216" src="https://github.com/user-attachments/assets/e3bebac7-9ee5-4993-9fb6-48e3f0445a83" />

### Step 1: Access NCBI

I accessed the National Center for Biotechnology Information (NCBI) at: https://ncbi.nlm.nih.gov

### Step 2: Search for Human Insulin

- Selected **Protein** from the dropdown menu next to the search bar
- Entered **"human insulin"** and chose **Search**
- Selected the result: **insulin [Homo sapiens]**

<img width="1484" height="538" alt="Screenshot 2026-03-04 132506" src="https://github.com/user-attachments/assets/69c01abc-a3bb-4bf1-b364-d41891d0f01f" />

### Step 3: Copy the Sequence

At the bottom of the search record, I copied the insulin sequence (from ORIGIN to //):

```
ORIGIN      
        1 malwmrllpl lallalwgpd paaafvnqhl cgshlvealy lvcgergffy tpktrreaed
       61 lqvgqvelgg gpgagslqpl alegslqkrg iveqcctsic slyqlenycn
//
```
<img width="1482" height="131" alt="Screenshot 2026-03-04 132652" src="https://github.com/user-attachments/assets/1c9c6914-5773-4cd1-805a-b0de9e8c9685" />

### Step 4: Save the Raw Sequence

In AWS Cloud9:
- **File > New File**
- Saved as: `preproinsulin-seq.txt`
- Pasted the sequence into the file

<img width="1904" height="908" alt="Screenshot 2026-03-04 135108" src="https://github.com/user-attachments/assets/d1066f7d-524e-4037-90a3-852ec120e505" />

### Bonus: Cleaning Programmatically with Regex

*Note to self: I could clean this file programmatically using regex to remove ORIGIN, numbers, //, spaces, and line breaks. After cleaning, I should confirm the file has exactly 110 characters.*

<img width="1904" height="918" alt="Screenshot 2026-03-04 135050" src="https://github.com/user-attachments/assets/99c2c3b1-69e2-43b5-bd02-89bdf94c2b7a" />

---

## Exercise 2️⃣: Obtaining the Protein Sequence of Human Insulin

*Background: Preproinsulin contains a 24aa signal sequence and an 86aa proinsulin molecule. Amino acids 25–54 and amino acids 90–110 are the processed insulin molecule.*

### File 1: Clean Preproinsulin Sequence

| Task | Details |
|------|---------|
| **File Name** | `preproinsulin-seq-clean.txt` |
| **Action** | Delete ORIGIN, numbers, //, spaces, and return carriages |
| **Verification** | Must contain 110 characters of lowercase letters |

**My Cleaned Sequence:**
```
malwmrllpllallalwgpdpaaafvnqhlcgshlvealylvcgergffytpktrreaedlqvgqvelgggpgagslqplalegslqkrgiveqcctsicslyqlenycn
```

<img width="1905" height="912" alt="Screenshot 2026-03-04 140133" src="https://github.com/user-attachments/assets/184c63f6-007e-4c00-b7db-f02671ff3782" />

**Character Count:** 110 ✓

---

### File 2: Insulin Signal Sequence (Amino Acids 1–24)

| Task | Details |
|------|---------|
| **File Name** | `lsinsulin-seq-clean.txt` |
| **Amino Acids** | 1–24 |
| **Verification** | Must contain 24 characters |
<img width="1901" height="909" alt="Screenshot 2026-03-09 165417" src="https://github.com/user-attachments/assets/eb956f2e-32a0-45ee-883e-7f305c2bafd6" />

**My Sequence:**
```
malwmrllpllallalwgpdpaaa
```
<img width="1905" height="906" alt="Screenshot 2026-03-04 142515" src="https://github.com/user-attachments/assets/8f9d5f61-73fb-4f2d-ab3f-eded62fbecf7" />

**Character Count:** 24 ✓

---

### File 3: Insulin B Chain (Amino Acids 25–54)

| Task | Details |
|------|---------|
| **File Name** | `binsulin-seq-clean.txt` |
| **Amino Acids** | 25–54 |
| **Verification** | Must contain 30 characters |
<img width="1902" height="906" alt="Screenshot 2026-03-04 144146" src="https://github.com/user-attachments/assets/04252b98-49cc-47e1-b999-73cf3284a0ee" />

**My Sequence:**
```
fvnqhlcgshlvealylvcgergffytpkt
```
<img width="1909" height="904" alt="Screenshot 2026-03-09 165816" src="https://github.com/user-attachments/assets/b8d44f4f-319c-4d98-b268-15367ee311a9" />


**Character Count:** 30 ✓

---

### File 4: Insulin C Peptide (Amino Acids 55–89)

| Task | Details |
|------|---------|
| **File Name** | `cinsulin-seq-clean.txt` |
| **Amino Acids** | 55–89 |
| **Verification** | Must contain 35 characters |

**My Sequence:**
```
rreaedlqvgqvelgggpgagslqplalegslqkr
```
<img width="1901" height="906" alt="Screenshot 2026-03-09 170436" src="https://github.com/user-attachments/assets/f4dd51aa-b0a0-4a77-aa31-af59d0093cd0" />


**Character Count:** 35 ✓

---

### File 5: Insulin A Chain (Amino Acids 90–110)

| Task | Details |
|------|---------|
| **File Name** | `ainsulin-seq-clean.txt` |
| **Amino Acids** | 90–110 |
| **Verification** | Must contain 21 characters |

**My Sequence:**
```
giveqcctsicslyqlenycn
```

**Character Count:** 21 ✓

<img width="1900" height="909" alt="Screenshot 2026-03-04 144244" src="https://github.com/user-attachments/assets/45bbcea3-181a-41d6-9db0-2ede8af68c76" />

---

## Summary of Files Created

| File Name | Description | Character Count |
|-----------|-------------|-----------------|
| `analyze-insulin.py` | Python file for future analysis | N/A |
| `preproinsulin-seq.txt` | Raw sequence from NCBI | ~110 + formatting |
| `preproinsulin-seq-clean.txt` | Cleaned full sequence | 110 |
| `lsinsulin-seq-clean.txt` | Signal sequence (aa 1-24) | 24 |
| `binsulin-seq-clean.txt` | B chain (aa 25-54) | 30 |
| `cinsulin-seq-clean.txt` | C peptide (aa 55-89) | 35 |
| `ainsulin-seq-clean.txt` | A chain (aa 90-110) | 21 |

---

## Reflection: Automation vs. Manual Work

> *"Deciding when to automate and when to work manually is a dilemma for computer programmers. Too much automation wastes time on coding, whereas too little restricts the scope of your program."*

For this lab, I chose to work **manually** because:
- It was a one-time task with only one file
- Setting up automation would have taken longer than manual cleaning
- The manual process helped me understand the insulin structure better

**However**, if I needed to download and process thousands of protein sequences, automation would be essential!

---


*Happy Coding with Python!* 🐍
