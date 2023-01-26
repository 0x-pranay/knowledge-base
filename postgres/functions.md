### How to get list of function having a search text in it. 

```sql

select 
proname as "functionName"
from pg_proc where prosrc like '%string_to_arrayX%';
```

```sql
select 
	routine_catalog AS DatabaseName
	,routine_schema AS SchemaName
	,routine_name AS FunctionName
	,routine_type AS ObjectType
from information_schema.routines 
where routine_definition like '%Your_Text%'
```









###  How to insert more than one row in a table with function in PostgreSQL ?

https://stackoverflow.com/questions/24343933/how-to-insert-multiple-rows-using-a-function-in-postgresql

```plsql
INSERT INTO mahasiswa(col_name1, col_name2)
   SELECT * FROM unnest(_arr1, _arr2); 
```

```plsql
INSERT INTO TAG.ATTRIBUTE (name, fleetid, clientid)
SELECT *, v_fleetId, p_clientid FROM unnest(v_names);
```







```


```





