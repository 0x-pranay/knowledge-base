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

The below command open local post 5433 and forward to 5432 on hopserver. 

`-L` 		flag mean you are forwarding local port.
 `-f` 		option tells the `ssh` command to run in the background and

`-N` 		not to execute a remote command. 

```
ssh -L 5433:<rds_endpoint | ip_address>:5432 -N ubuntu@hopserver.example.com
```

Connecting to postgres from local machine through port forwarding

```
psql -h 127.0.0.1 -p 5433 -d lightmetrics -U pranay -W
```



