# Introduction to Amazon Aurora 🚀

---

## Lab Overview & Objectives 🎯

This lab introduces me to Amazon Aurora and provides a basic understanding of how to use Aurora. I followed the steps to create an Aurora instance and then connected to it.

When I started the lab, the following resources were already created for me:

*A VPC with public and private subnets, a DB subnet group, a security group, and an EC2 instance (Command Host) with a database client were already provisioned using AWS CloudFormation.*

---

### Topics Covered:
After completing this lab, I am able to:
- ✅ Create an Aurora instance
- ✅ Connect to a pre-created Amazon EC2 instance
- ✅ Configure the Amazon EC2 instance to connect to Aurora
- ✅ Query the Aurora instance

---

### Technologies Used:
| Service | Description |
|---------|-------------|
| **Amazon Aurora** | A fully managed, MySQL-compatible, relational database engine that combines the performance and reliability of high-end commercial databases with the simplicity and cost-effectiveness of open-source databases. It delivers up to five times the performance of MySQL. |
| **Amazon EC2** | A web service that provides resizable compute capacity in the cloud, reducing the time required to provision new server instances to minutes. |
| **Amazon RDS** | Makes it easy to set up, operate, and scale a relational database in the cloud while managing time-consuming database administration tasks. |

---

## Prerequisites 📋

To successfully complete this lab, I needed:
- Some experience using the Linux operating system
- A basic understanding of structured query language (SQL)

---

## Task 1️⃣: Create an Aurora Instance 🗄️

In this task, I created an Aurora database (DB) instance.

At the top of the AWS Management Console, in the search bar, I searched for and chose **RDS**.

In the left navigation menu, I chose **Databases** and then chose **Create database**.

I configured the following options:

**Choose a database creation method:** `Standard create`

**Engine type:** `Aurora (MySQL Compatible)`

**Engine version:** The version specified as the default for major version 8.0

**Templates:** `Dev/Test`

**Settings:**
- **DB cluster identifier:** `aurora`
- **Master username:** `admin`
- **Master password:** `admin123`
- **Confirm password:** `admin123`

**Instance configuration:**
- **DB instance class:** `Burstable classes (includes t classes)`
- Selected `db.t3.medium` from the dropdown list

**Availability & durability:**
- **Multi-AZ deployment:** `Don't create an Aurora Replica`
  - *Note: Amazon RDS Multi-AZ deployments provide enhanced availability for production workloads. Since this is a lab environment, Multi-AZ deployment was not needed.*

**Connectivity:**
- **Virtual private cloud (VPC):** `LabVPC`
- **Subnet group:** `dbsubnetgroup` (created by CloudFormation)
- **Public access:** `No`
- **VPC security group:** `Choose existing`
- **Existing VPC security groups:** Removed the **default** security group
- From the dropdown list, chose **DBSecurityGroup**

**Monitoring:**
- Cleared the check box for **Enable Enhanced monitoring**

**Additional configuration (expanded):**
- **Initial database name:** `world`

**Encryption:**
- Cleared the check box for **Enable encryption**

**Maintenance:**
- Cleared the check box for **Enable auto minor version upgrade**

I scrolled to the bottom and chose **Create database**.

> **Note:** My Aurora DB instance was in the process of launching and took up to 5 minutes to launch. However, I continued to the next task.

Once the database completed creating, I saw a notification message:
```
Successfully created database aurora.
```

✅ **Task complete:** I have successfully created an Aurora instance.

---

## Task 2️⃣: Connect to an Amazon EC2 Linux Instance 🔌

In this task, I logged into the Amazon EC2 Linux instance that was launched for me when I started the lab using CloudFormation.

At the top of the AWS Management Console, in the search bar, I searched for and chose **EC2**.

In the left navigation menu, I chose **Instances**.

Next to the instance labelled **Command Host**, I selected the check box and then chose **Connect**.

For **Connect to instance**, I chose **Session Manager**.

I chose **Connect** to open a terminal window.

✅ **Task complete:** I have successfully connected to the Amazon EC2 instance named Command Host.

---

## Task 3️⃣: Configure the Amazon EC2 Linux Instance to Connect to Aurora 🔧

In this task, I used the **yum** package manager to install the MariaDB client and then configured the Amazon EC2 Linux instance to connect to the Aurora database.

**Command:** To install the MariaDB client, I ran the following command:

