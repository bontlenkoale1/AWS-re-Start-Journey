# Build Your DB Server and Interact With Your DB Using an App 🚀

---

## Lab Overview & Objectives 🎯

This lab is designed to reinforce the concept of leveraging an AWS-managed database instance for solving relational database needs using **Amazon Relational Database Service (Amazon RDS)**. Amazon RDS makes it easy to set up, operate, and scale a relational database in the cloud while managing time-consuming database administration tasks, allowing you to focus on your applications and business.

When I started the lab, the following resources were already created for me:
I started with the following infrastructure:

![architecture-lab1 (1)](https://github.com/user-attachments/assets/cf459a04-ec8d-4349-9f5c-c45e45094db7)


*A web server was already deployed in a public subnet, waiting to be connected to a database.*

Amazon RDS provides six familiar database engines to choose from:
- Amazon Aurora
- Oracle
- Microsoft SQL Server
- PostgreSQL
- MySQL
- MariaDB

---

## Task 1️⃣: Create a Security Group for the RDS DB Instance 🔒

In this task, I created a security group to allow the web server to access the RDS DB instance. The security group will be used when launching the database instance.

In the AWS Management Console, I selected the **Services** menu and then selected **VPC** under **Networking & Content Delivery**.

In the left navigation pane, I clicked **Security Groups** and then clicked **Create security group**.

I configured the following:

- **Security group name:** `DB Security Group`
- **Description:** `Permit access from Web Security Group`
- **VPC:** `Lab VPC`

In the **Inbound rules** section, I clicked **Add rule** and configured:

- **Type:** `MySQL/Aurora (3306)`
- **Source:** Typed `sg` in the search field and selected **Web Security Group**

This configures the Database security group to permit inbound traffic on port 3306 from any EC2 instance that is associated with the Web Security Group.

I scrolled to the bottom of the screen and clicked **Create security group**.


<img width="1910" height="914" alt="Screenshot 2026-02-15 220157" src="https://github.com/user-attachments/assets/c6639de5-2436-456a-ba8a-154d3ce4d79a" />

<img width="1917" height="915" alt="Screenshot 2026-02-15 220236" src="https://github.com/user-attachments/assets/9eda7bb8-4f42-4221-a219-5cd1eed5d19d" />


---

## Task 2️⃣: Create a DB Subnet Group 🌐

In this task, I created a DB subnet group that tells RDS which subnets can be used for the database. Each DB subnet group requires subnets in at least two Availability Zones.

In the AWS Management Console, I selected the **Services** menu and then selected **RDS** under Database.

In the left navigation pane, I clicked **Subnet groups**. (If the navigation pane was not visible, I clicked the ☰ menu icon.)

I clicked **Create DB Subnet Group** and configured:

- **Name:** `DB Subnet Group`
- **Description:** `DB Subnet Group`
- **VPC ID:** `Lab VPC`

In the **Add subnets** section for **Availability zones**, I clicked the dropdown and:
- Selected the first Availability zone
- Selected the second Availability zone

For **Subnets**, I clicked the dropdown and:
- For the first Availability zone, selected `10.0.1.0/24`
- For the second Availability zone, selected `10.0.3.0/24`

I clicked **Create**.

This adds Private Subnet 1 (10.0.1.0/24) and Private Subnet 2 (10.0.3.0/24).

<img width="1911" height="669" alt="Screenshot 2026-02-15 220831" src="https://github.com/user-attachments/assets/438ffb63-d773-4b0f-a683-faf21bb0fb9d" />

<img width="1914" height="917" alt="Screenshot 2026-02-15 220850" src="https://github.com/user-attachments/assets/d507051f-eea8-41b1-8276-facb5782e0a3" />

<img width="1919" height="911" alt="Screenshot 2026-02-15 220931" src="https://github.com/user-attachments/assets/4df68061-6b9d-4a6f-8c76-dec1971e4637" />

---

## Task 3️⃣: Create an Amazon RDS DB Instance 🗄️

In this task, I configured and launched a Multi-AZ Amazon RDS for MySQL database instance.

Amazon RDS Multi-AZ deployments provide enhanced availability and durability for Database (DB) instances, making them a natural fit for production database workloads. When you provision a Multi-AZ DB instance, Amazon RDS automatically creates a primary DB instance and synchronously replicates the data to a standby instance in a different Availability Zone (AZ).

In the left navigation pane, I clicked **Databases** and then clicked **Create database**.

I chose **Standard create** and configured the following:

**Engine options:**
- **Engine type:** `MySQL`
- **Engine version:** Latest version

<img width="1919" height="912" alt="Screenshot 2026-02-15 223406" src="https://github.com/user-attachments/assets/912f6d74-02ef-40f8-8fe8-ccc62f41e16e" />

**Templates:** `Dev/Test`

**Availability and durability:** `Multi-AZ DB Instance`

<img width="1908" height="908" alt="Screenshot 2026-02-15 223425" src="https://github.com/user-attachments/assets/c37ee240-10c0-423e-a651-889170c125af" />

**Settings:**
- **DB instance identifier:** `lab-db`
- **Master username:** `main`
- **Master password:** `lab-password`
- **Confirm password:** `lab-password`


<img width="1919" height="905" alt="Screenshot 2026-02-15 223443" src="https://github.com/user-attachments/assets/470c3638-1373-4b33-b998-8ab4d445eb4f" />


**Instance configuration:**
- Selected **Burstable classes (includes t classes)**
- Selected `db.t3.medium`

**Storage:**
- Selected **General Purpose (SSD)**


<img width="1912" height="911" alt="Screenshot 2026-02-15 223503" src="https://github.com/user-attachments/assets/5d840f36-0f10-4c56-bac1-03d44dfeb515" />



**Connectivity:**
- **Virtual Private Cloud (VPC):** `Lab VPC`
- **VPC security group:** Selected **Choose existing**
- Under **Existing VPC security groups**, used **X** to remove **default**
- Selected **DB Security Group**


<img width="1915" height="914" alt="Screenshot 2026-02-15 223532" src="https://github.com/user-attachments/assets/49ee6121-c0b2-40ba-b21f-f44356d1abfd" />

<img width="1911" height="918" alt="Screenshot 2026-02-15 223556" src="https://github.com/user-attachments/assets/412f14b5-6105-403d-afe4-0430c725549c" />

**Monitoring:**
- Expanded **Additional configuration** and unchecked **Enable Enhanced monitoring**

**Additional configuration (expanded):**
- **Initial database name:** `lab`
- **Backup:** Unchecked **Enable automated backups** (this turns off backups for faster deployment)

<img width="1917" height="909" alt="Screenshot 2026-02-15 223700" src="https://github.com/user-attachments/assets/9ab4552e-09e7-48d5-8836-15686fd1f20e" />

<img width="1919" height="918" alt="Screenshot 2026-02-15 223617" src="https://github.com/user-attachments/assets/be786e07-e1df-461a-9ffd-b6c1a0b7db7c" />


I scrolled to the bottom of the screen and clicked **Create database**.

I clicked on **lab-db** (the link itself).


I waited approximately **4 minutes** for the database to become available. The deployment process deploys a database in two different Availability zones.

While waiting, the status shows as **Creating** then changes to **Modifying** or **Available**.

Once available, I scrolled down to the **Connectivity & Security** section and copied the **Endpoint** field:

<img width="1906" height="915" alt="Screenshot 2026-02-15 224311" src="https://github.com/user-attachments/assets/c42c7d48-0240-4acb-bd92-3f34c1025c24" />

```
lab-db.cggq8lhnxvnv.us-west-2.rds.amazonaws.com
```

I pasted the Endpoint value into a text editor for later use.

---

## Task 4️⃣: Interact With Your Database 💻

In this task, I opened a web application running on the web server and configured it to use the database.

I copied the **WebServer IP address** from the **AWS Details** section above the instructions.

I opened a new web browser tab, pasted the WebServer IP address, and pressed **Enter**.

The web application was displayed, showing information about the EC2 instance. At the top of the web application page, I clicked the **RDS** link.

I then configured the application to connect to the database:

- **Endpoint:** Pasted the Endpoint I copied to a text editor
- **Database:** `lab`
- **Username:** `main`
- **Password:** `lab-password`

<img width="1919" height="961" alt="Screenshot 2026-02-15 224933" src="https://github.com/user-attachments/assets/f8804ab6-65d1-4afb-8175-22f6fc26c283" />



I clicked **Submit**.

A message appeared explaining that the application was running a command to copy information to the database. After a few seconds, the application displayed an **Address Book**.

The Address Book application uses the RDS database to store information.

I tested the web application by **adding**, **editing**, and **removing** contacts.

The data persists to the database and automatically replicates to the second Availability Zone.

---

At the end of this lab, I would have completed building and interacting with a highly available database server:

*A lab user launches an Amazon RDS DB instance with high availability, configures it to permit connections from the web server, opens a web application and interacts with the database.*



![architecture-lab2 (1)](https://github.com/user-attachments/assets/4de065e8-08c4-4ff4-a952-691b3b3ef79f)


---

## Key Takeaways 💡

### Amazon RDS Concepts Mastered:

| Concept | Purpose | Benefit |
|---------|---------|---------|
| **Multi-AZ Deployment** | Primary + standby DB in different AZs | High availability and automatic failover |
| **DB Subnet Groups** | Specifies subnets across multiple AZs | Network isolation and redundancy |
| **Security Groups** | Acts as virtual firewall | Granular access control |
| **RDS Endpoint** | Connection address for applications | Simplified connection management |

### Benefits of Amazon RDS:
| Benefit | Description |
|---------|-------------|
| **Managed Service** | No hardware provisioning, patching, or backups to manage |
| **High Availability** | Automatic failover to standby instance |
| **Scalability** | Easy to scale compute and storage resources |
| **Security** | Network isolation and controlled access |

---

## Important Notes ⚠️

- **Backups:** Automated backups were disabled for faster lab deployment; this is not recommended for production environments
- **Multi-AZ:** Provides enhanced availability but at additional cost
- **Security:** Database is in private subnets, accessible only through the web server
- **Credentials:** Store database credentials securely; never hardcode in applications

---

## Conclusion 🎉

Successfully built and interacted with a highly available database server using Amazon RDS:

- ✅ Created security groups for database access control
- ✅ Configured DB subnet groups across multiple Availability Zones
- ✅ Launched a Multi-AZ MySQL RDS instance
- ✅ Connected a web application to the database
- ✅ Verified data persistence and replication

---

## Additional Resources 📚

- [Amazon RDS Documentation](https://docs.aws.amazon.com/rds/)
- [Amazon RDS FAQs](https://aws.amazon.com/rds/faqs/)
- [Multi-AZ Deployments](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)
- [Security Groups for RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html)
- [DB Subnet Groups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.SubnetGroup)

---
