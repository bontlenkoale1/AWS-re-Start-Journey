# Data Protection Using Encryption (AWS KMS Lab)🔐 
---

##  Overview 📌

In this lab, I explored **data protection using encryption** by working with **AWS Key Management Service (AWS KMS)** and the **AWS Encryption CLI**.

Cryptography is used to protect sensitive information by converting readable data (**plaintext**) into an unreadable format (**ciphertext**).
Only authorized users with the correct key can decrypt the information back to its original form.

During this lab, I connected to a **File Server hosted on an Amazon EC2 instance**, created an **AWS KMS encryption key**, installed the **AWS Encryption CLI**, and used the key to **encrypt and decrypt sensitive files**.

This lab demonstrated how AWS services can be used to secure sensitive data and maintain **confidentiality, integrity, and security**.

---

#  Objectives 🎯

After completing this lab, I was able to:

* Create an **AWS KMS encryption key**
* Install and configure the **AWS Encryption CLI**
* Encrypt plaintext files
* Decrypt ciphertext back into readable data

---
# 🧪 Lab Environment

The lab environment included:

* **1 Amazon EC2 instance** named **File Server**
* **IAM role (voclabs)** for permissions
* **AWS Systems Manager Session Manager** to connect to the EC2 instance
* **AWS KMS** for key management
* **AWS Encryption CLI** for encrypting and decrypting files

Most backend infrastructure such as EC2 instances and IAM roles were **preconfigured**.

---

# Task 1️⃣: Create an AWS KMS Key

First, I created a **symmetric encryption key** using **AWS Key Management Service (KMS)**.

Symmetric encryption uses **the same key to encrypt and decrypt data**, which makes it fast and efficient.

### Steps I followed

1. Opened the **AWS Management Console**
2. Searched for **Key Management Service (KMS)**
3. Selected **Create a key**
4. Chose:

```
Key type: Symmetric
```


<img width="1904" height="907" alt="Screenshot 2026-02-25 161858" src="https://github.com/user-attachments/assets/25a64053-0099-4d9a-a322-41e412a98f5e" />


5. Added the following labels:

```
Alias: MyKMSKey
Description: Key used to encrypt and decrypt data files
```

<img width="1906" height="917" alt="Screenshot 2026-02-25 162004" src="https://github.com/user-attachments/assets/cd1c183d-ee66-47a8-a852-75990ddf51a4" />


6. Assigned **voclabs IAM role** as:

* Key Administrator
* Key Usage Permission

7. Finished creating the key and copied the **Key ARN**.

<img width="1906" height="918" alt="Screenshot 2026-02-25 162104" src="https://github.com/user-attachments/assets/6bd07d0a-56ab-4ada-b9bb-138908a26f94" />

The **ARN (Amazon Resource Name)** identifies the key and is later used in encryption commands.

---

# Task 2️⃣: Configure the EC2 File Server

Next, I configured the **File Server EC2 instance** so it could use the AWS KMS key.

### Connecting to the instance

1. Navigated to **EC2**
2. Selected the **File Server instance**
3. Clicked **Connect**
4. Connected using **Session Manager**

<img width="1911" height="907" alt="Screenshot 2026-03-01 090001" src="https://github.com/user-attachments/assets/a2a37c8a-c161-48ea-aeaa-b25af3b111c9" />

### Configure AWS credentials

Inside the instance terminal I ran:

```bash
cd ~
aws configure
```

Then I replaced the placeholder credentials with the **AWS credentials provided in Vocareum**.

To edit the credentials file:

```bash
vi ~/.aws/credentials
```

<img width="1911" height="912" alt="Screenshot 2026-03-01 090445" src="https://github.com/user-attachments/assets/7ae5f94f-f7fc-4e6d-9376-0a045323c185" />

After updating the file, I verified the configuration using:

