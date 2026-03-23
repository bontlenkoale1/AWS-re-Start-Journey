# AWS Lambda Exercise (Challenge)

## Overview
This lab demonstrates how to create an **AWS Lambda function** that counts the number of words in a text file uploaded to an **Amazon S3** bucket. The resulting word count is sent via **Amazon SNS** to an email address.

---

## AWS Services Used
- **AWS Lambda** (Compute) – Executes the word count function automatically.  
- **Amazon S3** (Storage) – Stores text files and triggers Lambda on upload.  
- **Amazon SNS** (Messaging) – Sends the word count result via email.  
- **Amazon CloudWatch** – Logs Lambda execution for monitoring and debugging.  

---

## Objectives
By completing this lab, I was able to:  
1. Create a Lambda function in Python to count words in a text file.  
2. Configure an S3 bucket to automatically trigger the Lambda function.  
3. Create an SNS topic to send the word count result via email.  
4. Test the Lambda function using sample text files.  

---

## Steps Performed

### 1. Created an SNS Topic
- Topic name: `WordCountTopic`  
- Subscribed an email address to receive notifications.  

<img width="1911" height="716" alt="SNS Topic Creation" src="https://github.com/user-attachments/assets/48562b89-952e-4371-91e2-403e93366cae" />

- Confirmed successful creation and subscription:

<img width="1512" height="425" alt="SNS Topic Created" src="https://github.com/user-attachments/assets/5bb4e795-f0af-4ceb-954e-16be55f09f89" />
<img width="1497" height="446" alt="SNS Subscription Confirmed" src="https://github.com/user-attachments/assets/a9ad560b-7938-43a4-aa15-90cff98fc519" />

---

### 2. Created a Lambda Function
- Function name: `WordCountLambda`  
- Runtime: Python 3.11  
- Role: `LambdaAccessRole` (predefined with required permissions)  
- Function reads uploaded S3 files, counts words, and sends results to the SNS topic.  

<img width="1909" height="642" alt="Lambda Function Code" src="https://github.com/user-attachments/assets/96ddc12c-3be7-49e8-8ff4-aef390b2e0ce" />

---

### 3. Created an S3 Bucket
- Bucket name: `wordcount-lab-bucket-bridgette`  
- Enabled **Lambda trigger for all object create events**.  

<img width="1832" height="655" alt="S3 Bucket Setup" src="https://github.com/user-attachments/assets/94a218e1-5f6d-4b94-8574-3e6ba5350535" />

---

### 4. Uploaded Test Files
- Sample file: `sample.txt`  
- Lambda counted the words and sent an email with the result.  

<img width="1487" height="361" alt="SNS Email Output" src="https://github.com/user-attachments/assets/5e8bfbaa-8d70-472f-9f7d-5cc7f5e6d00b" />

---

## Sample Email Output
