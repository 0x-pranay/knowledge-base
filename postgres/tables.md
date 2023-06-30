```
ALTER TABLE table_name 
ADD COLUMN column_name datatype column_constraint;
```


Create a table from an existing table and copy the data but without copies the table constraints, indexes and foregin key references.
TODO: refer postgres documentation
```
create table schema_name.new_table as select * from schema_name2.old_table
```

