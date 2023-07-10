# Networking basics

## Basic networking commands of Linux - 
- `ip link` - it is for list and modify interfaces on the host system

- `ip addr` - see the ip address assigned to those network interfaces

- `ip addr add 192.168.1.10/24 dev eth0` - to add ip address to that network interfaces

*These are the temporary changes ,if you want to do permanent modify the `/etc/network/interface file`*

- `route or ip route` - used to view ip routing table
  
- `ip route add 192.168.1.0/24 via 192.168.2.1 ` - used for add entries into routing table

- `cat /proc/sys/net/ipv4/ip_forward` - to see if ip forwarding is enabled on the host if you're using host system as a router

![image](https://github.com/Omkar0114/CKA-prep/assets/88308267/0f691787-6aa8-49ba-9f5a-06e0a2b63a2f)


