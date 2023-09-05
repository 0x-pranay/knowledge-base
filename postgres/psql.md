Download a query into a csv 



psql session

```
\pset format csv 

\o filename

\o

\pset format aligned
```





psql query 

```
\copy

```



```
To remove tags, pass tagIds with empty array. 
To add a new tag, pass tagIds with existing tagIds and new tagId in the same array
```















-----









Connection string issue.

- Having a $ sign doesn't work, instead use url encoded value ie `%24`





connect to a remote host

```
psql -h <IP_Address> -p <port_no> -d <database_name> -U <DB_username> -W

psql -h <rds_endpoint | ip_address | localhost > -p 5432 -d <database_name> -U nodejs_user -W
```





```
 ssh -L 5434:prod-apse2-pg-rds-masterdb-aurora.cluster-cc124tvxtmvx.ap-southeast-2.rds.amazonaws.com:5432 -i ~/lm-pems/hop_ssh_public-prod_usw2.pem -N ubuntu@ec2-52-12-222-195.us-west-2.compute.amazonaws.com



 ssh -L 5434:target_db_host:5432 -i ~/my_identity_file.pem -N ubuntu@tunnel_host_ip
```



```



`
 Host prod-hopserver
  36   │   Hostname ec2-52-12-222-195.us-west-2.compute.amazonaws.com
  37   │   Port 22
  38   │   User ubuntu
  39   │   IdentityFile ~/lm-pems/hop_ssh_public-prod_usw2.pem
  40   │

```

## Prompt coloring

```
set     red="%{\033[1;31m%}"
set   green="%{\033[0;32m%}"
set  yellow="%{\033[1;33m%}"
set    blue="%{\033[1;34m%}"
set magenta="%{\033[1;35m%}"
set    cyan="%{\033[1;36m%}"
set   white="%{\033[0;37m%}"
set     end="%{\033[0m%}"
```





https://www.cs.umd.edu/~srhuang/teaching/code_snippets/prompt_color.tcsh.html