```bash
sudo yum install mariadb -y
```

The MariaDB client is what I used in later steps to connect to the Aurora instance.

Using a different browser tab, I went back to the AWS Management Console and in the search bar, searched for and chose **RDS**.

In the left navigation pane, I chose **Databases**.

I waited for **aurora-instance-1** to display **Available**.

I chose **aurora** and then the **Connectivity & security** tab. In the **Endpoints** section, I copied the **Endpoint name** for the **Writer** instance to my text editor.

The endpoint looked similar to:
```
aurora.cluster-cabcdefghijklm.us-west-2.rds.amazonaws.com
```

### Understanding Aurora Endpoints:

| Endpoint Type | Description | Use Case |
|---------------|-------------|----------|
| **Cluster Endpoint** | Connects to the current primary DB instance | All write operations (INSERT, UPDATE, DELETE) and DDL changes. Also works for reads. Provides failover support. |
| **Reader Endpoint** | Connects to one of the available Aurora replicas | Read-only operations (queries). Provides load-balancing among replicas. |

**Example formats:**
- Cluster endpoint: `mydbcluster.cluster-123456789012.us-west-2.rds.amazonaws.com:3306`
- Reader endpoint: `mydbcluster.cluster-ro-123456789012.us-west-2.rds.amazonaws.com:3306`

Next, I logged into the database.

**Copy edit:** In the following command, I replaced `<endpoint_goes_here>` with the endpoint I copied to my text editor:

```bash
mysql -u admin --password='admin123' -h <endpoint_goes_here>
```

My command looked similar to:
```bash
mysql -u admin --password='admin123' -h mydbcluster.cluster-123456789012.us-west-2.rds.amazonaws.com
```

### MySQL Command-Line Client Switches:
| Switch | Description |
|--------|-------------|
| `-u` or `--user` | The MySQL username used to connect to a database instance |
| `-p` or `--password` | The MySQL password used to connect to a database instance |
| `-h` or `--host` | The host address of the database engine |

Once the command was updated, I copied it to my clipboard and returned to the Session Manager browser tab to run it.

✅ **Task complete:** I have successfully configured the Amazon EC2 Linux instance to connect to Aurora.

---

## Task 4️⃣: Create a Table and Insert and Query Records 📊

In this task, I learned how to create a table in a database, load data, and run a query.

**Command:** To list the available databases, I ran the following command:

```sql
SHOW DATABASES;
```

**Expected output:**
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| world              |
+--------------------+
5 rows in set (0.02 sec)
```

**Command:** To switch to the **world** database that I created in Task 1, I ran:

```sql
USE world;
```

**Expected output:**
```
Database changed
MySQL [world]>
```

**Command:** To create a new table named **country** in the world database, I ran:

```sql
CREATE TABLE `country` (
`Code` CHAR(3) NOT NULL DEFAULT '',
`Name` CHAR(52) NOT NULL DEFAULT '',
`Continent` enum('Asia','Europe','North America','Africa','Oceania','Antarctica','South America') NOT NULL DEFAULT 'Asia',
`Region` CHAR(26) NOT NULL DEFAULT '',
`SurfaceArea` FLOAT(10,2) NOT NULL DEFAULT '0.00',
`IndepYear` SMALLINT(6) DEFAULT NULL,
`Population` INT(11) NOT NULL DEFAULT '0',
`LifeExpectancy` FLOAT(3,1) DEFAULT NULL,
`GNP` FLOAT(10,2) DEFAULT NULL,
`GNPOld` FLOAT(10,2) DEFAULT NULL,
`LocalName` CHAR(45) NOT NULL DEFAULT '',
`GovernmentForm` CHAR(45) NOT NULL DEFAULT '',
`Capital` INT(11) DEFAULT NULL,
`Code2` CHAR(2) NOT NULL DEFAULT '',
PRIMARY KEY (`Code`)
);
```

**Expected output:**
```
Query OK, 0 rows affected, 7 warnings (0.02 sec)
```

**Command:** To insert new records into the country table, I ran the following commands:

```sql
INSERT INTO `country` VALUES ('GAB','Gabon','Africa','Central Africa',267668.00,1960,1226000,50.1,5493.00,5279.00,'Le Gabon','Republic',902,'GA');

