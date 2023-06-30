
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
  
- Convert an array of Jsonb objects into rows with keys as the columns

  ```plsql
  SELECT * FROM  jsonb_to_recordset('[{ "a": 1, "status": "COACHED"}, { "a": 2, "status": "SKIPPED" }]'::jsonb)  as X(a int, status text)
  ```

- Inserting into a table from an array of objects

  ```sql
  WITH input_data(role_template_json) AS (
  	VALUES ('[
    {
      "roleId": "blankTemplateId",
      "roleName": "Blank Template",
      "description": "Customize your role from scratch with no predefined permissions or UI configuration",
      "metadata": [],
      "permissions": []
    }
  ]
  '::jsonb) 
  )
  INSERT INTO ACCESS.ROLE_TEMPLATE( name, description, permissions_jsonb, ui_permissions_jsonb, portalId, active_flag)
  SELECT  obj->>'roleName', obj->>'description', obj->'permissions', obj->'metadata', 1, TRUE
  FROM INPUT_DATA, jsonb_array_elements(input_data.role_template_json) AS "obj"
  RETURNING *
  ```

  
