## Introduction To Amazon EC2 Hands-On Lab☁️

## 🔍Overview
This lab demonstrates hands-on practical experience in **launching**, **resizing**, **managing**, **configuring**, **securing**, **scaling**, **monitoring**, and applying **termination protection** to **Amazon EC2 instances**.

**Amazon Elastic Compute Cloud (EC2)** is a web service that provides resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers by allowing them to quickly provision and manage virtual servers as needed.

## What would i have learned during this lab🔬
At the end of this lab,I didnt only deploy a working web-server but also explored security,automotion and instance lifecyle management that are critical for building reliable and resilient cloud applications.


## 🏗️ Lab Architecture 

This lab architecture shows a setup that uses an EC2 virtual computer to run a simple website, protected by a firewall, in a secure AWS data center.


<img width="678" height="439" alt="lab architecture" src="https://github.com/user-attachments/assets/7c2df029-34a7-4039-831c-bebc5ed9cecf" />

----

# Lab Tasks
Task 1️⃣ : Launching EC2 Instance 
**Objective:**
In this task I was tasked with launching an Amazon EC2 Instance with *termination protection*,which will prevent me from terminating my EC2 Instance by accident.In addition,deploy my instance with a **User Data** which will allow me to deploy a simple web server.

• The first that I did was to navigate to my **AWS Management Console**, and on the search prompt that's on the navbar/navigation bar I searched for EC2 which then led me to the EC2 and clicked on the dashboard just to ensure that I was on the EC2 dashboard page,from there I clicked the *Launch Instance* yellow button.
• From the Launch Instance page, I proceeded to name my instance *Web Server* in the Names and tags panel. When you name your instance,AWS creates a key value pair. The key for this pair is ***Name*** and the value is the name you enter for your EC2 instance.
• Below the Name and tags,followed the AMI (Amazon Machine Image). An AMI provides the information required to launch an instance, which is a virtual server in the cloud. An AMI includes the following:
        • A template for the root volume for the instance(eg an Operating System or an applicaton server  with applications)
        • Launch permissions that control which AWS accounts can use the AMI to launch instances
        • A block device mapping that specifies the volumes ti attach to the instance when it is launched.
• The **Quick Start** list contains the commonly used AMIs. I located the Application and OS Images(Amazon Machine Image) panel and there under the AMI,I noticed the images listed there and decide to stick to using the Amazon Linux 2023 image which was already selected by default.
• From choosing the images, I followed with choosing an instance type,I selected t3.micro instance which has 2 virtual CPU and 1 GIB of memory from the dropdown. Instance types comprise varying combinations of CPU, memory, networking capacity and give you the flexibility to choose the appropriate resources for your applications. Each instance type includes one or more *instance sizes* so that you can scale your resources to the requirements of your target workload.
• I then configured a key pair in the (login) key pair panel and selected **proceed without a key pair**
• following with configuring the network settings,the VPC indicates which virtual private cloud you want to launch the instance into. You can have multiple VPCs including different ones for development, testing, and production.In the Network settings panel,I clicked on the edit button.
• In the VPC - required dropdown,I selected Lab VPC. configured security group as followed:
          • Security group name - required: Web Server security group
          • Description - required: security group for my web server
• A security group is a set of firewall rules that control the traffic for your instance. When you launch an instance,you associate one or more security groups with the instance. You add rules to each security group that allows traffic to or from its associated instances. You can modify the rules for security groups at any time, the new rules are automatically applied to all instances that are associated with the security group.
• Under the Inbound security groups rules I selected the Remove button as I wont be using SSH  to login my instance. Removing SSH access will improve the security of the instance.
• I followed by adding storage,Amazon EC2 stores data on a network-attached virtual disk called Amazon EBS. I launched the EC2 instance using the default 8 GIB disk volume.
• In the configuring advanced details,I expanded it and selected the dropdown for the Termination protection and chose **Enable**. I proceeded with coping and pasting the commands below into the **User Data**
<img width="1469" height="195" alt="User Data Script" src="https://github.com/user-attachments/assets/f8171672-86f2-4bfd-9e67-0564e555b022" />
