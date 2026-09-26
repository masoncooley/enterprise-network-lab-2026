# Network Design and Initial Configuration

## Company Definition
- Company name: Cooley Technologies
- Company size: ~50 employees
- Departments: Management, Sales, Accounting, IT

## Network Design
- IP addressing scheme:
  - Main Office: `10.10.0.0/16`
  - Branch Office: `10.20.0.0/16`
  
_The /16 networks are used as site-level address spaces, with individual /24 subnets allocated to each VLAN_

| VLAN # |          Name           |     Network    | Core SVI / Gateway |
| :----: | :---------------------: | :------------: | :-----------:      |
| 10     | Executive               | 10.10.10.0/24  | 10.10.10.1         |
| 20     | Sales                   | 10.10.20.0/24  | 10.10.20.1         |
| 30     | Accounting              | 10.10.30.0/24  | 10.10.30.1         |
| 40     | IT                      | 10.10.40.0/24  | 10.10.40.1         |
| 50     | Servers                 | 10.10.50.0/24  | 10.10.50.1         |
| 60     | Network Management      | 10.10.60.0/24  | 10.10.60.1         |
| 70     | Guest                   | 10.10.70.0/24  | 10.10.70.1         |
| 110    | Branch Users            | 10.20.10.0/24  | 10.20.10.1         |
| 120    | Branch Net. Management  | 10.20.20.0/24  | 10.20.20.1         |

---

|             |        R1       |        R2        |         ISP         |
| :---------: |  :---------:    |  :----------:    |   :-----------:     |
| Gigabit 0/0 | 203.0.113.2/30  | 198.51.100.2/30  | 203.0.113.1/30      |
| Gigabit 0/1 | 10.10.0.1/16    | 10.20.0.1/16     | 198.51.100.1/30     |
| Gigabit 0/2 | N/A             | N/A              | 192.0.2.1/24        |

## Design Goals
- Separate departments into individual broadcast domains using VLANs
- Provide Layer 3 routing between VLANs using the core multilayer switch
- Isolate guest traffic from internal networks
- Provide a dedicated network management VLAN
- Connect the main and branch offices using routed links
- Use OSPF for dynamic routing between sites

## Initial Configuration: 
- Create logical network topology in Cisco Packet Tracer
- Set hostname for each device
- Configure IP addresses for each router interface:
  - From Privileged EXEC mode `en`:
    - `show ip interface brief` to see names of all interfaces
  - From within Global Configuration mode `conf t`:
    - ```
      R1(config)#interface [interface name]
      R1(config-if)#ip address [interface IP address] [subnet mask]
      R1(config-if)#no shut
      ```
    - Repeat the above step for every connected interface of every router in the topology
