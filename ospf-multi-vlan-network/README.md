# OSPF Multi-VLAN Network Implementation

**Multi-router network with OSPF routing, departmental VLANs, security policies, and ISP connectivity**

## Project Overview

Multi-VLAN network demonstrating core networking concepts including dynamic routing, network segmentation, security policies, and centralized services.

## Network Architecture

**Topology**: Three-router hierarchical design with access switching
- **R1-Core**: Inter-VLAN routing and OSPF distribution
- **R2-Gateway**: Internet connectivity with NAT and DHCP services  
- **R3-ISP**: External ISP simulation
- **SW1-Access**: Departmental VLAN switching

## VLAN Segmentation

| VLAN | Department | Hosts | Subnet |
|------|------------|-------|--------|
| 990 | Department A | 800 | 99.0.0.0/22 |
| 902 | Department B | 200 | 99.0.4.0/24 |
| 516 | Department C | 120 | 99.0.5.0/25 |
| 99 | Management | 6 | 99.0.5.160/29 |

## Key Technologies

**Routing**: OSPF  
**Switching**: VLANs, 802.1Q Trunking, Port Security  
**Security**: Access Control Lists, Network Segmentation  
**Services**: DHCP, NAT/PAT, PPP/CHAP Authentication

## Files Structure

- **`/documentation/`** - Detailed network design and implementation guides
- **`/configs/`** - Complete router and switch configurations
- **`/packet-tracer/`** - Working network simulation file

---

*This project demonstrates practical networking skills in routing protocols, VLANs, security implementation, and service configuration.*
