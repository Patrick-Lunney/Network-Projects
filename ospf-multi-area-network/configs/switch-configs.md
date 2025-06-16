# Switch Configuration Files

Complete configuration for the access layer switch.

## SW1-Core Configuration

```cisco
hostname SW1-Core
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
 switchport trunk allowed vlan 99,154,902,990
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
 switchport port-security mac-address sticky 0060.4732.C9C2
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
 mac-address 0040.0bed.2201
 ip address 145.9.3.130 255.255.255.224
!
ip default-gateway 145.9.3.129
ip classless
!
ip flow-export version 9
!
banner motd ^C
****************************************
*        SW1-CORE SWITCH ACCESS        *
*      AUTHORISED PERSONNEL ONLY       *
*       Core Distribution Switch       *
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

## SW2-Branch Configuration

```cisco
hostname SW2-Branch
!
enable secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
!
no ip domain-lookup
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
 description Dept-B Workstation 1
 switchport access vlan 902
 switchport mode access
!
interface GigabitEthernet0/1
 description Trunk Link to R3-Branch
 switchport trunk allowed vlan 99,154,902,990
 switchport mode trunk
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan99
 ip address 145.9.3.194 255.255.255.240
!
ip default-gateway 145.9.3.193
!
banner motd ^C
****************************************
*       SW2-BRANCH SWITCH ACCESS       *
*     AUTHORISED  PERSONNEL  ONLY      *
*        Branch Access Switch          *
****************************************
^C
!
line con 0
 password cisco
 logging synchronous
 login
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
