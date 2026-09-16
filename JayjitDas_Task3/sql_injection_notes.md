# DVWA SQL Injection Testing Notes

## Task Information

- **Task:** Task 3 – SQL Injection on DVWA
- **Application:** Damn Vulnerable Web Application (DVWA)
- **Module:** SQL Injection
- **Security Level:** Low
- **Environment:** Local authorized security-training laboratory
- **Target:** DVWA running on the local Metasploitable VM

---

## Objective

The objective of this task is to demonstrate SQL Injection against the
DVWA SQL Injection module, document the actual results, explain why the
vulnerability occurs, and describe how developers can prevent it.

---

## Test 1 – Normal Query

**Input:**

```text
1

Result:

The application returned the corresponding user record, providing a
baseline for comparison with the injection tests.

Evidence:

screenshots/01-normal-query.png
Test 2 – SQL Injection Payload 1

Payload:

1' OR '1'='1

Result:

The application returned multiple database records, including:

admin / admin
Gordon / Brown
Hack / Me
Pablo / Picasso
Bob / Smith

Observation:

The input changed the intended SQL query logic and caused multiple
database records to be returned instead of the expected single record.

Evidence:

screenshots/02-sql-injection-1.png
Test 3 – SQL Injection Payload 2
Initial Payload
1' OR 1=1

Result:

The application returned a MySQL SQL syntax error:

You have an error in your SQL syntax; check the manual that
corresponds to your MySQL server version for the right syntax
to use near ''' at line 1

Observation:

The payload changed the SQL statement but left an unmatched quote,
causing a syntax error. The error message also revealed information
about the underlying MySQL database.

Corrected Payload
1' OR 1=1 #

Result:

The application successfully returned multiple records:

admin / admin
Gordon / Brown
Hack / Me
Pablo / Picasso
Bob / Smith

Observation:

The # comment marker caused the remaining part of the generated
MySQL query to be ignored, allowing the injected condition to alter
the query logic.

Evidence:

screenshots/03-sql-injection-2.png
Test Summary
Test	        Payload	               Result
Normal Query	1	            Normal record returned
SQL Injection1	1' OR '1'='1	Multiple records returned
SQL Injection2 	1' OR 1=1    	MySQL syntax error
SQL Injection2  1' OR 1=1 #	   Multiple records returned (Corrected)

Why SQL Injection Occurs :-
SQL Injection occurs when an application places user-controlled input
directly into an SQL query without safely separating data from SQL
syntax.

In this DVWA exercise, the supplied input was interpreted as part of
the SQL statement. The successful payloads therefore changed the
query's intended logic and returned multiple database records.

Security Impact

Depending on the application's implementation and database privileges,
SQL Injection can potentially allow:

- Unauthorized access to database information
- Bypass of intended query restrictions
- Modification or deletion of database records
- Disclosure of database structure or sensitive information

The exact impact depends on the application's database privileges
and functionality.

Recommended Remediation

Developers should use parameterized queries / prepared statements
instead of concatenating user input directly into SQL statements.

Additional protections include:

- Validate input according to the expected data type.
- Use least-privilege database accounts.
- Do not expose detailed SQL/database errors to users.
- Log database errors securely.
- Keep application and database software maintained.
- Safer Query Concept

Instead of constructing SQL with string concatenation:

SELECT first_name, surname
FROM users
WHERE user_id = ?

The user-supplied value should be passed separately as a parameter.

This prevents the input from being interpreted as SQL syntax.

Error Handling

The failed injection attempt exposed a MySQL syntax error.

In a production application, detailed database errors should be logged
internally but should not be displayed directly to users.

A safer user-facing response would be:

An unexpected error occurred. Please try again later.
Evidence
screenshots/
├── 01-normal-query.png
├── 02-sql-injection-1.png
└── 03-sql-injection-2.png
Conclusion

The DVWA SQL Injection module successfully demonstrated that
user-controlled input can alter SQL query behavior.

The payload:

1' OR '1'='1

returned multiple records.

The initial payload:

1' OR 1=1

produced a MySQL syntax error.

The corrected payload:

1' OR 1=1 #

also returned multiple records.

The results demonstrate the importance of parameterized queries,
prepared statements, input validation, least-privilege database
accounts, and safe error handling.

Disclaimer

All testing was performed only against a locally hosted DVWA
application in an authorized security-training laboratory.

Do not perform SQL Injection testing against systems or applications
without explicit authorization.


### Final file structure

```text
SecurityAnalyst-Beginner-Task3-DVWA-SQLInjection/
│
├── README.md
├── sql_injection_notes.md
└── screenshots/
    ├── 01-normal-query.png
    ├── 02-sql-injection-1.png
    └── 03-sql-injection-2.png