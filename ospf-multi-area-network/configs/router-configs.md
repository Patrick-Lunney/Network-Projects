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
 no ip address
 duplex auto
 speed auto
!
interface GigabitEthernet0/0/1.99
 description Management VLAN
 encapsulation dot1Q 99
 ip address 145.9.3.129 255.255.255.224
!
interface GigabitEthernet0/0/1.990
 description Dept-A VLAN
 encapsulation dot1Q 990
 ip address 145.9.0.1 255.255.254.0
 ip access-group DEPT-A-ACL in
!
interface Serial0/1/0
 description Link to R3-Branch
 bandwidth 512
 ip address 145.9.3.213 255.255.255.252
!
interface Serial0/1/1
 description Link to R2-Gateway
 bandwidth 128
 ip address 145.9.3.209 255.255.255.252
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
 no passive-interface Serial0/1/1
 network 145.9.3.208 0.0.0.3 area 0
 network 145.9.3.212 0.0.0.3 area 0
 network 145.9.0.0 0.0.1.255 area 1
 network 145.9.3.128 0.0.0.31 area 1
!
ip classless
!
ip flow-export version 9
!
ip access-list extended DEPT-A-ACL
 permit tcp 145.9.0.0 0.0.1.255 182.18.0.0 0.0.255.255 eq www
 deny ip 145.9.0.0 0.0.1.255 182.18.0.0 0.0.255.255
 permit ip any any
ip access-list standard TELNET-R1-CORE
 permit 145.9.0.0 0.0.1.255
 deny any
!
banner motd ^C
****************************************
*        R1-CORE ROUTER ACCESS         *
*      AUTHORISED PERSONNEL ONLY       *
*       Core Distribution Router       *
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
ip cef
no ipv6 cef
!
no ip domain-lookup
!
spanning-tree mode pvst
!
interface Loopback0
 description Database Server LAN
 ip address 145.9.3.161 255.255.255.224
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
 bandwidth 128
 ip address 145.9.3.210 255.255.255.252
 clock rate 2000000
!
interface Serial0/1/1
 description Link to R3-Branch
 bandwidth 512
 ip address 145.9.3.217 255.255.255.252
!
interface Serial0/2/0
 description Link to R4-ISP
 ip address 211.11.52.1 255.255.255.252
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
 no passive-interface Serial0/1/1
 network 145.9.3.208 0.0.0.3 area 0
 network 145.9.3.216 0.0.0.3 area 0
 network 145.9.3.160 0.0.0.31 area 2
 default-information originate
!
ip classless
ip route 0.0.0.0 0.0.0.0 211.11.52.2 
!
ip flow-export version 9
!
ip access-list standard TELNET-R2-GATEWAY
 deny 145.9.0.0 0.0.1.255
 permit any
!
banner motd ^C
****************************************
*       R2-GATEWAY ROUTER ACCESS       *
*      AUTHORISED PERSONNEL ONLY       *
*      Internet Gateway Router         *
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

## R3-Branch Configuration

```cisco
hostname R3-Branch
!
enable secret cisco
!
ip cef
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
 no ip address
 duplex auto
 speed auto
!
interface GigabitEthernet0/0/1.99
 description Management VLAN
 encapsulation dot1Q 99
 ip address 145.9.3.193 255.255.255.240
!
interface GigabitEthernet0/0/1.154
 description Dept-C VLAN
 encapsulation dot1Q 154
 ip address 145.9.3.1 255.255.255.128
!
interface GigabitEthernet0/0/1.902
 description Dept-B VLAN
 encapsulation dot1Q 902
 ip address 145.9.2.1 255.255.255.0
 ip access-group DEPT-B-PING-BLOCK in
!
interface Serial0/1/0
 description Link to R1-Core
 bandwidth 512
 ip address 145.9.3.214 255.255.255.252
 clock rate 2000000
!
interface Serial0/1/1
 description Link to R2-Gateway
 bandwidth 512
 ip address 145.9.3.218 255.255.255.252
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
 no passive-interface Serial0/1/1
 network 145.9.3.212 0.0.0.3 area 0
 network 145.9.3.216 0.0.0.3 area 0
 network 145.9.2.0 0.0.0.255 area 3
 network 145.9.3.0 0.0.0.127 area 3
 network 145.9.3.192 0.0.0.15 area 3
!
ip classless
!
ip flow-export version 9
!
ip access-list extended DEPT-B-PING-BLOCK
 deny icmp 145.9.2.0 0.0.0.255 145.9.0.0 0.0.1.255 echo
 permit ip any any
!
banner motd ^C
****************************************
*       R3-BRANCH ROUTER ACCESS        *
*      AUTHORISED PERSONNEL ONLY       *
*        Branch Office Router          *
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

## R4-ISP Configuration

```cisco
hostname R4-ISP
!
enable secret cisco
!
ip cef
no ipv6 cef
!
no ip domain-lookup
!
spanning-tree mode pvst
!
interface Loopback0
 description External Server 1
 ip address 182.18.0.1 255.255.0.0
!
interface Loopback1
 description External Server 2
 ip address 121.0.0.1 255.0.0.0
!
interface Loopback2
 description External Network 1
 ip address 141.66.0.1 255.255.0.0
!
interface Loopback3
 description External Network 2
 ip address 217.2.45.1 255.255.255.0
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
 description Link to R2-Gateway
 ip address 211.11.52.2 255.255.255.252
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
ip classless
ip route 145.9.0.0 255.255.0.0 211.11.52.1 
!
ip flow-export version 9
!
banner motd ^C
****************************************
*         R4-ISP ROUTER ACCESS         *
*      AUTHORISED PERSONNEL ONLY       *
*       Internet Service Provider      *
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