INSERT INTO `country` VALUES ('IRL','Ireland','Europe','British Islands',70273.00,1921,3775100,76.8,75921.00,73132.00,'Ireland/Éire','Republic',1447,'IE');

INSERT INTO `country` VALUES ('THA','Thailand','Asia','Southeast Asia',513115.00,1350,61399000,68.6,116416.00,153907.00,'Prathet Thai','Constitutional Monarchy',3320,'TH');

INSERT INTO `country` VALUES ('CRI','Costa Rica','North America','Central America',51100.00,1821,4023000,75.8,10226.00,9757.00,'Costa Rica','Republic',584,'CR');

INSERT INTO `country` VALUES ('AUS','Australia','Oceania','Australia and New Zealand',7741220.00,1901,18886000,79.8,351182.00,392911.00,'Australia','Constitutional Monarchy, Federation',135,'AU');
```

**Expected output for each INSERT:**
```
Query OK, 1 row affected (0.00 sec)
```

**Command:** To query the table, I ran the following SELECT statement:

```sql
SELECT * FROM country WHERE GNP > 35000 and Population > 10000000;
```

**Expected output:**
```
+------+-----------+-----------+---------------------------+-------------+-----------+------------+----------------+-----------+-----------+--------------+------------------------------------+---------+-------+
| Code | Name      | Continent | Region                    | SurfaceArea | IndepYear | Population | LifeExpectancy | GNP       | GNPOld    | LocalName    | GovernmentForm                      | Capital | Code2 |
+------+-----------+-----------+---------------------------+-------------+-----------+------------+----------------+-----------+-----------+--------------+------------------------------------+---------+-------+
| AUS  | Australia | Oceania   | Australia and New Zealand |  7741220.00 |      1901 |   18886000 |           79.8 | 351182.00 | 392911.00 | Australia    | Constitutional Monarchy, Federation |     135 | AU    |
| THA  | Thailand  | Asia      | Southeast Asia            |   513115.00 |      1350 |   61399000 |           68.6 | 116416.00 | 153907.00 | Prathet Thai | Constitutional Monarchy             |    3320 | TH    |
+------+-----------+-----------+---------------------------+-------------+-----------+------------+----------------+-----------+-----------+--------------+------------------------------------+---------+-------+
2 rows in set (0.00 sec)
```

The query returned two records for Australia and Thailand.

✅ **Task complete:** I have successfully created a table named country, inserted data into the table, and queried records returning two results.

---

## Key Takeaways 💡

### Aurora Concepts Mastered:

| Concept | Description |
|---------|-------------|
| **Aurora Cluster** | Consists of a primary instance and zero or more Aurora Replicas |
| **Cluster Endpoint** | Connects to the primary instance for write operations |
| **Reader Endpoint** | Load-balances read-only connections across replicas |
| **DB Subnet Group** | Collection of subnets designated for RDS/Aurora instances |
| **Security Groups** | Act as virtual firewalls for database access control |

### SQL Commands Used:

| Command | Purpose |
|---------|---------|
| `SHOW DATABASES;` | List all databases |
| `USE database_name;` | Switch to a specific database |
| `CREATE TABLE...` | Create a new table structure |
| `INSERT INTO...` | Add records to a table |
| `SELECT...WHERE...` | Query records with conditions |

### Aurora Performance Benefits:
- **5x performance** of standard MySQL
- **Fully managed** with automatic failover
- **Compatible** with existing MySQL applications
- **Scalable** storage that grows automatically

---

## Important Notes ⚠️

- **Multi-AZ:** Not enabled in this lab for faster deployment; recommended for production
- **Encryption:** Not enabled in this lab; can be enabled for production workloads
- **Auto Minor Version Upgrade:** Disabled to prevent unexpected updates during the lab
- **Enhanced Monitoring:** Disabled to simplify the lab environment
- **Security:** Database is in private subnets with no public access

---

## Conclusion 🎉

I have now successfully:

- ✅ Created an Aurora instance
- ✅ Connected to a pre-created Amazon EC2 instance
- ✅ Configured the Amazon EC2 instance to connect to Aurora
- ✅ Queried the Aurora instance

---

## Additional Resources 📚

- [Amazon RDS Multi-AZ Deployments](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)
- [Working with an Amazon RDS DB Instance in a VPC](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html)
- [What Is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [Encrypting Amazon RDS Resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html)
- [Enhanced Monitoring](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.html)
- [Amazon Aurora Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)

---
