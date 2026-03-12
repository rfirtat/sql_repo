# CREATE
### Create a new database
```sql
CREATE DATABASE DatabaseName
```
 
### Create a table
```sql
CREATE TABLE [IF NOT EXISTS] TableName  (
    Column1 DATA_TYPE,
    Column2 DATA_TYPE,
    ...
    ColumnN DATA_TYPE
);
```




# DELETE
Delete a **database**, including all tables
```sql
DROP DATABASE DatabaseName
```
Delete a **table**, along with all the table's rows
```sql
DROP TABLE [IF EXISTS] TableName
```

# USEFUL
`USE DatabaseName` selects a default database for use in subsequent statments  