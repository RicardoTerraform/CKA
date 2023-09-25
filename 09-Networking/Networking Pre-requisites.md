# Networking Pre-Requisites


### switching and routing
- list an modify interfaces on the host.
ip link

- see the IP addresses assigned to those interfaces.
ip addr

- set IP addresses on the interfaces
ip addr add 192.168.1.10/24 dev eth0

- is used to view the routing table
ip route

- is used to add entries into the routing table.
ip route add 192.168.1.0/24 via 192.168.2.1

### DNS

