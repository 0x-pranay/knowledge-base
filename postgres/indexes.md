[Things every developer absolutely, positively needs to know about database indexing - Kai Sassnowski](https://www.youtube.com/watch?v=HubezKbFL7E)

https://scalegrid.io/blog/using-jsonb-in-postgresql-how-to-effectively-store-index-json-data-in-postgresql/

https://github.com/dhamaniasad/awesome-postgres

https://www.postgresguide.com/cool/jsonb/



To analyze the size and load of indexes in PostgreSQL using various built-in functions and queries. Here are some common ways to do it:

1. **pg_stat_user_indexes**: This system view provides statistics about user-defined indexes, including their size in bytes. You can use it to get an overview of the index sizes in your database:

   ```sql
   SELECT relname AS index_name, pg_size_pretty(pg_size_bytes(idx_scan)) AS index_size
   FROM pg_stat_user_indexes
   ORDER BY pg_size_bytes(idx_scan) DESC;
   ```

   This query lists user-defined indexes and their sizes in descending order.

2. **pg_indexes_size()**: This function returns the size of an index in bytes. You can use it to check the size of a specific index:

   ```sql
   SELECT indexname AS index_name, pg_size_pretty(pg_indexes_size('your_index_name')) AS index_size
   FROM pg_indexes
   WHERE tablename = 'your_table_name';
   ```

   Replace `'your_index_name'` and `'your_table_name'` with the actual index and table names.

3. **pg_total_relation_size()**: This function returns the total size of a table or index, including both data and indexes. You can use it to see the total size of a specific index:

   ```sql
   SELECT indexname AS index_name, pg_size_pretty(pg_total_relation_size('your_index_name')) AS total_size
   FROM pg_indexes
   WHERE tablename = 'your_table_name';
   ```

4. **pg_size_pretty()**: This function converts the size in bytes to a more human-readable format.

5. **pg_stat_user_indexes and pg_indexes**: You can combine information from both `pg_stat_user_indexes` and `pg_indexes` to get a more comprehensive view of the indexes in your database, including both statistics and metadata.

6. **pg_stat_statements**: If you are using the `pg_stat_statements` extension, you can also track the number of times each index is scanned, which can give you an idea of the index load.

Remember to replace `'your_index_name'` and `'your_table_name'` with the actual names of the index and table you want to analyze. These queries will help you understand the size and load of your indexes, allowing you to make informed decisions about index maintenance, optimization, or removal when necessary.
