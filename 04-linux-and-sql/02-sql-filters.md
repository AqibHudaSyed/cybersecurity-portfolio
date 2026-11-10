# SQL Filters for Security Investigations

I used SQL filters on an organization's database to find suspicious login attempts and the employee machines that need security updates.

## Scenario

I am a security professional at a large organization. Some possible security issues were found with login attempts and employee machines. I used SQL filters on the organization database (MariaDB) to find the records that need to be investigated or updated.

## Skills used

| Area | Used for |
|---|---|
| `SELECT` / `FROM` | Choosing the table and columns to return |
| `WHERE` | Keeping only the rows that match a condition |
| `AND` / `OR` / `NOT` | Combining or reversing conditions |
| `LIKE` with `%` | Matching a text pattern (for example, anything that starts with `East`) |
| Comparison operators (`>`, `=`) | Filtering by time, date and values |

## Tables used

| Table | Columns |
|---|---|
| `log_in_attempts` | `event_id`, `username`, `login_date`, `login_time`, `country`, `ip_address`, `success` (0 = failed, 1 = successful) |
| `employees` | `employee_id`, `device_id`, `username`, `department`, `office` |

## Queries at a glance

| # | Task | Query | Result |
|---|---|---|---|
| 1 | Failed logins after business hours | `SELECT * FROM log_in_attempts WHERE login_time > '18:00' AND success = FALSE;` | 19 failed logins after 18:00 |
| 2 | Logins on two specific dates | `SELECT * FROM log_in_attempts WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';` | All logins on both dates |
| 3 | Logins from outside Mexico | `SELECT * FROM log_in_attempts WHERE NOT country LIKE 'MEX%';` | All logins where country is not MEX or MEXICO |
| 4 | Marketing employees in East offices | `SELECT * FROM employees WHERE department = 'Marketing' AND office LIKE 'East%';` | 7 employees |
| 5 | Finance or Sales employees | `SELECT * FROM employees WHERE department = 'Finance' OR department = 'Sales';` | All Finance and Sales employees |
| 6 | Everyone except IT | `SELECT * FROM employees WHERE NOT department = 'Information Technology';` | All employees outside IT |

### Sample output (query 1, first rows)

| event_id | username | login_date | login_time | country | ip_address | success |
|---|---|---|---|---|---|---|
| 2 | apatel | 2022-05-10 | 20:27:27 | CAN | 192.168.205.12 | 0 |
| 18 | pwashing | 2022-05-11 | 19:28:50 | US | 192.168.66.142 | 0 |
| 20 | tshah | 2022-05-12 | 18:56:36 | MEXICO | 192.168.109.50 | 0 |

### AND vs OR vs NOT

| Operator | Returns a row when... | Used in |
|---|---|---|
| `AND` | Both conditions are true | Queries 1 and 4 |
| `OR` | At least one condition is true | Queries 2 and 5 |
| `NOT` | The condition is false | Queries 3 and 6 |

`%` in `LIKE` means "any characters". `'East%'` matches `East-170`, `East-320` and so on.

## Report

### Project description
My organization found some possible security issues with login attempts and employee machines. I used SQL filters on the `log_in_attempts` and `employees` tables to find the records that need to be investigated or updated. I used the `WHERE` clause with the `LIKE`, `AND`, `OR` and `NOT` operators.

### Retrieve after hours failed login attempts
I'm investigating failed login attempts that were made after business hours (after 18:00, i.e. 6 PM) in the `log_in_attempts` table. I used the `WHERE` clause to check if `login_time` is greater than 18:00; `>` means it only returns logins after 18:00. I also added the filter `success = FALSE` using the `AND` operator, so it also checks that the login attempt failed (0). Here, 1 = True and 0 = False.

```sql
SELECT * FROM log_in_attempts WHERE login_time > '18:00' AND success = FALSE;
```

### Retrieve login attempts on specific dates
My team is investigating a suspicious event that occurred on 2022-05-09. I want all login attempts on this day and the day before (2022-05-08). The `login_date` column contains the dates of the login attempts. I used the `WHERE` clause on `login_date` with the `OR` operator, which returns the data if either of the conditions is true.

```sql
SELECT * FROM log_in_attempts WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

### Retrieve login attempts outside of Mexico
My team is investigating logins that did not originate in Mexico. The `country` field has entries with both `MEX` and `MEXICO`. To exclude Mexico, I used the `NOT` operator after `WHERE`, and the `LIKE` operator to match a pattern. The `%` after `MEX` means it matches any country that starts with `MEX`, so `LIKE` and `%` cover both `MEX` and `MEXICO`.

```sql
SELECT * FROM log_in_attempts WHERE NOT country LIKE 'MEX%';
```

### Retrieve employees in Marketing
My team is updating employee machines, and I need to find the employees in the Marketing department in all East building offices (such as East-170 or East-320). `SELECT *` returns all columns, and `WHERE` filters the rows where the department is Marketing `AND` the office starts with East. `AND` means both conditions must be true. I used `LIKE` and `%` to match East.

```sql
SELECT * FROM employees WHERE department = 'Marketing' AND office LIKE 'East%';
```

### Retrieve employees in Finance or Sales
My team and I need to perform a different update on the computers of all employees in the Finance or Sales department, and I need to find these employees. The `OR` operator returns rows if either condition is true. We cannot use `AND` here because it only gives a result if both conditions are true, so `AND` would return 0 rows.

```sql
SELECT * FROM employees WHERE department = 'Finance' OR department = 'Sales';
```

### Retrieve all employees not in IT
One more update was already made to computers in the Information Technology department. The team needs information about employees who are not in that department. I used the `NOT` operator with `WHERE` to keep every row except the Information Technology department.

```sql
SELECT * FROM employees WHERE NOT department = 'Information Technology';
```

### Summary
I used SQL filters to investigate login attempts and find employee machines that need updates. I found failed login attempts after 18:00, all login attempts on 2022-05-08 and 2022-05-09, and login attempts from outside Mexico. I also found employees in Marketing in the East building, in Finance or Sales, and all employees not in IT, using `AND`, `OR`, `NOT` and `LIKE` with `%`.

## What I learned

- `AND` narrows the results, `OR` widens them.
- `LIKE` with `%` helps when the same value is stored in different ways (MEX and MEXICO).
- A department column holds one value per row, so `department = 'Finance' AND department = 'Sales'` can never be true.
