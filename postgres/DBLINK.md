```
CREATE SERVER fdtest FOREIGN DATA WRAPPER dblink_fdw OPTIONS (hostaddr '127.0.0.1', dbname 'contrib_regression');
```

lightmetrics_health_server

## 1. Create server

```
lightmetrics_qa_health_server


CREATE SERVER my_other_server  FOREIGN DATA WRAPPER dblink_fdw OPTIONS (hostaddr '***', dbname 'dbname');





CREATE USER MAPPING FOR my_user SERVER my_other_server OPTIONS (user 'other_server_user', password 'other_server_password');





```

## Create user on target server

```
create user my_other_server_user with password '****';

```

```

```

## Query
