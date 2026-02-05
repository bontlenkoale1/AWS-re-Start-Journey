## Freshly_Ground_Static_Website  🕸️🌐
---
## Overview 🔍
Frshly_Ground is a local cafe that is loved by coffee enthusiats and book lovers. A chilling spot,that combines both nature and knowledge.  
The Cafe relied on outdated on-premises systems and limited digital infrastructure thus making running the cafe's manual operations slow, 
and the system would shutdown and leading to less exposure due to their website not reaching the right audience and less customer engagement.
They also had no reliable system for data backup and recovery.In a modern, digital-first world, this made it difficult to grow, scale, and 
compete with other cafes that already had strong online platforms. Due to their on-premises problems,they had a lot of downtime,inefficient daily operations and would often lose data. 

---

## Migration Objectives 🎯

**Migrate IT infrastructure to AWS to:**

• ✅ Enhance operational efficiency

• ✅ Improve customer engagement through a modern digital presence

• ✅ Modernize and secure IT systems

• ✅ Enable seamless scalability

• ✅ Reduce long-term operational costs

• ✅ Ensure high availability and disaster recovery

• ✅ Support future business growth and innovation


## Proposed Solution: AWS Migration 💡

# 1. Cloud Infrastructure Migration ☁️
Move from on-premises to a full AWS cloud environment, leveraging AWS’s scalability, reliability, security, and global infrastructure.

# 2. Online Presence Enhancement 🌐
 
**Develop and host a static website on Amazon S3 to:**

• Showcase the café’s menu, pricing, and story

• Provide contact information and location details

• Improve brand visibility and customer accessibility

• Lay the foundation for future e-commerce capabilities

----

## AWS Cloud Architecture 🏗️


<img width="515" height="525" alt="freshlyground (2)" src="https://github.com/user-attachments/assets/b8dd3eb0-371a-474c-9ca6-166973c4c63c" />



<img width="1227" height="688" alt="freshlyground" src="https://github.com/user-attachments/assets/2c79f896-630e-4cf4-a520-a7dc33cdf480" />


----

##  Static Amazon S3 Website 🌐

## Café Name 🏷️ 

FreshlyGround Café

![create bucket](https://github.com/user-attachments/assets/4037f45b-c669-4294-aac8-e809708f7cb6)

![WhatsApp Image 2026-02-05 at 11 28 40](https://github.com/user-attachments/assets/191f1974-f92d-48dc-900b-a4a7a93c0264)



![WhatsApp Image 2026-02-05 at 11 28 40](https://github.com/user-attachments/assets/fd54d5b6-bd84-4446-8a3a-ddea4ba1ad9a)

uploaded necessary files for the website

![files in objects](https://github.com/user-attachments/assets/8021f948-3795-4492-84a2-2dbbd1505653)



## How to Deploy the S3 Website 🛠️ 

**Create an S3 bucket named freshlyground-cafe-website**

• Enable Static Website Hosting in bucket properties

• Upload all files from s3-website/ to the bucket

• Set bucket policy to allow public read access

• Access the site via the S3 website endpoint or link a custom domain

----

## Successful Hosting 🌐📱
https://s3.eu-north-1.amazonaws.com/freshlyground.cafe-static-sitee/index.html

<img width="1916" height="958" alt="Screenshot 2026-02-05 161549" src="https://github.com/user-attachments/assets/6e485e88-4cfc-457f-9123-0085b209ac29" />


<img width="1919" height="976" alt="Screenshot 2026-02-05 162205" src="https://github.com/user-attachments/assets/8d355f5d-1cfa-40c4-a613-c9212a8216fb" />


<img width="1919" height="958" alt="Screenshot 2026-02-05 161625" src="https://github.com/user-attachments/assets/04aafa4a-e32a-49d9-ab0d-44393ca09ffa" />



