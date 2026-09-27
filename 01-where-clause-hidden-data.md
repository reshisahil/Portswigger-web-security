# SQL Injection: WHERE Clause Allowing Retrieval of Hidden Data

**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice
**Category:** SQL Injection
**Status:** Solved

## 1. Lab Objective

The application contains a SQL injection vulnerability in its product category filter.

The objective was to manipulate the SQL query to retrieve unreleased products.

## 2. Understanding the Vulnerability

The application uses the following SQL query:

```sql
SELECT * FROM products
WHERE category = 'Gifts' AND released = 1
```

* `SELECT *` retrieves all columns.
* `FROM products` specifies the table.
* `WHERE` filters the rows returned.
* `category = 'Gifts'` selects products in the Gifts category.
* `released = 1` restricts results to released products.

The vulnerability occurs because user input is incorporated into the SQL query without being safely handled.

## 3. Exploitation

**Payload used:**

```sql
' OR 1=1--
```

The injected `OR 1=1` condition is always true. The `--` comments out the remaining SQL in the query.

The resulting query behaves approximately like this:

```sql
SELECT * FROM products
WHERE category = 'Gifts' OR 1=1
```

Because `1=1` is always true, the query returns products beyond the original category and release restrictions.

## 4. Result

The application displayed unreleased products, successfully completing the lab.

## 5. Key Takeaways

* A `WHERE` clause filters rows based on conditions.
* SQL injection can alter the logic of a database query.
* `OR 1=1` creates a condition that is always true.
* The `--` sequence can comment out the remainder of a SQL statement, depending on the database.

## 6. Prevention

* Use parameterized queries or prepared statements.
 # Parameterized queries prevent SQL injection by separating SQL instructions from user input, ensuring that supplied values are treated as data rather than executable SQL code.
* Avoid building SQL queries by directly concatenating user input.
* Apply appropriate database permissions.
* Validate input as an additional security measure.

## 7. What I Learned
. The problem is that the application is treating user input as part of the SQL code.

. This lab helped me understand how SQL injection can manipulate a `WHERE` clause and expose data that the application was supposed to hide.

**Lab completed:** ✅
