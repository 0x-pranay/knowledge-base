https://www.freecodecamp.org/news/how-to-get-a-docker-container-ip-address-explained-with-examples

https://www.postgresql.org/docs/12/functions-json.html

## JSON

- Convert a table containing key and value as columns into a single json

  ```plsql
  	SELECT
  -- 	JSONB_AGG(ROW_TO_JSON(R.*)),
  -- 	ROW_TO_JSON(R.*)
  	jsonb_object(array_agg(key), array_agg(value)) AS KV
  -- 	array_agg(key),
  -- 	array_agg(value)
  FROM jsonb_each_text('{
  					 "total": 126,
  					 "Bookmarked": 3,
  					 "Seen": 64,
  					"Ignored": 38, "Reported": 6, "Blocked": 15 
  					 }') R
  WHERE key::text = ANY ('{ Seen, Bookmarked }'::text[]);
  
  ```

- Convert a two coloumn table into a jsonb with value as int

  ```plsql
  SELECT
  
  	jsonb_object_agg(key,value::int)
  
  FROM jsonb_each_text('{
  					 "total": 126,
  					 "Bookmarked": 3 
  					 }') R
  ```
  
  
