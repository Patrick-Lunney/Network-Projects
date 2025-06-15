# OSPF Multi-VLAN Network Implementation

**Multi-router network with OSPF routing, departmental VLANs, security policies, and ISP connectivity**

## Project Overview

Designed and implemented a scalable network infrastructure supporting multiple departments with secure inter-VLAN routing, centralized services, and internet connectivity. The solution demonstrates enterprise networking concepts including dynamic routing protocols, network segmentation, and comprehensive security policies.

## Network Architecture

**Topology**: Three-router network with hierarchical design
- **Core Router**: Central OSPF routing and inter-VLAN services
- **Gateway Router**: Internet connectivity with NAT and DHCP services  
- **ISP Router**: External connectivity simulation

**Address Space**: 99.0.0.0/8 corporate network with VLSM subnetting  
**WAN Connection**: 191.22.42.0/30 with PPP/CHAP authentication

## VLAN Segmentation

| VLAN | Department | Hosts | Subnet | Subnet Mask |
|------|------------|-------|--------|-------------|
| 990 | Department A | 800 | 99.0.0.0/22 | 255.255.252.0 |
| 902 | Department B | 200 | 99.0.4.0/24 | 255.255.255.0 |
| 516 | Department C | 120 | 99.0.5.0/25 | 255.255.255.128 |
| 1 | Management | 6 | 99.0.5.160/29 | 255.255.255.248 |

**Additional Networks**:
- Database Server LAN: 99.0.5.128/27 (20 hosts)
- Internal Serial Link: 99.0.5.168/30
- ISP Connection: 191.22.42.0/30

## Technical Implementation

### Routing Protocol (OSPF)
- Dynamic route advertisement for all internal networks
- Bandwidth optimization for serial links (256 kbps)
- Default route distribution from gateway router
- Broadcast suppression on edge networks

### Security Features
- **Access Control Lists**: Department-specific internet access policies
- **Port Security**: MAC address learning with violation protection
- **Telnet Access Control**: Administrative access restrictions
- **Database Protection**: Isolated server access policies

### Network Services
- **DHCP**: Centralized IP allocation for workstation VLANs
- **NAT Overloading**: Public IP sharing with departmental pools
- **Inter-VLAN Routing**: 802.1Q trunk-based routing
- **PPP/CHAP**: Secure ISP authentication

## Key Features Demonstrated

**VLSM Subnetting**: Efficient IP address allocation using Variable Length Subnet Masking  
**OSPF Configuration**: Dynamic routing with area design and route optimization  
**Security Policies**: Granular access controls for network segmentation  
**WAN Connectivity**: Point-to-Point Protocol with authentication  
**Network Services**: DHCP automation and NAT implementation

## Files Structure

- **`/documentation/`** - Network design specifications and configuration guides
- **`/configs/`** - Complete router and switch configuration files
- **`/packet-tracer/`** - Working network simulation demonstrating all functionality

## Technologies Used

**Routing**: OSPF (Open Shortest Path First)  
**Switching**: VLANs, 802.1Q Trunking, Port Security  
**Security**: Access Control Lists, Network Segmentation  
**WAN**: PPP, CHAP Authentication, Serial Links  
**Services**: DHCP, NAT/PAT, DNS Resolution  
**Hardware**: Cisco ISR4321 Routers, Catalyst 2960/3650 Switches

## Verification Results

All network functionality tested and verified:
- ✅ OSPF route convergence and neighbor relationships
- ✅ Inter-VLAN connectivity and traffic isolation
- ✅ DHCP automatic IP assignment and exclusions
- ✅ Internet access with NAT translation
- ✅ Security policy enforcement via ACLs
- ✅ PPP/CHAP authentication between routers
- ✅ Port security and MAC address learning

---

*This project demonstrates practical implementation of enterprise networking protocols and security measures commonly used in production environments.*
