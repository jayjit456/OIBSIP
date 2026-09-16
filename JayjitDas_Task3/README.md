# OASIS INFOBYTE - Security Analyst Internship

## Task 3: SQL Injection on DVWA

## Project Information

- **Internship:** OASIS Infobyte – Security Analyst
- **Task:** Task 3 – SQL Injection on DVWA
- **Application:** Damn Vulnerable Web Application (DVWA)
- **Module:** SQL Injection
- **Security Level:** Low
- **Target:** Local DVWA running on the Metasploitable virtual machine
- **Testing Environment:** Authorized local security-training laboratory
- **Testing Tool:** Web Browser

---

## 1. Objective

The objective of this task is to demonstrate a classic SQL Injection
vulnerability in the DVWA SQL Injection module.

The assessment was performed in a controlled local laboratory
environment to understand how malicious input can alter SQL query
logic.

The task covers:

- DVWA configuration
- Normal SQL query behavior
- SQL Injection testing
- Multiple injection payloads
- Result analysis
- Security impact
- Recommended remediation

---

## 2. What is DVWA?

Damn Vulnerable Web Application (DVWA) is an intentionally vulnerable
web application designed for security training and learning.

It provides controlled exercises for studying common web application
security vulnerabilities.

For this task, the SQL Injection module was configured at the
**Low** security level.

---

## 3. Lab Environment

The DVWA application was accessed locally through the Metasploitable
virtual machine.

The testing was performed only against the authorized laboratory
application.

The application was accessed through the Metasploitable IP address
using a web browser.

---

## 4. DVWA SQL Injection Module

After logging into DVWA:

1. Open the **DVWA Security** section.
2. Set the security level to **Low**.
3. Click **Submit**.
4. Open the **SQL Injection** module.
5. Use the **User ID** input field for testing.

The SQL Injection page was used to compare normal input with
specially crafted SQL Injection input.

---

## 5. Normal Query Test

### Input

```text
1

Result :-

The application processed the normal user ID input and returned the
corresponding user record.

This result was used as the baseline for comparison with the injection
tests.

Evidence :- 
          screenshots/01-normal-query.png

6. SQL Injection Test 1
Payload :- 
1' OR '1'='1

Result :- 

The application returned multiple records instead of only the
expected record.

Observed records included:
admin / admin
Gordon / Brown
Hack / Me
Pablo / Picasso
Bob / Smith

Observation :-

The supplied input changed the intended SQL query logic.

This demonstrates that user-controlled input was being interpreted as
part of the SQL statement.

Security Impact

An SQL Injection vulnerability may allow unauthorized access to
database information or bypass intended query restrictions.

Evidence :-
       screenshots/02-sql-injection-1.png
7. SQL Injection Test 2
Initial Payload :- 
 1' OR 1=1
 Result:-
The application returned a MySQL syntax error:
You have an error in your SQL syntax; check the manual that
corresponds to your MySQL server version for the right syntax
to use near ''' at line 1

Observation

The payload modified the SQL statement but resulted in an unmatched
quote, causing a syntax error.

The error message also exposed information about the underlying
database technology.

Corrected Payload :-
1' OR 1=1 #

Result:-
The application returned multiple records:
admin / admin
Gordon / Brown
Hack / Me
Pablo / Picasso
Bob / Smith

Observation

The # character was interpreted as a MySQL comment marker. This
caused the remaining part of the generated query to be ignored,
allowing the injected condition to change the query logic.

Evidence:- 
screenshots/03-sql-injection-2.png

8. Why SQL Injection Occurs

SQL Injection occurs when an application places untrusted user input
directly into an SQL query without properly separating user data from
SQL syntax.

When the application fails to use safe query construction techniques,
a user may be able to introduce SQL expressions into the query.

In this DVWA exercise, the successful payloads altered the intended
query condition and caused multiple records to be returned.

9. Data Exposed During Testing
The successful tests returned multiple database records, including:

admin / admin
Gordon / Brown
Hack / Me
Pablo / Picasso
Bob / Smith
This demonstrates that the application did not restrict the result
to a single intended user record.

10. Security Impact:-

Depending on the application and database privileges, SQL Injection
can potentially lead to:

- Unauthorized database access
- Authentication or authorization bypass
- Disclosure of sensitive information
- Modification of database records
- Deletion of database data
- Disclosure of database structure

The actual impact depends on the application's implementation and
the privileges assigned to its database account.


11. Recommended Remediation :-
The primary defense against SQL Injection is to use:

Parameterized Queries / Prepared Statements

Instead of constructing SQL statements through string concatenation,
the application should treat user input as a separate parameter.

Example:
SELECT first_name, surname
FROM users
WHERE user_id = ?

The ? represents a parameter that is supplied separately from the
SQL statement.

This prevents user input from being interpreted as SQL syntax.

Additional Security Measures :-
- Validate input according to the expected data type.
- Use least-privilege database accounts.
- Avoid dynamic SQL where it is unnecessary.
- Do not expose detailed database errors to users.
- Log application and database errors securely.
- Keep the application and database software updated.

12. Error Handling :- 

During the initial second-payload test, the application displayed a
MySQL syntax error.

In a production application, detailed database errors should not be
shown directly to users.

Instead, technical details should be logged securely while the user
receives a generic message such as:

 An unexpected error occurred. Please try again later.

13. Evidence :-
The screenshots included with this project document the actual testing
process and results.
 screenshots/
├── 01-normal-query.png
├── 02-sql-injection-1.png
└── 03-sql-injection-2.png

Detailed payload information and analysis are documented in:  sql_injection_notes.md

14. Project Structure :
SecurityAnalyst-Beginner-Task3-DVWA-SQLInjection/
│
├── README.md
├── sql_injection_notes.md
└── screenshots/
    ├── 01-normal-query.png
    ├── 02-sql-injection-1.png
    └── 03-sql-injection-2.png

15. Ethical Considerations

All testing in this task was performed against a deliberately
vulnerable DVWA application in an authorized local security-training
laboratory.

No external or production website was tested.

SQL Injection testing must only be performed against applications for
which explicit authorization has been provided.

16. Conclusion

The DVWA SQL Injection module demonstrated how user-controlled input
can alter SQL query behavior when an application does not properly
separate data from SQL syntax.

The payload: 1' OR '1'='1

returned multiple database records.

The initial payload: 1' OR 1=1

produced a MySQL syntax error.

The corrected payload: 1' OR 1=1 #

also returned multiple records.

The exercise demonstrates the importance of parameterized queries,
prepared statements, input validation, least-privilege database
accounts, secure error handling, and proper application maintenance.

Disclaimer

This project was performed solely for authorized educational and
security-training purposes in a controlled local DVWA laboratory.

Do not perform SQL Injection testing against systems or applications
without explicit authorization.
