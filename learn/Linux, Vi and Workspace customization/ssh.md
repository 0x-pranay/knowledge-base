### How to close a frozen terminal or exit a ssh connection: 

```
 ~.  - terminate session

 ~B  - send a BREAK to the remote system

 ~R  - Request rekey (SSH protocol 2 only)

 ~#  - list forwarded connections

 ~?  - this message

 ~~  - send the escape character by typing it twice
```



## SSH Agent Forwarding

- It allows us to use our private, local ssh keys on a remote server without actually storing it on the remote server
- SSH agent forwarding is built into ssh, and all we need to do is add our keys to `ssh-agent` process using `ssh-add` command.

Scenarios

1. Where we want to make a git pull/push to a private repo but dont want your private keys on that remote server but only on your local machine.
2. Where we want to connect to a target host/instance using a hopserver without actually storing the ssh .pem keys on the hopserver. 



Example commands using Scenario 2. 

1. First check if ssh-agent process is running

   ```bash
   eval `ssh-agent`
   ```

2. Add ssh private keys into ssh-agent using the below command

   ```
   ssh-add ~/path/to/ec2-pems/keypair-ec2-dev.pem
   ```

   or

   ```
   ssh-add ~/.ssh/id_ed25519
   ```

3. Allow forwarding for  a ssh session using

   ```
   ssh -A hopserver
   ```

   or to always allow forwarding to a domain

   Add this to `~/.ssh/config`

   ```
   Host hopserver
     ForwardAgent yes
   ```

4. Connecting to target host. SSH looks for the correct private key from a list of private keys added earlier to ssh-agent.

   ```
   ssh ubuntu@10.10.3.254
   ```

5. (optional) If we need to go a bit deeper. example into the target host and then make a git pull using your github credentials.

   ```
   # add your github registered ssh Keys to ssh-agent like in step 2. 
   # In step 4 do this instead
   ssh -A ubuntu@10.10.3.254
   
   # Now make a git pull or git clone 
   git clone git://a-private-repo.git
   ```

   



http://www.unixwiz.net/techtips/ssh-agent-forwarding.html
http://www.unixwiz.net/techtips/openssh.html

https://www.howtogeek.com/devops/what-is-ssh-agent-forwarding-and-how-do-you-use-it/
