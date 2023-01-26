# Roles

```postgresql
SELECT CURRENT_USER;
SELECT CURRENT_ROLE;
```



- Get all rows:   

  ```postgresql
  SELECT rolname from pg_roles;
  ```

  ```sql
  SELECT * FROM information_schema.administrable_role_authorizations;
  SELECT * FROM information_schema.applicable_roles;
  
  
  ```

  - Create a new role

    ```postgresql
    CREATE USER nodejs_user PASSWORD '****'
    ```


# Privileges

- View all privileges

  ```sql
  SELECT * FROM information_schema.routine_privileges;
  
  SELECT * FROM INFORMATION_SCHEMA.USAGE_PRIVILEGES;
  
  SELECT * FROM INFORMATION_SCHEMA.TABLE_PRIVILEGES;
  
  SELECT * FROM  INFORMATION_SCHEMA.COLUMN_PRIVILEGES;
  
  ```

- View grouped privileges

  ```postgresql
  --- TABLE
  SELECT TABLE_SCHEMA, PRIVILEGES, ARRAY_AGG(table_NAME) 
  FROM  (
  	SELECT table_schema, table_name, ARRAY_AGG(privilege_type) AS PRIVILEGES 
  	FROM (
  		SELECT * FROM INFORMATION_SCHEMA.TABLE_PRIVILEGES 
  		WHERE GRANTEE = 'nodejs_user'
  		ORDER BY TABLE_SCHEMA, TABLE_NAME, PRIVILEGE_TYPE)T
  	GROUP BY 1, 2)R
  GROUP BY 1, 2
  
  --- FUNCTION
  SELECT OBJECT_SCHEMA, ARRAY_AGG(OBJECT_NAME) 
  FROM ( SELECT * 
  	  FROM  INFORMATION_SCHEMA.USAGE_PRIVILEGES 
  	  WHERE GRANTEE = 'nodejs_user'
  	  ORDER BY OBJECT_SCHEMA, OBJECT_NAME
  	  ) T
  GROUP BY OBJECT_SCHEMA
  
  --- USAGE on SEQUENCES
  SELECT OBJECT_SCHEMA, ARRAY_AGG(OBJECT_NAME) 
  FROM ( SELECT * 
  	  FROM  INFORMATION_SCHEMA.USAGE_PRIVILEGES 
  	  WHERE GRANTEE = 'nodejs_user'
  	  ORDER BY OBJECT_SCHEMA, OBJECT_NAME
  	  ) T
  GROUP BY OBJECT_SCHEMA
  
  -- Schema 
  SELECT n.nspname AS "Name",
    pg_catalog.pg_get_userbyid(n.nspowner) AS "Owner",
    pg_catalog.array_to_string(n.nspacl, E'\n') AS "Access privileges",
    pg_catalog.obj_description(n.oid, 'pg_namespace') AS "Description"
  FROM pg_catalog.pg_namespace n
  WHERE n.nspname !~ '^pg_' AND n.nspname <> 'information_schema'
  ORDER BY 1;
  
  ```

  

  ```
  
  {pgp_sym_encrypt,uuid_ns_dns,uuid_ns_url,uuid_generate_v1,encode_uri_component,is_integer,uuid_generate_v1mc,signs3url,jsonb_concat_array,remove_json_keys,uuid_generate_v4,uuid_generate_v3,date_utc_to_localx,datediff,is_numeric,gen_random_uuid,pgp_pub_decrypt_bytea,date_utc_to_local,array_trim,uuid_generate_v5,convert_boolean,convert_date,local_timestamp_to_utc,date_formatx,convert_integer,convert_numeric,convert_smallint,convert_timestamp,convert_timestampx,date_format,string_to_arrayx,hmac,hmac,crypt,gen_salt,gen_salt,encrypt,decrypt,encrypt_iv,digest,digest,pgp_sym_encrypt_bytea,pgp_sym_encrypt,pgp_sym_encrypt_bytea,pgp_sym_decrypt,pgp_sym_decrypt_bytea,pgp_sym_decrypt,pgp_sym_decrypt_bytea,pgp_pub_encrypt,pgp_pub_encrypt_bytea,pgp_pub_encrypt,pgp_pub_encrypt_bytea,pgp_pub_decrypt,pgp_pub_decrypt_bytea,pgp_pub_decrypt,date_local_to_utc,replace_multiple,urlencode,key_exists,validate_timestamp,sort_jsonb_array,jsonb_remove_array_element,validate_skip_limit,pgp_pub_decrypt,pgp_pub_decrypt_bytea,pgp_key_id,armor,armor,datediff_ms,is_boolean,dearmor,pgp_armor_headers,uuid_nil,uuid_ns_oid,uuid_ns_x500,decrypt_iv,gen_random_bytes,is_date}
  ```

  

  

# Docs

- https://www.postgresql.org/docs/current/sql-grant.html
- https://www.postgresql.org/docs/current/sql-revoke.html
- https://www.postgresql.org/docs/current/information-schema.html
- https://linuxhint.com/check-postgres-user-privileges/#:~:text=Another%20way%20to%20do%20this,databases%20as%20well%20as%20tables.