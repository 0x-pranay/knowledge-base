### check ssl in postgres

 load the `sslinfo` extension and then call the `ssl_is_used()` function to determine if SSL is being used. The function returns `t` if the connection is using SSL, otherwise it returns `f`.

```
CREATE EXTENSION sslinfo;

SELECT ssl_is_used();

```

