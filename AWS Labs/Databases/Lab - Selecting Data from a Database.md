# Selecting Data from a Database 📊

---

## Lab Overview & Objectives 🔍

The database operations team created a relational database named **world** containing three tables: **city**, **country**, and **countrylanguage**. Based on specific use cases defined in the lab exercise, I wrote several queries using database operators and the SELECT statement.

When I started the lab, the following resources were already created for me:


![architecture-start (4)](https://github.com/user-attachments/assets/538e2845-1b8b-4db9-a9fa-6a9e2744d7a5)



*A Command Host instance and world database containing three tables (city, country, and countrylanguage) were already provisioned.*

---

After completing this lab, I am able to:
- ✅ Use the SELECT statement to query a database
- ✅ Use the COUNT() function
- ✅ Use the following operators to query a database:
  - `<`
  - `>`
  - `=`
  - `WHERE`
  - `ORDER BY`
  - `AND`

---

## Task 1️⃣: Connect to the Command Host 🔌

In this task, I connected to an instance containing a database client, which is used to connect to a database. This instance is referred to as the **Command Host**.

In the AWS Management Console, I chose the **Services** menu, then **Compute**, and then **EC2**.

In the left navigation menu, I chose **Instances**.

Next to the instance labelled **Command Host**, I selected the check box and then chose **Connect**.


<img width="1917" height="920" alt="Screenshot 2026-02-12 134342" src="https://github.com/user-attachments/assets/b05f11ee-7e03-4408-83f0-0334090b2e12" />


For **Connect to instance**, I chose the **Session Manager** tab.

I chose **Connect** to open a terminal window.

<img width="1916" height="923" alt="Screenshot 2026-02-12 134422" src="https://github.com/user-attachments/assets/3d17ca8a-3514-4097-93eb-479ac875e631" />


To configure the terminal to access all required tools and resources, I ran the following commands:

```bash
sudo su
cd /home/ec2-user/
```

To connect to the database server, I ran the following command in the terminal. A password was configured when the database was installed.

```bash
mysql -u root --password='re:St@rt!9'
```

> **Note:** At any stage of the lab, if the Session Manager window became unresponsive or I needed to reconnect to the database, I followed these steps:
> 1. Closed the Session Manager window and tried to reconnect
> 2. Ran the following commands in the terminal:
>    ```bash
>    sudo su
>    cd /home/ec2-user/
>    mysql -u root --password='re:St@rt!9'
>    ```

✅ **Task complete:** I successfully connected to the Command Host and database server.

---

## Task 2️⃣: Query the World Database 🔎

In this task, I queried the **world** database using various SELECT statements and database operators.

### View Existing Databases

**Command:** To show the existing databases, I ran:

```sql
SHOW DATABASES;
```

I verified that a database named **world** was available.

### Query All Data from a Table

**Command:** To list all rows and columns in the **country** table, I ran:

```sql
SELECT * FROM world.country;
```


<img width="1915" height="923" alt="Screenshot 2026-02-12 135342" src="https://github.com/user-attachments/assets/bbf32908-a16c-4f5e-9676-547446e5cb31" />


### Count Rows in a Table

The **COUNT()** function returns the number of rows in a table. To count all rows in a table, I used `COUNT(*)`. To count rows with a value in a specific column, I included the column name: `COUNT(Population)`.

**Command:** To list the number of rows in the **country** table, I ran:

```sql
SELECT COUNT(*) FROM world.country;
```


<img width="1909" height="911" alt="Screenshot 2026-02-12 135530" src="https://github.com/user-attachments/assets/d7b196c8-8160-4b92-b18b-9fc87eb1262c" />


### Understand Table Structure

**Command:** To list all columns in the **country** table and understand the table schema, I ran:

```sql
SHOW COLUMNS FROM world.country;
```

<img width="1909" height="911" alt="Screenshot 2026-02-12 135530" src="https://github.com/user-attachments/assets/268e2ad0-d7f7-4013-b03b-5595593352b7" />



### Query Specific Columns

**Command:** To return a result set that includes the **Name, Capital, Region, SurfaceArea, and Population** columns, I ran:

```sql
SELECT Name, Capital, Region, SurfaceArea, Population FROM world.country;
```



<img width="1914" height="916" alt="Screenshot 2026-02-12 135642" src="https://github.com/user-attachments/assets/8aa71a9d-887f-44a7-9dd0-640f1df0cefa" />



### Use Column Aliases with AS

Database column names are sometimes not user friendly. To add more descriptive column names to the query output, I used the **AS** option.

**Command:** To display SurfaceArea as "Surface Area", I ran:

```sql
SELECT Name, Capital, Region, SurfaceArea AS "Surface Area", Population FROM world.country;
```

I observed that the SurfaceArea column was displayed as **Surface Area** in the results.

### Order Results with ORDER BY

Ordered result sets are easier to view and work with. To order the output based on a column, I used the **ORDER BY** option.

**Command:** To order the output by population (ascending by default):

```sql
SELECT Name, Capital, Region, SurfaceArea AS "Surface Area", Population FROM world.country ORDER BY Population;
```

### Order in Descending Order with DESC

To order data in descending order, I used the **DESC** option with ORDER BY.

**Command:** To order by population from highest to lowest:

```sql
SELECT Name, Capital, Region, SurfaceArea AS "Surface Area", Population FROM world.country ORDER BY Population DESC;
```


### Filter Results with WHERE

I added conditions to SELECT statements by using the **WHERE** clause.

**Command:** To list all rows with a population greater than 50,000,000:

```sql
SELECT Name, Capital, Region, SurfaceArea AS "Surface Area", Population FROM world.country WHERE Population > 50000000 ORDER BY Population DESC;
```


<img width="1919" height="922" alt="Screenshot 2026-02-12 135900" src="https://github.com/user-attachments/assets/7283601c-110e-4153-acd9-79995ef28929" />



I used the `>` comparison operator. Similarly, other comparison operators can be used to compare values.

### Combine Conditions with AND

I constructed a WHERE clause using multiple conditions and operators.

**Command:** To list rows with a population greater than 50,000,000 **AND** less than 100,000,000:

```sql
SELECT Name, Capital, Region, SurfaceArea AS "Surface Area", Population FROM world.country WHERE Population > 50000000 AND Population < 100000000 ORDER BY Population DESC;
```

<img width="1919" height="925" alt="Screenshot 2026-02-12 140045" src="https://github.com/user-attachments/assets/3a891185-be3c-48b3-a9cb-1451081bfdd2" />


The **AND** operator indicates that both conditions must be true.

---

## Challenge: Query the country Table 🧩

**Question:** Which country in Southern Europe has a population greater than 50,000,000?

**My Solution:**

```sql
SELECT Name, Capital, Region, Population 
FROM world.country 
WHERE Region = 'Southern Europe' 
  AND Population > 50000000;
```

✅ **Challenge completed:** I successfully queried the country table to find the specific country meeting both criteria.

---

## Key Takeaways 💡

### SQL Commands Mastered:

| Command/Operator | Purpose | Example |
|-----------------|---------|---------|
| `SELECT` | Retrieve data from a database | `SELECT * FROM world.country;` |
| `COUNT()` | Count rows in a table | `SELECT COUNT(*) FROM world.country;` |
| `WHERE` | Filter records based on conditions | `WHERE Population > 50000000` |
| `ORDER BY` | Sort results (ascending by default) | `ORDER BY Population` |
| `DESC` | Sort in descending order | `ORDER BY Population DESC` |
| `AS` | Create column aliases | `SurfaceArea AS "Surface Area"` |
| `>` | Greater than operator | `Population > 50000000` |
| `<` | Less than operator | `Population < 100000000` |
| `=` | Equal to operator | `Region = 'Southern Europe'` |
| `AND` | Combine multiple conditions | `condition1 AND condition2` |

### Comparison Operators Reference:

| Operator | Description |
|----------|-------------|
| `=` | Equal to |
| `<>` or `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |
| `BETWEEN` | Between a range |
| `LIKE` | Pattern matching |
| `IN` | Match any value in a list |

---

## Important Notes ⚠️

- **Data Source:** Sample data in this course is taken from Statistics Finland, general regional statistics (February 4, 2022)
- **Database Structure:** The world database contains three tables: city, country, and countrylanguage
- **Case Sensitivity:** SQL keywords are case-insensitive, but table and column names may be case-sensitive depending on the operating system
- **String Values:** String values in WHERE clauses must be enclosed in quotes (`'Southern Europe'`)

---

## Conclusion 🎉

I have now successfully:

- ✅ Used the SELECT statement to query a database
- ✅ Used the COUNT() function to count rows
- ✅ Used comparison operators (`<`, `>`, `=`) to filter data
- ✅ Used WHERE clauses to filter records
- ✅ Used ORDER BY to sort results
- ✅ Used AND to combine multiple conditions

---

## Additional Resources 📚

- [MySQL SELECT Statement Documentation](https://dev.mysql.com/doc/refman/8.0/en/select.html)
- [MySQL COUNT() Function](https://dev.mysql.com/doc/refman/8.0/en/counting-rows.html)
- [MySQL ORDER BY Clause](https://dev.mysql.com/doc/refman/8.0/en/order-by-optimization.html)
- [MySQL WHERE Clause](https://dev.mysql.com/doc/refman/8.0/en/where-optimization.html)
- [MySQL Comparison Operators](https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html)
- [Country, city, and language data, Statistics Finland](https://www.stat.fi/index.en.html)

---
