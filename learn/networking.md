### Check if port forwarding is enabled or not

```
sudo iptables -t nat -vnL
```

View running ports. 

```
sudo ss -ltnp
```



port forwarding 

````
ssh -i ~/path/to/key.pem -L 5433:postgres-server:5432 -N user@hopserver.example.com
````





```
ssh -L 5433:<rds_endpoint | ip_address>:5432 -N ubuntu@remote_bastion.example.com
```

Connecting to postgres from local machine through port forwarding

```
psql -h 127.0.0.1 -p 5433 -d <databasename> -U <username> -W
```

