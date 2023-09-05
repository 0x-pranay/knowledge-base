VPN: [15.206.209.141]



Bypass vpn for specific sites

```
sudo ip route add <target_ip_address>/32 via 192.168.1.1 dev eth0

```

192.168.1.1 -> IP address of your default gateway

Get this by `ip route` Look for the line that starts with "default" in the output. This line represents the default route, which is used for all traffic that does not match any of the other routes.

````

````

--

---

To create a proxy on your local Ubuntu desktop that can be used with the Proxy Switcher Omega extension in Chrome to control which websites go through VPN and which do not, you can use a combination of OpenVPN and a local proxy server.

Here are the general steps to follow:

1. Install a local proxy server on your Ubuntu machine, such as Squid Proxy.
2. Configure the local proxy server to listen on a specific port, such as 3128, and to allow traffic from your local network.
3. Configure the OpenVPN client to route traffic for specific websites through the local proxy server.
4. Configure the Proxy Switcher Omega extension in Chrome to use the local proxy server for specific websites.

Here are more detailed steps to follow:

1. Install and configure Squid Proxy on your Ubuntu machine. You can do this by running the following commands in a terminal window:

```
sqlCopy codesudo apt-get update
sudo apt-get install squid
sudo nano /etc/squid/squid.conf
```

In the Squid configuration file, make sure that the `http_access` and `acl` directives allow traffic from your local network, and set the `http_port` directive to a specific port number, such as 3128. Save and close the file.

1. Connect to the OpenVPN server using the OpenVPN client on your Ubuntu machine.
2. Add a specific route for the websites that you want to bypass the VPN and use the local proxy server instead. You can do this by adding a custom routing table in the OpenVPN client configuration file, such as:

```
cssCopy coderoute-nopull
route website.com 255.255.255.255 net_gateway table 10
route website2.com 255.255.255.255 net_gateway table 10
route 0.0.0.0 0.0.0.0 vpn_gateway
```

This will add a custom routing table named "10" for the websites you want to bypass the VPN, and route all other traffic through the VPN gateway.

1. Configure the Proxy Switcher Omega extension

- 
- 
- https://chat.openai.com/chat/50b5525b-89ab-4a88-bb76-e1db06e9fa87
- 