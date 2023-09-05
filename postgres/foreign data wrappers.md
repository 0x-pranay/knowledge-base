### View all foreign servers

`SELECT * FROM pg_foreign_server`

### View all foreign data wrappers

`SELECT * FROM pg_foreign_data_wrapper;`

### View all user mappings

`SELECT * FROM pg_user_mappings;`





### Create a foreign server and user mapping

``` sql
CREATE SERVER db_b_server
	FOREIGN DATA WRAPPER postgres_fdw    OPTIONS (dbname 'databaseB', host 'localhost', port '5432');

-- Create a user mapping
CREATE USER MAPPING FOR current_user
    SERVER db_b_server
    OPTIONS (user 'db_b_user', password 'db_b_password');
```





### Drop user mapping

```
DROP USER MAPPING [IF EXISTS] FOR [user] SERVER [server_name];

DROP USER MAPPING IF EXISTS FOR my_user SERVER my_server;

```





### Executing the query using the foreign server

```sql
CREATE OR REPLACE FUNCTION insert_update_row_in_db_b()
RETURNS VOID AS $$
DECLARE
    db_b_conn TEXT := 'dbname=databaseB host=localhost port=5432 user=db_b_user password=db_b_password';
BEGIN
    -- Insert/update operation in databaseB
    EXECUTE format('
        INSERT INTO databaseB.schemaB.tableB (column1, column2, column3)
        VALUES (%L, %L, %L)
        ON CONFLICT (unique_column) DO UPDATE
        SET column1 = EXCLUDED.column1, column2 = EXCLUDED.column2, column3 = EXCLUDED.column3',
        value1, value2, value3)
    USING db_b_conn;

    -- Commit the transaction
    COMMIT;
END;
$$ LANGUAGE plpgsql;

```



- https://www.postgresql.org/docs/current/plpgsql-statements.html#PLPGSQL-STATEMENTS-EXECUTING-DYN
- 





- https://www.postgresql.org/docs/current/postgres-fdw.html
- https://www.postgresql.org/docs/current/sql-createforeigndatawrapper.html
- https://www.postgresql.org/docs/current/dblink.html

- https://www.postgresql.org/docs/current/file-fdw.html