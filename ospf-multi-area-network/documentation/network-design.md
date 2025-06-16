# Network Design Documentation

## Project Overview

This project implements a multi-area OSPF network demonstrating hierarchical routing design, departmental VLAN segmentation, and security policies across multiple network areas.

## Network Topology

**Architecture**: Four-router multi-area design with departmental switching
- **R1-Core**: Core distribution router with inter-VLAN routing
- **R2-Gateway**: Internet gateway router with data center services
- **R3-Branch**: Branch office router with departmental access
- **R4-ISP**: External ISP simulation with service networks
- **SW1-Core**: Core departmental switching with VLAN segmentation
- **SW2-Branch**: Branch office switching with departmental access

## IP Addressing Scheme (VLSM Implementation)

### Corporate Network: 145.9.0.0/16

| Network | VLAN | Department | Hosts Needed | Hosts Available | Subnet | Subnet Mask | Gateway |
|---------|------|------------|--------------|-----------------|--------|-------------|---------|
| 145.9.0.0/23 | 990 | Dept-A | 400 | 510 | 145.9.0.0 | 255.255.254.0 | 145.9.0.1 |
| 145.9.2.0/24 | 902 | Dept-B | 140 | 254 | 145.9.2.0 | 255.255.255.0 | 145.9.2.1 |
| 145.9.3.0/25 | 154 | Dept-C | 68 | 126 | 145.9.3.0 | 255.255.255.128 | 145.9.3.1 |
| 145.9.3.128/27 | 99 | Management (Core) | 18 | 30 | 145.9.3.128 | 255.255.255.224 | 145.9.3.129 |
| 145.9.3.160/27 | - | Database Server LAN | 18 | 30 | 145.9.3.160 | 255.255.255.224 | 145.9.3.161 (Lo0) |
| 145.9.3.192/28 | 99 | Management (Branch) | 12 | 14 | 145.9.3.192 | 255.255.255.240 | 145.9.3.193 |

### WAN Serial Links
- **R1-Core to R2-Gateway**: 145.9.3.208/30
- **R1-Core to R3-Branch**: 145.9.3.212/30
- **R2-Gateway to R3-Branch**: 145.9.3.216/30

### External Networks
- **ISP Link**: 211.11.52.0/30
- **ISP Services**: 182.18.0.0/16, 121.0.0.0/8, 141.66.0.0/16, 217.2.45.0/24

## Protocol Implementation

### Multi-Area OSPF
- **Process ID**: 1
- **Area 0 (Backbone)**: All WAN serial links between internal routers
- **Area 1 (Core Office)**: R1-Core departmental networks (Dept-A, Management)
- **Area 2 (Data Center)**: R2-Gateway database services (Loopback0)
- **Area 3 (Branch Office)**: R3-Branch departmental networks (Dept-B, Dept-C, Management)
- **Passive Interfaces**: All VLAN interfaces
- **Active Interfaces**: Serial links between routers only
- **Default Route**: Distributed from R2-Gateway
- **Bandwidth Tuning**: Serial links configured for optimal path selection

### VLAN Configuration
- **Trunking**: 802.1Q between routers and switches
- **Management VLAN**: VLAN 99 (VLAN 1 shutdown for security)
- **Access Ports**: Configured with departmental VLAN assignments
- **Trunk Optimization**: Only active VLANs allowed on trunk ports

### Static Routing
- **Gateway Router**: R2-Gateway with default route to ISP
- **ISP Return Route**: Static route to corporate network (145.9.0.0/16)
- **OSPF Distribution**: Default route advertised to all internal areas

## Security Implementation

### Access Control Lists (ACLs)

#### Dept-A Security Policy (DEPT-A-ACL)
- **HTTP Access**: Permitted to ISP web server (182.18.0.0/16) only
- **Internet Restrictions**: All other access to ISP web server (182.18.0.0/16) denied
- **Inter-Department**: Can receive ping replies from Dept-B (when Dept-A initiates)
- **General Internet**: Full access permitted to other networks

#### Dept-B Security Policy (DEPT-B-PING-BLOCK)
- **Inter-Department**: Cannot initiate pings to Dept-A networks
- **General Access**: Full access to all other networks

#### Management Access Control
- **Telnet Access**: Dept-A users can access R1-Core only
- **Administrative Restriction**: Dept-A users denied telnet to R2-Gateway
- **Console Access**: Protected with passwords on all devices

### Port Security
- **MAC Address Learning**: Sticky configuration on Dept-A access ports
- **Maximum Devices**: 4 per port
- **Violation Action**: Protect (drop unauthorized frames)
- **Applied Ports**: Dept-A access ports (Gi1/0/13, Gi1/0/14)

### Password Security
- **Enable Secret**: Configured on all devices
- **Console Access**: Password protected
- **VTY Lines**: Password protected with transport restrictions
- **Line Security**: Telnet-only transport configured

## Verification and Testing

### Connectivity Testing
- **Inter-Area Routing**: Verified between all OSPF areas
- **Internet Access**: Confirmed with appropriate restrictions
- **VLAN Isolation**: Proper segmentation between departments

### Protocol Verification
- **OSPF Neighbors**: All expected adjacencies established
- **Route Learning**: Inter-area routes propagated correctly
- **Area Separation**: OSPF database contains appropriate area information
- **Default Route**: Distributed throughout internal network

### Security Verification
- **ACL Enforcement**: Traffic restrictions working as designed
- **Port Security**: MAC address learning and violation protection active
- **Management Access**: Telnet restrictions enforced

## Design Rationale

### Multi-Area OSPF Design
- **Hierarchical Structure**: Clear area boundaries for scalability
- **Backbone Area**: WAN links form Area 0 for optimal routing
- **Area Segmentation**: Departmental networks isolated by function and location

### Security Implementation
- **ACL-based Policies**: Granular control over inter-department access
- **Management VLAN Separation**: Administrative traffic isolated from user VLANs
- **VLAN 1 Mitigation**: Default VLAN disabled for security best practices

---

*This network demonstrates practical networking skills in multi-area OSPF design, hierarchical routing, VLAN segmentation, and security implementation using standard networking protocols.*
