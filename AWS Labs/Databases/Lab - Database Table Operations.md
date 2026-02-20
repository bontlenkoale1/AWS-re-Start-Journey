## Database Table Operations lab 🗄️

----

## Lab Overview & Objectives 🔍

The database operations team for an organization configured a relational database instance and tasked me with practicing database and table management.
In this lab, I demonstrated common database and table operations including creating, viewing, altering and deleting databases and tables.

When I started the lab, the following resources were already created for me:

![architecture-start (3)](https://github.com/user-attachments/assets/532ed08b-1587-4208-9cec-0581ecdeeff7)

A database client is installed on an instance.

----

## Task 1️⃣: Connecting to the Command Host 🔌
I established a connection to an EC2 instance configured with a database client. The client is used to run structured query language(SQL)queries against a relational database. This instance is referred to as the ***Command Host***.
In the AWS Management Console, on the services menu. I chose **compute** and followed with clicking on the EC2.
On the EC2 dashboard, I selected **Instances**  which took me to the instances.
On the instances, theres an instance labelled **"Command Host"**,next to it theres a checkbox ✅ that I checked and above it a connect button that I clicked on.

<img width="1902" height="920" alt="Screenshot 2026-02-11 145701" src="https://github.com/user-attachments/assets/c3cdf799-5d44-449f-8577-7dcab856c0ed" />

For Connect to instance, I seleted the **Session Manager** tab followed with clicking on the **connect** button to open a terminal window


<img width="1915" height="911" alt="Screenshot 2026-02-11 150138" src="https://github.com/user-attachments/assets/4d47423a-ab43-4321-8a71-6ef2b7bd59c8" />


To configure the terminal to access all required tools and resources, run the following command:

```
sudo su
cd /home/ec2-user/
mysql -u root --password='re:St@rt!9'
```
