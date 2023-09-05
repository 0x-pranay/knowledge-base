Installing

```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
```

## 2024-06-05

1. Creating an AWS VPC (Virtual Private Cloud)

2. Creating a public subnet inside our VPC

3. Adding an Internet Gateway for our VPC which will help give us public internet access from inside the VPC

4. Adding a custom route table for our subnet

5. Adding a Security Group for our VPC to control the network traffic

6. Adding a network interface for our to-be-created EC2 Instance

7. Providing the network interface with a public static IP (AWS Elastic IP)

8. Finally creating the AWS EC2 Instance inside the subnet created and installing nginx inside of it

---

Projects

1. aws
   1. ec2
      1. nginx

custom network

1. vpc
   1. subnets
      1. public
         1. route table -> igw
      2. private
         1. route table
            1. inbound -> NAT

![undefined](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c7/NAT_Concept-en.svg/1920px-NAT_Concept-en.svg.png)

NAT:

data comprises of packets

packets -> tcp / udp protocols

packets

​ final_destination : 10.152.16.16

​ immediate_destination:

​ origin
