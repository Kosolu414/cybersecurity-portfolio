# Applying Filters to SQL Queries

* **Scenario:** As a security professional at a large organization. Part of the job is to investigate security issues to help keep the system secure. I recently discovered some potential security issues that involve login attempts and employee machines.

My task is to examine the organization’s data in their employees and log_in_attempts tables. I’ll need to use SQL filters to retrieve records from different datasets and investigate the potential security issues.

## Step-by-step Implementation of SQL Filters

That’s awesome! A portfolio project showcasing SQL filtering is highly valuable because it proves you know how to handle real-world data triage and security investigations.

To help make this portfolio-ready, I have structured the implementation steps below into a clean, professional **"Technical Workflow"** format. You can copy and paste this directly into your GitHub README or project documentation.

---

## Technical Workflow: Implementing SQL Filters for Security Analysis

### Step 1: Formulate the Base Query

Begin by identifying the target table and specifying the columns required for the investigation. For comprehensive security log analysis, select all columns to maintain full context.

* **Syntax:** `SELECT * FROM table_name;`

* **Portfolio Example:** `SELECT * FROM log_in_attempts;`


### Step 2: Initialize Data Filtering with `WHERE`

Append the `WHERE` clause immediately after the `FROM` statement. This instructs the database engine to evaluate row-level conditions rather than returning the entire dataset.

### Step 3: Apply Logical Operators Based on Use Case

Depending on the investigative objective, utilize logical operators (`AND`, `OR`, `NOT`) to isolate specific data patterns:

* **Isolating Compound Conditions (`AND`)**
* *Use Case:* When all defined criteria must simultaneously be met.


* *Code Application:* To isolate failed login attempts that occurred strictly after hours:
```sql
WHERE login_time > '18:00' AND success = FALSE;
```
> *"By filtering for `login_time > '18:00' AND success = FALSE`, I successfully minimized alert fatigue by eliminating thousands of standard daytime events, allowing the security team to focus exclusively on high-risk, after-hours brute force attempts."*
>



* **Expanding Scope Across Alternatives (`OR`)**
* *Use Case:* When a record is considered relevant if it matches any one of multiple criteria.


* *Code Application:* To audit system access across a specific multi-day window:
```sql
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```[cite: 1]


```




* **Excluding Baseline Data (`NOT`)**
* *Use Case:* When you need to filter out known-safe or irrelevant records to highlight anomalies.


* *Code Application:* To isolate non-IT personnel for targeted department audits:
```sql
WHERE NOT department = 'Information Technology';
```[cite: 1]


```





### Step 4: Implement Wildcards for Dynamic Pattern Matching

When dealing with inconsistent text strings or partial entries, leverage the `LIKE` operator combined with the percentage (`%`) wildcard. The `%` acts as a placeholder for zero or more characters.

* *Code Application:* To catch all variations of a country label (e.g., 'MEX' and 'MEXICO') while excluding them from the results:
```sql
WHERE NOT country LIKE 'MEX%';
```[cite: 1]


```



### Step 5: Execute and Validate Results

Run the complete query to extract the targeted subset of data. Verify that the output aligns with the parameters defined in the logical constraints to ensure zero false positives.

---

* **[👉 View File permissions Report](./Apply_filters_to_SQL_queries.pdf)*** 
