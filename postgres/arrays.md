## How to lowercase an array 

```sql
select lower(array['Tallinn', 'Tartu','Narva']::text)::text[];
```