## How iptables Work

Network traffic is made up of packets. Data is broken up into smaller pieces (called packets), sent over a network, then put back together. Iptables identifies the packets received and then uses a set of rules to decide what to do with them.

Iptables filters packets based on:

- **Tables:** Tables are files that join similar actions. A table consists of several **chains**.
- **Chains:** A chain is a string of **rules**. When a packet is received, iptables finds the appropriate table, then runs it through the chain of **rules** until it finds a match.
- **Rules:** A rule is a statement that tells the system what to do with a packet. Rules can block one type of packet, or forward another type of packet. The outcome, where a packet is sent, is called a **target**.
- **Targets:** A target is a decision of what to do with a packet. Typically, this is to accept it, drop it, or reject it (which sends an error back to the sender).

### Tables and Chains

Linux firewall iptables has four default tables. We will list all four along with the chains each table contains.

1. Filter

   The **Filter** table is the most frequently used one. It acts as a bouncer, deciding who gets in and out of your network. It has the following default chains:

- **Input** – the rules in this chain control the packets received by the server.
- **Output** – this chain controls the packets for outbound traffic.
- **Forward** – this set of rules controls the packets that are routed through the server.

2. Network Address Translation (NAT)

   This table contains [NAT (Network Address Translation)](https://phoenixnap.com/glossary/nat-network-address-translation) rules for routing packets to networks that cannot be accessed directly. When the destination or source of the packet has to be altered, the NAT table is used. It includes the following chains:

- **Prerouting –** this chain assigns packets as soon as the server receives them.
- **Output –** works the same as the output chain we described in the **filter** table.
- **Postrouting –** the rules in this chain allow making changes to packets after they leave the output chain.

3. Mangle

   The **Mangle** table adjusts the IP header properties of packets. The table has all the following chains we described above:

- **Prerouting**
- **Postrouting**
- **Output**
- **Input**
- **Forward**

4. Raw

   The **Raw** table is used to exempt packets from connection tracking. The raw table has two of the chains we previously mentioned:

- **Prerouting**
- **Output**



### Enable Loopback Traffic

It’s safe to allow traffic from your own system (the localhost). Append the **Input** chain by entering the following:

```
sudo iptables -A INPUT -i lo -j ACCEPT
```



### Delete a rule

```
sudo iptables -t nat -D POSTROUTING <number>
```



## Persisting the changes.

``` sudo apt-get install iptables-persistent```

sudo /etc/init.d/iptables-persistent save 
sudo /etc/init.d/iptables-persistent reload

```
iptables-save > /etc/network/iptables.rules
```





## Redirect incoming traffic in hopserver to rds instance

```
iptables -t nat -A PREROUTING -p tcp --dport 5432 -j DNAT --to-destination <target_private_ip>:5432
```

### Run the below script to get the new IP address and use a cronjob every 5 secs to check for new IP when rds rotates the private ip.
```
new_ip=$(nslookup <rds-endpoint-static>.ap-south-1.rds.amazonaws.com  | awk '/Address: / { print $2 }')

```

or

```
aws rds describe-db-instances --db-instance-identifier <rds-id> --query 'DBInstances[*].Endpoint.Address' --output text


```



```
nslookup <rds-endpoint-static>.ap-south-1.rds.amazonaws.com  | awk '/Address: / { print $2 }'


### WIP progress bash script
```
#current_ip=$(iptables -t nat -L PREROUTING -n --line-numbers | grep 5432 | awk '{print $8}' | cut -d ':' -f1)
#new_ip=$(aws rds describe-db-instances --db-instance-identifier <rds-instance-identifier> --query 'DBInstances[*].Endpoint.Address' --output text)
#
#if [ "$current_ip" != "$new_ip" ]; then
#           iptables -t nat -A PREROUTING -p tcp --dport 5432 -j DNAT --to-destination $new_ip:5432
#               service iptables save
#fi

current_ip=$(cat rds_private_ip.txt)
new_ip=$(nslookup <rds-static-endpoint>.ap-south-1.rds.amazonaws.com  | awk '/Address: / { print $2 }')

if [ "$current_ip" != "$new_ip" ]; then
       
        service iptables save
fi

```

```



https://www.cyberciti.biz/faq/howto-iptables-show-nat-rules/

