# VLANs and Trunking
Now that all the network appliances are set up with IP addresses, VLANs can be configured.

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


## VLAN Configuration
- 
