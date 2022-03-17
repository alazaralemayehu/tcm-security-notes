## 1\. SQL Injection

**SQL Injection** is a vulnerability that lets an attacker interfere with the SQL queries an application makes to a database.

- **SQL Injection** structure is divided into Three
- **SQL Injection**
  - In-Band (Classical)
    - Error
    - Union
  - Inferential (Blind)
    - Boolean
    - Time
  - Out-of-Band

**In-Band SQL Injection**

- It occurs when an attacker uses the same communication channel to launch the attack and gather the result of the attack.
- Retrieved data is shown directly on the application web page
- Two types:
  - Error based: the attacker forces the database to generate an error, giving the attacker information upon which to refine the injection
  - Union-based: that leverage the UNION SQL operator to combine the results of two queries into a single result set

**Inferential (Blind) SQL Injection**

- There is no actual transfer of data via the web application. We don't see the output of the result. Based on asking true/false questions.
- Takes longer than In-Band SQL Injection
- Two Types:
  - Boolean-based SQLi is a blind SQLi technique that uses Boolean conditions to return a different result depending on whether the query returns a TRUE or FALSE result. \[The injection contains a command to compare some part of the result and check the result is TRUE or FALSE\]
  - Time-Based SQLI is a blind SQLi technique that relies on the database pausing for a specified amount of time, then returning the results, indicating a successful SQL query execution. \[The injection contains a command to sleep for some times and check if it accepts the injection or not\]
    **Out-of-Band (OAST) SQLi**
- the vulnerability that consists of triggering an out-of-band network connection to a system that you control
- Not common
- A variety of protocols can be used in DNS HTTP.
  ### **Finding SQLi vulnerabilities**

Black Box Testing and White Box Testing

**In Blak box Testing**, it is good to follow the following steps:

- Map the application
- Fuzz the application:
  - Submit **SQL-specific characters** and look for errors and anomalies
  - Submit **boolean conditions such as OR 1=1 and OR 1=2** and look for differences in the application's response
  - Submit payloads designed to when executed within a SQL query, and look or discrepancies in the time taken to respond
  - Submit OAST payloads designed to target out-of-band network interactions.
    **In White box testing**, it is good to follow these steps
- Enable web server and database logging to see the output of our injection
- Map the application
  - Visible functionality in the application
  - Regex search on all instances in the code to find a code that talks to the database
  - Search for the usage of insecure SQL functions
  - Code review
    - follow the code path for all input vectors
  - Test any potential SQLi vulnerabilities

### **Exploiting error-based SQLi**

- Submit SQL-specific characters such as 'or ", and look for errors or other anomalies
- Different characters can give you various errors

### **Exploiting Union-based SQLi**

- Union-based SQLi leverages the union functionality provided by SQL.
- Two rules for combining the results sets of two queries by using UNION:
  - The number and order of the columns must be the same in all queries
  - The data types must be compatible
- Exploitation
  - Figure out the number of columns that query is making
  - Figure out the data types of the columns
  - use the UNION to output information from the database
- Ways to figure out several** columns** are:
  - to use **ORDER BY** (since order by clause orders are based on the columns when the order by is above the number of columns error happen)
  - To use **UNION SELECT NULL**. increase the amount of NULL until the number of NULL is the same as the number columns required
- Ways to figure out **data types of the column**:
  - To keep the probing column to test whether it can hold string data by submitting a series of UNION SELECT payloads that place a string value into each column.
    **Automated Exploitation Tools**
  - SQLMap
  - Web Application Vulnerability Scanners (WAVS)

**How to prevent SQLi vulnerabilities**

- **Primary Defences:**
  - Use of prepared statements (parameterized Queries)
  - Use of Stored Procedures (Partial)
  - Use Allowlist Input Validation (Partial)
  - Escaping All User Supplied Inputs (Partial)
- **Additional Defences:**
  - Enforcing Least Privilege
  - Performing Allowlist Input Validation as a Secondary Defence

**More Resources**

- Web Security Academy: https://portswigger.net/web-security
  Web Application Hacker’s Handbook: Chapter 9 Attacking Data Stores
  OWASP – SQL Injection: https://owasp.org/www-community/attacks/SQL_Injection
  OWASP – SQL Prevention Cheat Sheet: [https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
  PentestMonkey – SQL Injection: https://pentestmonkey.net/category/cheat-sheet/sql-injection

## 2\. Cross-site Scripting

Cross-site scripting (XSS) allows an attacker to compromise users' interaction with the vulnerable application. The vulnerability allows an attacker to pretend as a victim and perform any action that the user can achieve. This attack happens by circumventing the Same Origin Policy.

It works by manipulating a vulnerable website so that the website returns malicious JavaScript to the User. When the malicious code executes inside the victim's browser, it can compromise the interaction between applications.

The best way to confirm if XSS vulnerability exists is to cause the browser to execute arbitrary JavaScript, E.g., alert().

when testing for XSS, the critical task is to examine the context:

- The location within the response where attacker-controllable data appears.
- Any input validation or other processing performed on that data by the application.

**Types of XSS attacks**

1.  **Reflected XSS**: The malicious script comes from the current HTTP request
    The attack payload is included with the data within the immediate response sent with the request. When the user visits the URL crafted by the attacker, the attacker's script executes in the user's browser in the context of that user's session. That means the attacker has access to the session can retrieve any data to which the user has access.

- If reflected XSS is successful, it has the following impacts:
  - perform any action within the application that the user can perform
  - View/modify any information that the user is capable of
  - initiating interactions with other application users, including malicious attacks that will appear to originate from the initial victim user. \[Simulate the victim\]

2.  **Stored XSS**: The malicious script comes from the database. The data received from an untrusted source will be displayed in later HTTP responses in an unsafe way.

If an attacker can control what is being displayed using stored XSS, it does everything that reflected XSS does.

4.  **DOM-based XSS**: vulnerability exists in client-side code rather than server-side code.

Exploiting XSS vulnerabilities to steal cookies can happen by accessing the cookies and sending them to a website that listens to the incoming request. This approach has some limitations:

- The victim may not be logged in
- applications may hide their cookies using the HttpOnly header
- Session access may be locked down to external user's attributes, such as IP address
- The session may time out before it is possible to hijack it
