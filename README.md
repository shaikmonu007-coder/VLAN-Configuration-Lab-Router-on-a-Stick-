# VLAN-Configuration-Lab-Router-on-a-Stick-
A VLAN Configuration Lab using Router-on-a-Stick (perfect for CCNA-level).
# 🧠 VLAN Configuration Lab (Router-on-a-Stick)

## 🔹 Objective
To configure inter-VLAN communication between multiple VLANs using a single physical router interface (Router-on-a-Stick method).

---

## 🔹 Topology
Devices used:
- 1 × Cisco 2811 Router  
- 2 × Cisco 2960 Switches  
- 3 × PCs (for VLAN 10, 20, and 30)

---

## 🔹 VLAN Details
| VLAN ID | VLAN Name | Subnet | Default Gateway |
|----------|------------|--------|-----------------|
| 10 | HR | 192.168.10.0/24 | 192.168.10.1 |
| 20 | IT | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Finance | 192.168.30.0/24 | 192.168.30.1 |

---

## 🔹 Configuration Steps

### 🖥️ On Switch
```bash
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name HR
Switch(config)# vlan 20
Switch(config-vlan)# name IT
Switch(config)# vlan 30
Switch(config-vlan)# name Finance

Switch(config)# interface range fa0/1 - 3
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport  access vlan 10
! (Assign VLANs as needed)
Switch(config)# interface fa0/24
Switch(config-if)# switchport mode trunk
Router> enable
Router# configure terminal
Router(config)# interface g0/0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface g0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router:
Router(config)# interface g0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0

Router(config)# interface g0/0.30
Router(config-subif)# encapsulation dot1Q 30
Router(config-subif)# ip address 192.168.30.1 255.255.255.0
Verification:
Switch# show vlan brief
Router# show ip interface brief
PC> ping 192.168.20.2
