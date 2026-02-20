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


To configure the terminal to access all required tools and resources, run the following command:

```
sudo su
cd /home/ec2-user/
```
To connect to the relational database instance, run the following command in the terminal. A password was configured when the database was installed.
```
mysql -u root --password='re:St@rt!9'
```

----

## Task 2️⃣: Create a Database and Table
In this task, I will create a database named world and a table named country, then alter the country table.
View Existing Databases,run the following query.

```
SHOW DATABASES;
```

<img width="1890" height="280" alt="show database" src="https://github.com/user-attachments/assets/1a37973b-d727-40a8-990b-aac4c385bc16" />


To create a new database named **world**, run the following command.

```
CREATE DATABASE world;
```

<img width="1917" height="917" alt="Screenshot 2026-02-11 150333" src="https://github.com/user-attachments/assets/13b7f7d8-bea3-4419-be53-fc99d178e139" />

To verify that the **world** database has been created, run the following query. 

```
SHOW DATABASES;
```

To store data in a database, the database needs to contain one or more tables. In an SQL database, a table needs a well-defined structure, known as a table schema. To create a table named **country**, run the following command. 

```
CREATE TABLE world.country (
  `Code` CHAR(3) NOT NULL DEFAULT '',
  `Name` CHAR(52) NOT NULL DEFAULT '',
  `Conitinent` enum('Asia','Europe','North America','Africa','Oceania','Antarctica','South  America') NOT NULL DEFAULT 'Asia',
  `Region` CHAR(26) NOT NULL DEFAULT '',
  `SurfaceArea` FLOAT(10,2) NOT NULL DEFAULT '0.00',
  `IndepYear` SMALLINT(6) DEFAULT NULL,
  `Population` INT(11) NOT NULL DEFAULT '0',
  `LifeExpectancy` FLOAT(3,1) DEFAULT NULL,
  `GNP` FLOAT(10,2) DEFAULT NULL,
  `GNPOld` FLOAT(10,2) DEFAULT NULL,
  `LocalName` CHAR(45) NOT NULL DEFAULT '',
  `GovernmentForm` CHAR(45) NOT NULL DEFAULT '',
  `HeadOfState` CHAR(60) DEFAULT NULL,
  `Capital` INT(11) DEFAULT NULL,
  `Code2` CHAR(2) NOT NULL DEFAULT '',
  PRIMARY KEY (`Code`)
);
```


<img width="1917" height="917" alt="Screenshot 2026-02-11 150333" src="https://github.com/user-attachments/assets/a70768fa-776c-4f82-bf60-8ba9814f19be" />


To verify that the **country** table was created, use the **SHOW TABLES**; command to list the tables in the database. You use the USE command to specify which database to run a query against. Run the following commands in your terminal. 

```
USE world;
SHOW TABLES;
```

<img width="1919" height="936" alt="Screenshot 2026-02-11 150457" src="https://github.com/user-attachments/assets/f95bae34-22e4-48dc-95ea-ac66ca8a8d25" />

Used the **SHOW COLUMNS** query to list all the columns on a table. Run the following query to list all columns and their properties in the country table.

```
SHOW COLUMNS FROM world.country;
```

<img width="1911" height="907" alt="Screenshot 2026-02-11 150627" src="https://github.com/user-attachments/assets/e390aecc-44d6-4d31-bee1-8d469f9eb990" />

I Noticed that the Continent column is spelled incorrectly as **Conitinent**.

<img width="1919" height="502" alt="continent" src="https://github.com/user-attachments/assets/d2984d92-44e4-4621-b7eb-c7118934de12" />

The **ALTER TABLE** command is used to alter the table's schema. To fix the incorrectly spelled Continent column, run the following command.

```
ALTER TABLE world.country RENAME COLUMN Conitinent TO Continent;
```

To verify that the Continent column name in the country table has been corrected, run the following query.

```
SHOW COLUMNS FROM world.country;
```

<img width="1911" height="907" alt="Screenshot 2026-02-11 150627" src="https://github.com/user-attachments/assets/18cf8b97-102e-4040-b816-36320f9a4f4a" />


## Challenge 1: Create a city Table ✅

Created a table named city with two columns, both using the CHAR data type.

```
CREATE TABLE world.city (
  `Name` CHAR(52),
  `Region` CHAR(26) 
);
```

<img width="1907" height="635" alt="Screenshot 2026-02-11 151505" src="https://github.com/user-attachments/assets/ed5a2dc7-7ac8-4d91-a9c6-7e7c7320e7d2" />


## Task 3️⃣: Delete a database and tables

The **DROP TABLE** command is used to delete (drop) a table in a database. Once a table has been dropped, it cannot be recovered unless a backup is available. To drop the **city** table, run the following command.

```
DROP TABLE world.city;
```


## Challenge 2: Drop the country Table ✅

Wrote a query to drop the country table.

```
DROP TABLE world.country;
```

To verify that **both tables** have been dropped, run the following query.

```
SHOW TABLES;
```

To drop the **world** database, run the following command.

```
DROP DATABASE world;
```

To verify that the world database has been deleted, run the following query.

```
SHOW DATABASES;
```

----

At the end of this lab, I would have completed some common database and table operations:


![architecture-end (2)](https://github.com/user-attachments/assets/696f003c-4661-41cd-b510-5ed0708f409c)



A lab user creates a database and tables. Other displayed statements are SHOW, ALTER, and DROP.


---

## Key Takeaways 💡

### SQL Commands Mastered:
| Command | Purpose | Example |
|---------|---------|---------|
| `CREATE DATABASE` | Create a new database | `CREATE DATABASE world;` |
| `CREATE TABLE` | Create a new table | `CREATE TABLE world.country (...);` |
| `SHOW DATABASES` | List all databases | `SHOW DATABASES;` |
| `SHOW TABLES` | List tables in current database | `SHOW TABLES;` |
| `SHOW COLUMNS` | Display table structure | `SHOW COLUMNS FROM world.country;` |
| `ALTER TABLE` | Modify table structure | `ALTER TABLE...RENAME COLUMN...;` |
| `DROP TABLE` | Delete a table | `DROP TABLE world.city;` |
| `DROP DATABASE` | Delete a database | `DROP DATABASE world;` |

---



## Important Notes ⚠️

- **Data Source:** Sample data in this course is taken from Statistics Finland, general regional statistics (February 4, 2022)
- **Irreversible Operations:** The `DROP` command permanently deletes databases and tables. This action cannot be undone without a backup.
- **AWS Restrictions:** This lab environment restricts access to only the services and actions needed to complete the exercises.

---

## Conclusion 🎉

Successfully completed common database and table operations including:
- ✅ Creating databases and tables with `CREATE`
- ✅ Viewing database objects with `SHOW`
- ✅ Modifying table structures with `ALTER`
- ✅ Removing databases and tables with `DROP`

---

## Additional Resources 📚

- [MySQL CREATE Database Documentation](https://dev.mysql.com/doc/refman/8.0/en/create-database.html)
- [MySQL CREATE Table Documentation](https://dev.mysql.com/doc/refman/8.0/en/create-table.html)
- [MySQL SHOW Statements](https://dev.mysql.com/doc/refman/8.0/en/show.html)
- [MySQL ALTER Table Documentation](https://dev.mysql.com/doc/refman/8.0/en/alter-table.html)
- [MySQL DROP Database Documentation](https://dev.mysql.com/doc/refman/8.0/en/drop-database.html)
- [MySQL DROP Table Documentation](https://dev.mysql.com/doc/refman/8.0/en/drop-table.html)

---

