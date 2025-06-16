# Router Configuration Files

Complete configuration files for all routers in the network.

## R1-Core Configuration

```cisco
hostname R1-Core
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
interface GigabitEthernet0/0/0
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/0/1
 description Trunk Link to SW1-Access
 no ip address
 duplex auto
 speed auto
!
interface GigabitEthernet0/0/1.99
 description Management VLAN
 encapsulation dot1Q 99
 ip address 99.0.5.161 255.255.255.248
!
interface GigabitEthernet0/0/1.516
 description Dept-C VLAN
 encapsulation dot1Q 516
 ip address 99.0.5.1 255.255.255.128
!
interface GigabitEthernet0/0/1.902
 description Dept-B VLAN
 encapsulation dot1Q 902
 ip address 99.0.4.1 255.255.255.0
 ip helper-address 99.0.5.129
 ip access-group DEPT-B-ACL in
!
interface GigabitEthernet0/0/1.990
 description Dept-A VLAN
 encapsulation dot1Q 990
 ip address 99.0.0.1 255.255.255.0
 ip helper-address 99.0.5.129
 ip access-group DEPT-A-ACL in
!
interface Serial0/1/0
 description Link to R2-Gateway
 bandwidth 256
 ip address 99.0.5.169 255.255.255.252
 clock rate 2000000
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/2/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/2/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 1
 log-adjacency-changes
 passive-interface default
 no passive-interface Serial0/1/0
 network 99.0.0.0 0.0.3.255 area 0
 network 99.0.4.0 0.0.0.255 area 0
 network 99.0.5.0 0.0.0.127 area 0
 network 99.0.5.160 0.0.0.7 area 0
 network 99.0.5.168 0.0.0.3 area 0
!
ip classless
!
ip flow-export version 9
!
ip access-list extended DEPT-A-ACL
 permit tcp 99.0.0.0 0.0.3.255 154.3.0.0 0.0.255.255 eq www
 deny ip 99.0.0.0 0.0.3.255 154.3.0.0 0.0.255.255
 permit icmp 99.0.0.0 0.0.3.255 99.0.4.0 0.0.0.255 echo-reply
 deny icmp 99.0.0.0 0.0.3.255 99.0.4.0 0.0.0.255 echo
 permit ip any any
ip access-list extended DEPT-B-ACL
 deny ip 99.0.4.0 0.0.0.255 99.0.5.128 0.0.0.31
 permit ip any any
ip access-list standard TELNET-R1-CORE
 permit 99.0.0.0 0.0.3.255
!
banner motd ^C
****************************************
*        R1-CORE ROUTER ACCESS         *
*      AUTHORISED PERSONNEL ONLY       *
*    Network Infrastructure Device     *
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
 access-class TELNET-R1-CORE in
 password cisco
 login
 transport input telnet
!
end
```

## R2-Gateway Configuration

```cisco
hostname R2-Gateway
!
enable secret cisco
!
ip dhcp excluded-address 99.0.0.1 99.0.0.4
ip dhcp excluded-address 99.0.4.1 99.0.4.4
!
ip dhcp pool DEPT-A-VLAN
 network 99.0.0.0 255.255.252.0
 default-router 99.0.0.1
ip dhcp pool DEPT-B-VLAN
 network 99.0.4.0 255.255.255.0
 default-router 99.0.4.1
!
ip cef
no ipv6 cef
!
username R3-ISP password 0 cisco
!
no ip domain-lookup
!
spanning-tree mode pvst
!
interface Loopback0
 description Database Server LAN
 ip address 99.0.5.129 255.255.255.224
 ip nat inside
!
interface GigabitEthernet0/0/0
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 description Link to R1-Core
 bandwidth 256
 ip address 99.0.5.170 255.255.255.252
 ip nat inside
!
interface Serial0/1/1
 description Link to R3-ISP
 ip address 191.22.42.1 255.255.255.252
 encapsulation ppp
 ppp authentication chap
 ip nat outside
 clock rate 2000000
!
interface Serial0/2/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/2/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 1
 log-adjacency-changes
 passive-interface default
 no passive-interface Serial0/1/0
 network 99.0.5.128 0.0.0.31 area 0
 network 99.0.5.168 0.0.0.3 area 0
 default-information originate
!
ip nat pool DEPT-A-POOL 135.12.64.43 135.12.64.84 netmask 255.255.255.128
ip nat pool DEPT-B-POOL 135.12.64.85 135.12.64.126 netmask 255.255.255.128
ip nat pool MGMT-POOL 135.12.64.1 135.12.64.42 netmask 255.255.255.128
ip nat inside source list DEPT-A-NAT pool DEPT-A-POOL overload
ip nat inside source list DEPT-B-NAT pool DEPT-B-POOL overload
ip nat inside source list MGMT-NAT pool MGMT-POOL overload
ip classless
ip route 0.0.0.0 0.0.0.0 191.22.42.2 
!
ip flow-export version 9
!
ip access-list extended MGMT-NAT
 permit ip 99.0.5.160 0.0.0.7 any
ip access-list extended DEPT-A-NAT
 permit ip 99.0.0.0 0.0.3.255 any
ip access-list extended DEPT-B-NAT
 permit ip 99.0.4.0 0.0.0.255 any
ip access-list standard TELNET-R2-GATEWAY
 deny 99.0.0.0 0.0.3.255
 permit any
!
banner motd ^C
****************************************
*       R2-GATEWAY ROUTER ACCESS       *
*      AUTHORISED PERSONNEL ONLY       *
*       Internet Gateway Device        *
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
 access-class TELNET-R2-GATEWAY in
 password cisco
 login
 transport input telnet
!
end
```
## R3-ISP Configuration

```cisco
hostname R3-ISP
!
enable secret cisco
!
ip cef
no ipv6 cef
!
username R2-Gateway password 0 cisco
!
no ip domain-lookup
!
spanning-tree mode pvst
!
interface Loopback0
 description External Web Server 1
 ip address 154.3.0.1 255.255.0.0
!
interface Loopback1
 description External Web Server 2
 ip address 18.0.0.1 255.0.0.0
!
interface Loopback2
 description External Web Server 3
 ip address 162.55.0.1 255.255.0.0
!
interface Loopback3
 description External Web Server 4
 ip address 201.12.80.1 255.255.255.0
!
interface GigabitEthernet0/0/0
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/1/1
 description Link to R2-Gateway
 ip address 191.22.42.2 255.255.255.252
 encapsulation ppp
 ppp authentication chap
!
interface Serial0/2/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/2/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
ip route 135.12.64.0 255.255.255.128 191.22.42.1 
!
ip flow-export version 9
!
banner motd ^C
****************************************
*        R3-ISP ROUTER ACCESS          *
*      AUTHORISED PERSONNEL ONLY       *
*       External ISP Simulation        *
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
!
end
```
