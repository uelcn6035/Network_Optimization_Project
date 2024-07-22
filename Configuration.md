# Optimized Network

## Access Switch 1-4
interface range F0/1-2
 switchport mode trunk

interface range F0/3-20
 switchport access vlan 10
 switchport mode access
 switchport voice vlan 30
 spanning-tree portfast
 spanning-tree bpduguard enable

interface range F0/21-24
 switchport access vlan 20
 spanning-tree portfast
 spanning-tree bpduguard enable
```
## DSW-1
int f0/7
switchport trunk encapsulation dot1q 
switchport mode trunk
ex
```
## WLC-Control-PC
int f0/10
switchport mode access
switchport access vlan 10
switchport voice vlan 30
spanning-tree portfast
spanning-tree bpduguard enable
ex
```
## WLC
int f0/9
switchport mode access
switchport access vlan 20
spanning-tree portfast
##spanning-tree bpduguard enable
ex
```
## Link to Access Switch
interface range F0/1-4
switchport trunk encapsulation dot1q 
switchport mode trunk
ex
```
## VLAN Configuration
vlan 10
name LAN
ex
vlan 20
name WIRELESS
ex
vlan 30
name VOICE
ex
```
## Interface Configuration
interface range F0/22-24
channel-group 1 mode active
interface port-channel 1
switchport trunk encapsulation dot1q 
switchport mode trunk
ex
```
## HSRP & INTER-VLAN Routing
int vlan 10
ip add 192.168.1.1 255.255.255.224
ip helper-address  192.168.1.110
standby 10 priority 200
standby 10 ip 192.168.1.2
ex

int vlan 20
ip add 192.168.1.33 255.255.255.224
ip helper-address  192.168.1.110
standby 20 priority 255
standby 20 ip 192.168.1.34
ex

int vlan 30
ip add 192.168.1.65 255.255.255.240
ip helper-address  192.168.1.110
standby 20 priority 255
standby 20 ip 192.168.1.66
ex

int f0/8
no switchport 
ip add 192.168.1.93 255.255.255.252
ex
```
## DSW-2
int f0/7
switchport trunk encapsulation dot1q 
switchport mode trunk
ex
```
## DHCP Server
int f0/10
no switchport 
ip add 192.168.1.109 255.255.255.252
ex
```
## WLC
int f0/9
switchport mode access
switchport access vlan 20
spanning-tree portfast
##spanning-tree bpduguard enable
ex
```
## Link to Access Switch
interface range F0/1-4
switchport trunk encapsulation dot1q 
switchport mode trunk
ex
```
## VLAN Configuration
vlan 10
name LAN
ex
vlan 20
name WIRELESS
ex
vlan 30
name VOICE
ex
```
## Interface Configuration
interface range F0/22-24
channel-group 1 mode passive
interface port-channel 1
switchport trunk encapsulation dot1q 
switchport mode trunk
ex

interface range F0/22-24
no channel-group 1 mode active
no interface port-channel 1
no switchport trunk encapsulation dot1q 
no switchport mode trunk
ex
```
## HSRP & INTER-VLAN Routing
int vlan 10
ip add 192.168.1.3 255.255.255.224
ip helper-address  192.168.1.110
standby 10 priority 255
standby 10 ip 192.168.1.2
ex

int vlan 20
ip add 192.168.1.35 255.255.255.224
ip helper-address  192.168.1.110
standby 20 priority 200
standby 20 ip 192.168.1.34
ex

int vlan 30
ip add 192.168.1.67 255.255.255.240
ip helper-address  192.168.1.110
standby 20 priority 200
standby 20 ip 192.168.1.66
ex

int f0/8
no switchport 
ip add 192.168.1.89 255.255.255.252
ex
```
## Core Router
en
conf t
int f0/1
ip add 192.168.1.90 255.255.255.252
no shut
ex

int f0/0
ip add 192.168.1.94 255.255.255.252
no shut
ex

int f1/0
ip add 192.168.1.105 255.255.255.252
no shut
ex
```
## ISP Router
int g0/0/0
ip add 192.168.1.97 255.255.255.252
ex

int g0/0/1
ip add 192.168.1.102 255.255.255.252
ex
```
## OSPF Config
### Distribution switch 1
ip routing
router ospf 1
router-id 1.1.1.1
network 192.168.1.92 0.0.0.3 area 0
network 192.168.1.0 0.0.0.31 area 0
network 192.168.1.32 0.0.0.31 area 0
network 192.168.1.64 0.0.0.15 area 0
```
### Distribution switch 2
ip routing
router ospf 1
router-id 2.2.2.2
network 192.168.1.88 0.0.0.3 area 0
network 192.168.1.108 0.0.0.3 area 0
network 192.168.1.0 0.0.0.31 area 0
network 192.168.1.32 0.0.0.31 area 0
network 192.168.1.64 0.0.0.15 area 0
```
### CORE ROUTER
router ospf 1
router-id 3.3.3.3
network 192.168.1.92 0.0.0.3 area 0
network 192.168.1.88 0.0.0.3 area 0
network 192.168.1.104 0.0.0.3 area 0
ex
```
### ISP CORE
router ospf 1
router-id 4.4.4.4
network 192.168.1.96 0.0.0.3 area 0
network 192.168.1.100 0.0.0.3 area 0
ex
```
### IBM Cloud Instance
router ospf 1
router-id 5.5.5.5
network 10.10.1.96 0.0.0.7 area 0
network 192.168.1.100 0.0.0.3 area 0
ex
```
## VOICE VLAN
int fa1/1.30
encapsulation dot1Q 30
ip add 192.168.1.65 255.255.255.240
service dhcp
ip dhcp pool VOICE
network 192.168.1.64 255.255.255.240
default-router 192.168.1.65
option 150 ip 192.168.1.65
ex
telephony-service
max-dn 5
max-ephones 5
auto assign 1 to 10
ip source-address 192.168.1.65 port 2000
ex

ephone-dn 1
number 201
ex

ephone-dn 2
number 202
ex

ephone-dn 3
number 203
ex

ephone-dn 4
number 204
ex

ephone-dn 5
number 205
ex
```
```
