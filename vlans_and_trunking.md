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
- Core-SW1 needs all Main Office VLANs, whereas SW1, SW2, and SW3 only need the VLANs for devices they are directly connected to
  - ***Ex:*** SW1 needs VLANs 10, 40, and 60
- Configure basic VLAN info on each switch:
  - For SW1:
    ```cisco
    SW1(config)# vlan 10
    SW1(config-vlan)# name EXECUTIVE
    SW1(config-vlan)# exit
    SW1(config)# vlan 40
    SW1(config-vlan)# name IT
    SW1(config-vlan)# exit
    SW1(config)# vlan 60
    SW1(config-vlan)# name MANAGEMENT
    SW1(config-vlan)# exit
    SW1(config)# exit
    SW1# write memory
    ```
- Assign ports to VLANs:
  - For SW1:
    - ```cisco
      SW1(config)#interface range fa0/1 - 4
      SW1(config-if-range)#switchport mode access 
      SW1(config-if-range)#switchport access vlan 10
      SW1(config-if-range)#exit
    
      SW1(config)#interface range fa0/5 - 8
      SW1(config-if-range)#switchport mode access 
      SW1(config-if-range)#switchport access vlan 40
      SW1(config-if-range)#exit
    
      SW1(config)#interface range fa0/9 - 12
      SW1(config-if-range)#switchport mode access 
      SW1(config-if-range)#switchport access vlan 60
      ```
  - Here I am assigning ranges of ports (`interface range`) but single ports can be assigned too

- Configure SVIs on Core-SW1:
  - For every VLAN in Main Office:
    ```cisco
    CORE-SW1(config)#interface vlan 10

    %LINK-5-CHANGED: Interface Vlan10, changed state to up

    CORE-SW1(config-if)#ip address 10.10.10.1 255.255.255.0
    CORE-SW1(config-if)#no shut
    ```
