# Switch Configuration Files

Complete configuration for the access layer switch.

## SW1-Access Configuration

```cisco
hostname SW1-Access
!
enable secret cisco
!
no ip cef
no ipv6 cef
!
no ip domain-lookup
!
spanning-tree mode pvst
!
interface GigabitEthernet1/0/1
!
interface GigabitEthernet1/0/2
!
interface GigabitEthernet1/0/3
!
interface GigabitEthernet1/0/4
!
interface GigabitEthernet1/0/5
!
interface GigabitEthernet1/0/6
!
interface GigabitEthernet1/0/7
!
interface GigabitEthernet1/0/8
!
interface GigabitEthernet1/0/9
!
interface GigabitEthernet1/0/10
!
interface GigabitEthernet1/0/11
 description Trunk Link to R1-Core
 switchport trunk allowed vlan 99,516,902,990
 switchport mode trunk
!
interface GigabitEthernet1/0/12
!
interface GigabitEthernet1/0/13
 description Dept-A Workstation 1
 switchport access vlan 990
 switchport mode access
 switchport port-security
 switchport port-security maximum 4
 switchport port-security mac-address sticky 
 switchport port-security violation protect 
 switchport port-security mac-address sticky 00D0.BA3B.3C8B
!
interface GigabitEthernet1/0/14
 description Dept-A Workstation 2
 switchport access vlan 990
 switchport mode access
 switchport port-security
 switchport port-security maximum 4
 switchport port-security mac-address sticky 
 switchport port-security violation protect 
!
interface GigabitEthernet1/0/15
!
interface GigabitEthernet1/0/16
!
interface GigabitEthernet1/0/17
!
interface GigabitEthernet1/0/18
!
interface GigabitEthernet1/0/19
!
interface GigabitEthernet1/0/20
!
interface GigabitEthernet1/0/21
!
interface GigabitEthernet1/0/22
!
interface GigabitEthernet1/0/23
!
interface GigabitEthernet1/0/24
 description Dept-B Workstation
 switchport access vlan 902
 switchport mode access
!
interface GigabitEthernet1/1/1
!
interface GigabitEthernet1/1/2
!
interface GigabitEthernet1/1/3
!
interface GigabitEthernet1/1/4
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan99
 mac-address 0060.2f2a.1b01
 ip address 99.0.5.162 255.255.255.248
!
ip default-gateway 99.0.5.161
ip classless
!
ip flow-export version 9
!
banner motd ^C
****************************************
*       SW1-ACCESS SWITCH ACCESS       *
*      AUTHORISED PERSONNEL ONLY       *
*      Departmental Access Switch      *
****************************************
^C
!
line con 0
 password cisco
 logging synchronous
 login
!
line aux 0
!
line vty 0 4
 password cisco
 login
 transport input telnet
line vty 5 15
 password cisco
 login
 transport input telnet
!
end
```
