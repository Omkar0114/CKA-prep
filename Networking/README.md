# Networking basics

## Basic networking commands of Linux - 
- `ip link` - it is for listing and modifies interfaces on the host system

- `ip addr` - see the IP address assigned to those network interfaces

- `ip addr add 192.168.1.10/24 dev eth0` - to add ip address to that network interfaces

*These are the temporary changes if you want to permanently modify the `/etc/network/interface file`*

- `route or ip route` - used to view IP routing table
  
- `ip route add 192.168.1.0/24 via 192.168.2.1 ` - used for add entries into routing table

- `cat /proc/sys/net/ipv4/ip_forward` - to see if IP forwarding is enabled on the host if you're using the host system as a router

![image](https://github.com/Omkar0114/CKA-prep/assets/88308267/0f691787-6aa8-49ba-9f5a-06e0a2b63a2f)


## DNS - Domain Name System

- DNS is the naming convention for IP address.
- you can configure the names for specific IP addresses for particular hosts
- `/etc/hosts` - contains the hosts names for the ip addresses locally
- `/etc/resolv.conf` - This file lists all configured search domains.
- CoreDNS is the solution for the server ips
- If we need to change the ip naming every time we can store all IPs in the `nameserver` server and put it into the `/etc/hosts` directory

- If you have both local files and nameserver are configured on /etc/hosts and /etc/resolv.conf server how to follow the searching order?
  - Use the order in the `/etc/nsswitch.conf` file stored
 
- There are various tools such as `nslookuo www.google.com` pinging google.com OR `dig` 
