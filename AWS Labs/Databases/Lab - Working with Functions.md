# Working with Functions 🔧

---

## Lab Overview & Objectives 🎯

The database operations team created a relational database named **world** containing three tables: **city**, **country**, and **countrylanguage**. Based on specific use cases in the lab exercise, I wrote several queries using database functions with the SELECT statement and WHERE clause.

When I started the lab, the following resources were already created for me:

![architecture-start (5)](https://github.com/user-attachments/assets/53df889e-c184-48be-a8c3-cf5ed42cb8ff)



*A Command Host instance and world database containing three tables (city, country, and countrylanguage) were already provisioned.*

---

After completing this lab, I am able to:
- ✅ Use aggregate functions **SUM()**, **MIN()**, **MAX()**, and **AVG()** to summarize data
- ✅ Use the **SUBSTRING_INDEX()** function to split strings
- ✅ Use the **LENGTH()** and **TRIM()** functions to determine the length of a string
- ✅ Use the **DISTINCT()** function to filter duplicate records
- ✅ Use functions in the SELECT statement and WHERE clause

---

## Task 1️⃣: Connect to the Command Host 🔌

In this task, I connected to an instance containing a database client, which is used to connect to a database. This instance is referred to as the **Command Host**.

In the AWS Management Console, I chose the **Services** menu, then **Compute**, and then **EC2**.

In the navigation pane, I chose **Instances**.

Next to the instance labelled **Command Host**, I selected the check box and then chose **Connect**.

For **Connect to instance**, I chose the **Session Manager** tab.

I chose **Connect** to open a terminal window.

To configure the terminal to access all required tools and resources, I ran the following commands:

```bash
sudo su
cd /home/ec2-user/
```

To connect to the database server, I ran the following command in the terminal. A password was configured when the database was installed.

```bash
mysql -u root --password='re:St@rt!9'
```



✅ **Task complete:** I successfully connected to the Command Host and database server.

---

## Task 2️⃣: Query the World Database with Functions 🔎

In this task, I queried the **world** database using various SELECT statements and database functions. Functions process and manipulate data in a query. There are a wide range of SQL functions, and this lab reviews a subset of commonly used functions.

### View Existing Databases

**Command:** To show the existing databases, I ran:

```sql
SHOW DATABASES;
```

I verified that a database named **world** was available.

### Review Table Structure and Data

**Command:** To review the table schema, data, and number of rows in the **country** table, I ran:

```sql
SELECT * FROM world.country;
```

---

### Aggregate Functions: SUM(), AVG(), MAX(), MIN(), COUNT()

Aggregate functions perform calculations on a set of values and return a single value. Because the query does not include a WHERE condition, the functions aggregate data from all records in the country table.

**Command:** To summarize population data across all countries:

```sql
SELECT sum(Population), avg(Population), max(Population), min(Population), count(Population) FROM world.country;
```


<img width="1910" height="915" alt="Screenshot 2026-02-12 151733" src="https://github.com/user-attachments/assets/ffd1a491-25fc-44f2-9f4f-bd4352f115cb" />



| Function | Purpose |
|----------|---------|
| **SUM()** | Adds all the population values together |
| **AVG()** | Generates an average across all population values |
| **MAX()** | Finds the row with the highest population value |
| **MIN()** | Finds the row with the lowest population value |
| **COUNT()** | Finds the number of rows with a population value |

---

### String Functions: SUBSTRING_INDEX()

In some cases, I needed to split a string. The **SUBSTRING_INDEX()** function returns a substring from a string before a specified number of occurrences of a delimiter.

**Syntax:** `SUBSTRING_INDEX(string, delimiter, count)`

**Command:** To split the Region column where a space occurs (returns the first part of each region name):

```sql
SELECT 
    Region, 
    SUBSTRING_INDEX(Region, " ", 1)
FROM world.country;
```
<img width="1914" height="899" alt="Screenshot 2026-02-12 151847" src="https://github.com/user-attachments/assets/592dca1d-8133-45e5-8c63-77a3cd931e54" />

After running the query, I noticed that the second column includes the beginning of each region name.

---

### Using Functions in WHERE Clauses

Sometimes I needed to search rows using a string fragment. The following query includes **SUBSTRING_INDEX()** as part of a condition in the WHERE clause to filter records.

**Command:** To filter records that include "Southern" in the first part of the region name:

```sql
SELECT Name, Region 
FROM world.country 
WHERE SUBSTRING_INDEX(Region, " ", 1) = "Southern";
```

<img width="1914" height="899" alt="Screenshot 2026-02-12 151847" src="https://github.com/user-attachments/assets/3820599d-715a-4063-b6ee-fb20ce74b882" />

---

### String Functions: LENGTH() and TRIM()

The **LENGTH()** function returns the length of a string in bytes. The **TRIM()** function removes leading and trailing spaces from a string.

**Command:** To return only regions that have fewer than 10 characters in their names (after trimming spaces):

```sql
SELECT Region 
FROM world.country 
WHERE LENGTH(TRIM(Region)) < 10;
```

<img width="1917" height="916" alt="Screenshot 2026-02-12 152210" src="https://github.com/user-attachments/assets/18b8acb6-6156-4446-9278-ef0d43008795" />


| Function | Purpose |
|----------|---------|
| **TRIM()** | Clears leading and trailing blank spaces |
| **LENGTH()** | Returns a count of the remaining characters |

---

### Filtering Duplicates: DISTINCT()

I noticed duplicate records in the previous example. The **DISTINCT()** function filters out duplicate values.

**Command:** To return unique region names with fewer than 10 characters:

```sql
SELECT DISTINCT(Region) 
FROM world.country 
WHERE LENGTH(TRIM(Region)) < 10;
```

---

## Challenge: Split Region Names 🧩

**Requirement:** Write a query to return rows that have **Micronesian/Caribbean** as the name in the region column. The output should split the region as **Micronesia** and **Caribbean** into two separate columns: one named **Region Name 1** and one named **Region Name 2**.

**My Solution:**

```sql
SELECT 
    SUBSTRING_INDEX(Region, '/', 1) AS 'Region Name 1',
    SUBSTRING_INDEX(Region, '/', -1) AS 'Region Name 2'
FROM world.country 
WHERE Region = 'Micronesian/Caribbean';
```


<img width="1919" height="901" alt="Screenshot 2026-02-12 152255" src="https://github.com/user-attachments/assets/b7e8dac9-4ac0-4382-af69-e48c0d561630" />



**Alternative solution (if needing country names as well):**

```sql
SELECT 
    Name,
    SUBSTRING_INDEX(Region, '/', 1) AS 'Region Name 1',
    SUBSTRING_INDEX(Region, '/', -1) AS 'Region Name 2'
FROM world.country 
WHERE Region = 'Micronesian/Caribbean';
```

✅ **Challenge completed:** I successfully used SUBSTRING_INDEX() to split the region name into two separate columns.

---

## Key Takeaways 💡

### SQL Functions Mastered:

| Function | Purpose | Example |
|----------|---------|---------|
| **SUM()** | Calculates total of numeric column | `SUM(Population)` |
| **AVG()** | Calculates average of numeric column | `AVG(Population)` |
| **MAX()** | Finds maximum value | `MAX(Population)` |
| **MIN()** | Finds minimum value | `MIN(Population)` |
| **COUNT()** | Counts rows | `COUNT(Population)` |
| **SUBSTRING_INDEX()** | Splits string on delimiter | `SUBSTRING_INDEX(Region, ' ', 1)` |
| **LENGTH()** | Returns string length | `LENGTH(Region)` |
| **TRIM()** | Removes leading/trailing spaces | `TRIM(Region)` |
| **DISTINCT()** | Removes duplicate values | `DISTINCT(Region)` |

### Function Categories:

| Category | Functions | Use Case |
|----------|-----------|----------|
| **Aggregate Functions** | SUM(), AVG(), MAX(), MIN(), COUNT() | Summarizing data across multiple rows |
| **String Functions** | SUBSTRING_INDEX(), LENGTH(), TRIM() | Manipulating text data |
| **Filtering Functions** | DISTINCT() | Removing duplicates from result sets |

---

## Important Notes ⚠️

- **Data Source:** Sample data in this course is taken from Statistics Finland, general regional statistics (February 4, 2022)
- **Aggregate Functions:** When using aggregate functions without GROUP BY, they return a single row summarizing all selected rows
- **String Delimiters:** The delimiter in SUBSTRING_INDEX() can be any character or string (space, comma, slash, etc.)
- **Positive vs Negative Count:** In SUBSTRING_INDEX(), positive count returns left side, negative count returns right side
- **TRIM() Importance:** Always use TRIM() with LENGTH() to get accurate character counts when data might have spaces

---

## Conclusion 🎉

I have now successfully:

- ✅ Used aggregate functions **SUM()**, **MIN()**, **MAX()**, and **AVG()** to summarize data
- ✅ Used the **SUBSTRING_INDEX()** function to split strings
- ✅ Used the **LENGTH()** and **TRIM()** functions to determine string length
- ✅ Used the **DISTINCT()** function to filter duplicate records
- ✅ Used functions in the SELECT statement and WHERE clause

At the end of this lab, you would have used the SELECT statement and WHERE clause with some common database functions:
![architecture-end (3)](https://github.com/user-attachments/assets/2db06c47-be0d-4ebd-93d8-455f5629f1ce)

A lab user is connected to a database instance. It also displays some commonly used SQL database functions.

---

## Additional Resources 📚

- [MySQL SELECT Statement Documentation](https://dev.mysql.com/doc/refman/8.0/en/select.html)
- [MySQL Aggregate Functions](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html)
- [MySQL String Functions](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html)
- [SUM() Function](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html#function_sum)
- [AVG() Function](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html#function_avg)
- [MIN() and MAX() Functions](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html#function_min)
- [SUBSTRING_INDEX() Function](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_substring-index)
- [LENGTH() Function](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_length)
- [TRIM() Function](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_trim)
- [Country, city, and language data, Statistics Finland](https://www.stat.fi/index.en.html)

---
