# SQL Injection: Login Bypass

**Platform:** PortSwigger Web Security Academy
**Difficulty:** Apprentice
**Category:** SQL Injection
**Status:** Solved

## 1. Lab Objective

The application contains a SQL injection vulnerability in its login function.

The objective was to log in as the `administrator` user without knowing the password.

## 2. Vulnerability

The login function uses user-supplied input in a SQL query that checks the username and password.

If the input is not handled safely, an attacker may manipulate the query and bypass authentication.

## 3. Payload

```sql
administrator'--
```

I entered this payload in the username field and used a random password.

## 4. How It Works

The application query can be represented as:

```sql
SELECT * FROM users
WHERE username = 'administrator'
AND password = 'random';
```

The injected single quote closes the username string, and `--` comments out the remaining part of the query.

The query effectively becomes:

```sql
SELECT * FROM users
WHERE username = 'administrator';
```

This removes the password condition, allowing the application to authenticate the administrator account if the query returns that user.

## 5. Result

Successfully logged in as the administrator without knowing the password.

## 6. Key Takeaways

* SQL injection can bypass authentication.
* SQL comments can remove remaining conditions from a vulnerable query.
* Login forms must handle user input safely.
* Parameterized queries help prevent SQL injection.

## 7. Prevention

Use parameterized queries or prepared statements to separate SQL instructions from user input.

**Lab completed:** ✅
