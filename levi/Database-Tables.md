Topic: Database Tables
Date: 2/5/18
***

## Indexing
- Adding indexes will increase the write speed, but will significantly decrease the time it takes to conduct a read.
- `CREATE index (email) on users;`
- Can use UNIQUE to add unique key to each value of a column (i.e. emails).
- Looking at the WHERE in your operation will tell you where an index may be appropriate.
- Using keyword EXPLAIN will tell you what Postgresql will do to complete the operation. 


## Normalization
- Setting up our database tables to be of a specific convention.
- Every column should have only one value.

- If you have data that can be split up into multiple tables, you can create an in between table acting as a referencing table.
```sql
CREATE TABLE students_classes (
  Student_id INT REFERENCES (student) ON id,
  Class_id INT REFERENCES (class) ON id
);
```

- If you have data in a table that is more closely related to itself than to the primary focus of that table, you should break out that data into its own table. For example, address data in a table about a student. This address data can be in its own table and be referenced by key.

#### Students
| id | name | address_id | age |
|----|------|------------|-----|
| 1 | Alex | 1 | 30 |
| 2 | Alice | 2 | 25 |

#### Address
| id | student_id | city | state | zip |
|----|------------|------|-------|-----|
| 1 | 1 | Aiea | HI | 96813 |
| 2 | 2 | Honolulu | HI | 96813 |