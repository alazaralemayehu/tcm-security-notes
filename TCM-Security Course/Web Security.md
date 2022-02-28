## 1. **SQL Injection**

**SQL Injection** is vulnerability that lets an attacker to interferring with the SQL queries that an application makes to a database.

- **SQL Injection** structure  is divided into Three 
- **SQL Injection** 
	- In-Band (Classical)
		- Error
		- Union
	- Infrential (Blind) 
		- Boolean
		- Time
	- Out-of-Band 

**In-Band SQL Injection**

- Occurs when an attacker uses the same communcation channel to both launch the attack and gather the result of the attack. 
- Retrieved data is shown directly in the application web page
- Two types:
	- Error based: the attacker forces the database to generate an error, giving the attacker information upon which to refine the injection
	- Union based: that leverage the UNION SQL operator to combine the results of two queries into a single result set

**Inferential (Blind) SQL Injection**
- Occurs where tehre is not actual transfer of data via the web application. We  don't see the output of the result. Based on asking true/false questions.
- Takes longer than In-Band SQL Injection
- Two Types:
	- Boolean-based SQLi is a blind SQLi technique that usese Boolean conditions to return a different result depending on whether the query returns a TRUE or FALSE result. [The injection contains a command to compare some part of the result and check the result is TRUE or FALSE]
	- Time-Based SQLI is a blind SQLi technique that relies on the database pausing for a specified amount of time, then returning the results indicating a successful SQL query execution. [The injection contains a command to sleep for some times and check if it accepts the injection or not]
**Out-of-Band (OAST) SQLi**
- vulnerability that consists of triggering an out-of-band network connection to a system that you control 
- Not ommont
- A variety of protocols can bse used in DNS, HTTP


	### **Finding SQLi vulnerabilities**

Black Box Testing and White Box Testing

**In Blak box Testing**, it is good to follow the following steps:
- Map the application
- Fuzz the application:
	- Submit **SQL-specific character** and look for errors and anomalies
	- Submit **boolean conditions such as OR 1=1 and OR 1=2** and look for differences in the applcation's response
	- Submit paylods designed to  when exectuted withing a SQL query, and lookf or differences in the time taken to respond
	- Submit OAST payloads designed to tirrget out-of-band network interactions.
**In White box testing**, it is good to follow the these steps
- Enable web server and database logging to see output of our injection
- Map the application
	- Visibile functionality in the application
	- Regex search on all instances in the code to find a code that talks to the database
	- Search for usage of insecure sql functions
	- Code review
		- follow the code path for all input vectors
	- Test any potential SQLi vulnerabilities 

### **Exploiting Error-based SQLi**
- Submit SQL-sepcific character such as 'or ", and look for errors or other anomalies
- Different characters can give you differet errors

### **Exploiting Union-based SQLi**
- Union-based SQLi leverages the union functionality provided by sql
- Two rules for combining the results sets of two queries by using UNION:
	- The number and order of the columns must be the same in all queires
	- The data types must be compatible
- Exploitation
	- Figure out the number of columns that query is making
	- Figure out the data types of the columns
	- use the UNION to output information from database
	
- Ways to figure out **number of columns** is:
	- to use **ORDER BY** (since order by clause orders based on the columns, when the order by is above the number of columns error happen)
	- to use **UNION SELECT NULL**. increase amount of NULL until the number of NULL is the same as the number columns required
- Ways to figure out **data types of the column**:
	- To keep probing column to test whether it can hold string data by submitting a series of UNION SELECT payloads that place a string value into each column inturn.
	
	**Automated Exploitation Tools**
	- sqlmap
	- Web Application Vulnerability Scanners (WAVS) 

**How to prevent SQLi vulnerabilities**
- **Primary Defenses:**
	- Use of prepared statements (Parameterized Queries)
	- Use of Stored Procedures (Partial)
	- Use Allowlist Input Validation (Partial)
	- Escaping All User Supplied Inputs (Partial)
- **Additional Defenses:**
	- Enforcing Least Privilege
	- Performing Allowlist Input Validation as a Secondary Defense
	
**More Resources**
- Web Security Academy: https://portswigger.net/web-security 
Web Application Hacker’s Handbook: Chapter 9 Attacking Data Stores
OWASP – SQL Injection: https://owasp.org/www-community/attacks/SQL_Injection
OWASP – SQL Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html
PentestMonkey – SQL Injection: https://pentestmonkey.net/category/cheat-sheet/sql-injection