## Introduction to Amazon EC2 Hands-On Lab ☁️

## 🔍 Overview
This lab demonstrates hands-on practical experience in **launching**, **resizing**, **managing**, **configuring**, **securing**, **scaling**, **monitoring**, and applying **termination protection** to **Amazon EC2 instances**.

**Amazon Elastic Compute Cloud (EC2)** is a web service that provides resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers by allowing them to quickly provision and manage virtual servers as needed.

## 🔬 What I Learned During This Lab
At the end of this lab, I not only deployed a working web-server but also explored **security**, **automation**, and **instance lifecycle management**,critical aspects for building reliable and resilient cloud applications.

## 🏗️ Lab Architecture
This lab architecture shows a setup that uses an EC2 virtual computer to run a simple website, protected by a firewall, in a secure AWS data center.

<img width="678" height="439" alt="Lab Architecture" src="https://github.com/user-attachments/assets/7c2df029-34a7-4039-831c-bebc5ed9cecf" />

---

## 🛠️ Lab Tasks

### Task 1️⃣: Launching an EC2 Instance  
**Objective:**  
Launch an Amazon EC2 instance with *termination protection* to prevent accidental termination, and deploy it with **User Data** to run a simple web server.

- Navigated to the **AWS Management Console**, searched for **EC2** in the navigation bar, and accessed the EC2 dashboard. Clicked the ***Launch Instance*** yellow button.
- Named the instance ***Web Server*** in the *Name and tags* panel. AWS automatically creates a key-value pair with the key `Name` and the entered value.
- In the *Application and OS Images (Amazon Machine Image)* panel, selected the default **Amazon Linux 2023 AMI** from the *Quick Start* list.
  - An AMI provides the template for the instance’s root volume, launch permissions, and block device mapping.
- Chose the **t3.micro** instance type (2 vCPUs, 1 GiB memory) from the dropdown.
- Configured the key pair in the *Key pair (login)* panel and selected **Proceed without a key pair**.
- Edited *Network settings*:
  - Selected **Lab VPC** from the *VPC* dropdown.
  - Configured security group:
    - **Security group name:** *Web Server security group*
    - **Description:** *Security group for my web server*
  - Removed the default SSH inbound rule to improve instance security.
- Added storage using the default **8 GiB Amazon EBS** volume.
- In *Advanced details*:
  - Enabled **Termination protection** from the dropdown.
  - Copied and pasted the following script into **User Data**:

<img width="1469" height="195" alt="User Data Script" src="https://github.com/user-attachments/assets/f8171672-86f2-4bfd-9e67-0564e555b022" />