```bash
cat ~/.aws/credentials
```
<img width="1908" height="909" alt="Screenshot 2026-03-01 090624" src="https://github.com/user-attachments/assets/fdfacf11-492d-4ea3-8251-f9079eee29b4" />

### Install AWS Encryption CLI

Next, I installed the AWS Encryption CLI:

```bash
pip3 install aws-encryption-sdk-cli
```

<img width="1908" height="909" alt="Screenshot 2026-03-01 090624" src="https://github.com/user-attachments/assets/1a12bf20-c7e9-498a-97d1-3a8433f1474b" />

Then I updated the system path:

```bash
export PATH=$PATH:/home/ssm-user/.local/bin
```
<img width="1868" height="918" alt="Screenshot 2026-03-01 090757" src="https://github.com/user-attachments/assets/d1b0cda2-3d7f-4e3f-bb2e-06c2ec384cb5" />

This allowed me to run encryption commands from the terminal.

---

# 🔒 Task 3: Encrypt and Decrypt Data

In this task, I created **sample text files containing sensitive data** and encrypted them using the AWS KMS key.

### Create plaintext files

```bash
touch secret1.txt secret2.txt secret3.txt
echo 'TOP SECRET 1!!!' > secret1.txt
```

To view the plaintext file:

```bash
cat secret1.txt
```

Output:

```
TOP SECRET 1!!!
```

---

# 🔐 Encrypt the File

First, I stored the **KMS Key ARN** in a variable:

```bash
keyArn=(KMS ARN)
```

Then I encrypted the file using the AWS Encryption CLI:

```bash
aws-encryption-cli --encrypt \
--input secret1.txt \
--wrapping-keys key=$keyArn \
--metadata-output ~/metadata \
--encryption-context purpose=test \
--commitment-policy require-encrypt-require-decrypt \
--output ~/output/.
```

This command:

* Encrypts the plaintext file
* Uses the **KMS key**
* Stores encryption metadata
* Outputs the encrypted file

To confirm the command succeeded:

```bash
echo $?
```

If the value returned is **0**, the command was successful.

### View encrypted file

```bash
ls output
```

Result:

```
secret1.txt.encrypted
```

When I opened the encrypted file:

```bash
cat secret1.txt.encrypted
```

The contents appeared as **ciphertext**, which is unreadable without decryption.

---

# 🔓 Decrypt the File

To decrypt the encrypted file:

```bash
aws-encryption-cli --decrypt \
--input secret1.txt.encrypted \
--wrapping-keys key=$keyArn \
--commitment-policy require-encrypt-require-decrypt \
--encryption-context purpose=test \
--metadata-output ~/metadata \
--max-encrypted-data-keys 1 \
--buffer \
--output .
```

The decrypted file was created as:

```
secret1.txt.encrypted.decrypted
```

To view the decrypted contents:

```bash
cat secret1.txt.encrypted.decrypted
```

Output:

```
TOP SECRET 1!!!
```

This confirmed that the encryption and decryption process worked successfully.

---

# 🔁 How Symmetric Encryption Works

Encryption Process:

```
Plaintext → Encryption Algorithm + Key → Ciphertext
```

Decryption Process:

```
Ciphertext → Decryption Algorithm + Same Key → Plaintext
```

AWS KMS securely manages the **encryption keys** used in this process.

---

# 🏁 Conclusion

In this lab, I successfully:

✅ Created an **AWS KMS symmetric encryption key**
✅ Configured an **EC2 File Server environment**
✅ Installed the **AWS Encryption CLI**
✅ Encrypted plaintext files into ciphertext
✅ Decrypted the encrypted files back into readable data

This lab demonstrated how **AWS KMS and the AWS Encryption CLI can be used together to protect sensitive data using encryption.**

---

# 📚 AWS Services Used

* **AWS Key Management Service (KMS)** – Key creation and management
* **Amazon EC2** – File server hosting the data
* **AWS Systems Manager Session Manager** – Secure instance access
* **AWS Encryption CLI** – Encryption and decryption operations
---
