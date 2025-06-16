# OSPF Multi-Area Network Implementation
**Multi-router network with multi-area OSPF routing, departmental VLANs, and security policies**

## Project Overview
Multi-area OSPF network demonstrating hierarchical routing design, network segmentation, and departmental security policies across multiple office locations.

## Network Architecture
**Topology**: Four-router multi-area design with departmental switching
- **R1-Core**: Core distribution router with inter-VLAN routing (Areas 0,1)
- **R2-Gateway**: Internet gateway router with data center services (Areas 0,2)  
- **R3-Branch**: Branch office router with departmental access (Areas 0,3)
- **R4-ISP**: External ISP simulation
- **SW1-Core**: Core departmental switching
- **SW2-Branch**: Branch office switching

## OSPF Area Design
| Area | Purpose | Networks | Router(s) |
|------|---------|----------|-----------|
| 0 | Backbone | WAN Serial Links | All internal routers |
| 1 | Core Office | Dept-A, Management | R1-Core |
| 2 | Data Center | Database Services | R2-Gateway |
| 3 | Branch Office | Dept-B, Dept-C, Management | R3-Branch |

## VLAN Segmentation
| VLAN | Department | Hosts | Subnet | Area |
|------|------------|-------|--------|------|
| 990 | Dept-A | 400 | 145.9.0.0/23 | 1 |
| 902 | Dept-B | 140 | 145.9.2.0/24 | 3 |
| 154 | Dept-C | 68 | 145.9.3.0/25 | 3 |
| 99 | Management | 30 | 145.9.3.128/27, 145.9.3.192/28 | 1,3 |

## Key Technologies
**Routing**: Multi-Area OSPF  
**Switching**: VLANs, 802.1Q Trunking, Port Security  
**Security**: Access Control Lists, Network Segmentation  
**Services**: Static Routing to ISP

## Files Structure
- **`/documentation/`** - Detailed network design and implementation guides
- **`/configs/`** - Complete router and switch configurations
- **`/packet-tracer/`** - Working network simulation file

---
*This project demonstrates practical networking skills in multi-area OSPF design, hierarchical routing, VLANs, and security implementation.*
