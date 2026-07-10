# Applying Filters to SQL Queries

* **Scenario:** As a security professional at a large organization. Part of the job is to investigate security issues to help keep the system secure. I recently discovered some potential security issues that involve login attempts and employee machines.

My task is to examine the organization’s data in their employees and log_in_attempts tables. I’ll need to use SQL filters to retrieve records from different datasets and investigate the potential security issues.

## Step-by-step Implementation of SQL Filters

### Step 1: Formulate the Base Query

Begin by specifying the columns you want to retrieve and the target table. In these security tasks, all columns are selected using `SELECT *`.

* **Example:** `SELECT * FROM log_in_attempts` or `SELECT * FROM employees`.



### Step 2: Add the `WHERE` Clause

Introduce the `WHERE` clause immediately after the table name to initiate the filtering process.

### Step 3: Apply Logical Operators and Conditions

Depending on your specific security or administrative goal, combine your conditions using logical operators (`AND`, `OR`, `NOT`) and wildcards:

* **To filter for multiple simultaneous conditions (AND):** Use `AND` when all conditions must be true.


* *Implementation:* To find failed logins after hours, combine the time and status:
```sql
WHERE login_time > '18:00' AND success = FALSE;
```[cite: 1]

```


* *Implementation:* To find Marketing employees in a specific building:
```sql
WHERE department = 'Marketing' AND office LIKE 'East%';
```[cite: 1]


```




* **To filter for alternative conditions (OR):** Use `OR` when a record only needs to match one of multiple criteria.


* *Implementation:* To find login activity across two different dates:
```sql
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```[cite: 1]

```


* *Implementation:* To pull employees from multiple departments:
```sql
WHERE department = 'Finance' OR department = 'Sales';
```[cite: 1]


```




* **To exclude specific data (NOT):** Use `NOT` to filter out records that match a certain criteria.


* *Implementation:* To find all employees except those in IT:
```sql
WHERE NOT department = 'Information Technology';
```[cite: 1]


```





### Step 4: Incorporate Wildcards for Pattern Matching (Optional)

When dealing with variations in text data, use the `LIKE` operator with the percentage sign (`%`) wildcard to match partial strings.

* *Implementation:* To capture variations of Mexico (like 'MEX' and 'MEXICO') while excluding them, use:
```sql
WHERE NOT country LIKE 'MEX%';
```[cite: 1]


```



### Step 5: Execute and Review the Output

Run the completed query to extract the isolated, targeted data patterns necessary for your security or administrative investigation.

* **Phase 1:** Auditing the File SystemAction: Navigated to the targeted directory (e.g., /home/researcher2/projects) and ran the ls -la command to expose all files, subdirectories, and hidden files (like .project_x.txt).  
**Analysis:** Analyzed the 10-character string (e.g., -rw-rw-r--) to determine the exact read ($r$), write ($w$), and execute ($x$) rights allocated to the User, Group, and Other.

* **Phase 2:** Remediating Unauthorized Access
**Action:** Identified files where unauthorized users or broad "other" groups had write or execute access.  
**Correction:** Utilized the chmod command to restrict permissions. For example, explicitly removing write or execute access from others or groups (chmod o-w filename or chmod g-x directory_name) to match corporate compliance.

* **Phase 3:** Verification.  
**Action:** Re-ran ls -la to confirm that the permissions string correctly updated and that the system achieved the desired secure state.

### 📈 Key Outcomes & Security Impact

* **Principle of Least Privilege:** Successfully restricted sensitive files so only authorized researchers can modify them.
* **System Hardening:** Mitigated risks of internal unauthorized data manipulation or malicious script execution by revoking unnecessary execute ($x$) rights on files and directories.
* **Compliance:** Realigned the directory structures with organizational security policies.

* **[👉 View File permissions Report](./Apply_filters_to_SQL_queries.pdf)*** 
