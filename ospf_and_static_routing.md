# OSPF and Static Routing Configuration

OSPF (Open Shortest Path First) is a dynamic interior gateway protocol (IGP) used to exchange routing information between routers within an autonomous system (like within a single ISP). Unlike static routing, OSPF allows routers to dynamically learn routes to networks that are not directly connected.

In this lab specifically, OSPF is used to allow communication between the Main Office and Branch Office. For a network this small, static routing would work perfectly. However, if the network were to grow in size (as most networks do), it would quickly become very difficult to configure all the necessary static routes.

## OSPF Setup

### R1
```
R1(config)#router ospf 1
R1(config-router)#router-id 1.1.1.1
R1(config-router)#network 10.10.254.0 0.0.0.3 area 0
R1(config-router)#network 10.10.253.0 0.0.0.3 area 0
```
### R2
```
R2(config)#router ospf 1
R2(config-router)#router-id 2.2.2.2
R2(config-router)#network 10.20.0.0 0.0.255.255 area 0
R2(config-router)#network 10.10.253.0 0.0.0.3 area 0
```
### Core-SW1
```
CORE-SW1(config)#router ospf 1
CORE-SW1(config-router)#router-id 3.3.3.3
CORE-SW1(config-router)#network 10.10.0.0 0.0.255.255 area 0
CORE-SW1(config-router)#network 10.10.254.0 0.0.0.3 area 0
```

## Static Routing

Syntax for `ip route` command: `ip route [network ID] [subnet mask] [IP address of next hop]`
### R1
- Default route: `ip route 0.0.0.0 0.0.0.0 203.0.113.1`

### Core-SW1
- Default route: `ip route 0.0.0.0 0.0.0.0 10.10.254.1`

### R2
- Default route: `ip route 0.0.0.0 0.0.0.0 198.51.100.1`

### ISP
- Route to Main Office (`R1`): `ip route 10.10.0.0 255.255.0.0 203.0.113.2`
- Route to Branch Office (`R2`): `ip route 10.20.0.0 255.255.0.0 198.51.100.2`


---

**Go to next page: [Security and SSH](security_and_ssh.md)**
