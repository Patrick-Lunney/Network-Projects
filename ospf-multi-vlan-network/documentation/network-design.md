# Network Design Documentation

## Project Overview

This project implements a multi-VLAN network demonstrating core networking concepts including dynamic routing, network segmentation, security policies, and centralised services.

## Network Topology

**Architecture**: Three-router hierarchical design with centralised switching
- **R1-Core**: Inter-VLAN routing and internal connectivity
- **R2-Gateway**: Internet gateway with NAT and DHCP services
- **R3-ISP**: External ISP simulation with web servers
- **SW1-Access**: Departmental access switching with VLAN segmentation

## IP Addressing Scheme (VLSM Implementation)

### Corporate Network: 99.0.0.0/8

| Network | VLAN | Department | Hosts Needed | Hosts Available | Subnet | Subnet Mask | Gateway |
|---------|------|------------|--------------|-----------------|--------|-------------|---------|
| 99.0.0.0/22 | 990 | Department A | 800 | 1022 | 99.0.0.0 | 255.255.252.0 | 99.0.0.1 |
| 99.0.4.0/24 | 902 | Department B | 200 | 254 | 99.0.4.0 | 255.255.255.0 | 99.0.4.1 |
| 99.0.5.0/25 | 516 | Department C | 120 | 126 | 99.0.5.0 | 255.255.255.128 | 99.0.5.1 |
| 99.0.5.128/27 | - | Database Server LAN | 20 | 30 | 99.0.5.128 | 255.255.255.224 | 99.0.5.129 (Loopback) |
| 99.0.5.160/29 | 99 | Management | 6 | 6 | 99.0.5.160 | 255.255.255.248 | 99.0.5.161 |
| 99.0.5.168/30 | - | Internal Serial Link | 2 | 2 | 99.0.5.168 | 255.255.255.252 | - |

### External Networks
- **ISP Link**: 191.22.42.0/30
- **NAT Pool**: 135.12.64.0/25 (split into 3 equal pools)

## Protocol Implementation

### OSPF (Open Shortest Path First)
- **Process ID**: 1
- **Area**: 0 (backbone area)
- **Networks Advertised**: All internal corporate networks
- **Passive Interfaces**: All VLAN interfaces
- **Active Interfaces**: Serial links between routers only
- **Default Route**: Distributed from R2-Gateway
- **Bandwidth Tuning**: Serial links configured for optimal path selection

### VLAN Configuration
- **Trunking**: 802.1Q between R1-Core and SW1-Access
- **Management VLAN**: VLAN 99 (not default VLAN 1)
- **Access Ports**: Configured with port security (sticky MAC learning)
- **Port Security**: Maximum 4 devices, violation protection enabled

### DHCP Services
- **Server Location**: R2-Gateway (centralised)
- **Pools**: Department A and Department B networks
- **Exclusions**: Gateway addresses (.1-.4 reserved)
- **Helper Addresses**: Configured on R1-Core for cross-VLAN DHCP

### NAT Implementation
- **Type**: NAT Overloading (PAT)
- **Pool Division**: 135.12.64.0/25 split into 3 equal pools without VLSM
  - Management: 135.12.64.1-42
  - Department A: 135.12.64.43-84  
  - Department B: 135.12.64.85-126
- **Inside Interfaces**: All internal networks
- **Outside Interface**: Serial link to ISP

### PPP/CHAP Authentication
- **Location**: WAN link between R2-Gateway and R3-ISP
- **Protocol**: Point-to-Point Protocol with Challenge-Handshake Authentication
- **Security**: Mutual authentication between gateway and ISP
- **Purpose**: Secure ISP connectivity with subscriber authentication

## Security Implementation

### Access Control Lists (ACLs)

#### Department A Security Policy (DEPT-A-ACL)
- **HTTP Access**: Permitted to ISP web server (154.3.0.0/16) only
- **Internet Restrictions**: All other access to ISP web server (154.3.0.0/16) denied
- **Inter-Department**: Can receive ping replies from Department B
- **Inter-Department**: Cannot initiate pings to Department B
- **General Internet**: Full access permitted

#### Department B Security Policy (DEPT-B-ACL)  
- **Database Access**: Denied access to Database Server LAN (99.0.5.128/27)
- **Internet Access**: Full internet access permitted
- **Inter-Department**: Can ping Department A (asymmetric policy)

#### Management Access Control
- **Telnet Access**: Department A users can access R1-Core only
- **Administrative Restriction**: Department A users denied telnet to R2-Gateway
- **Console Access**: Protected with passwords on all devices

### Port Security
- **MAC Address Learning**: Sticky configuration
- **Maximum Devices**: 4 per port
- **Violation Action**: Protect (drop unauthorised frames)
- **Applied Ports**: Department A access ports (G1/0/13, G1/0/14)

### Password Security
- **Enable Secret**: Configured on all devices
- **Console Access**: Password protected
- **VTY Lines**: Password protected with transport restrictions
- **Line Security**: Telnet-only transport (SSH can be added in production)

## Verification and Testing

### Connectivity Testing
- **Inter-VLAN Routing**: Verified between all departments
- **Internet Access**: Confirmed with appropriate restrictions
- **DHCP Functionality**: Automatic IP assignment working
- **NAT Translation**: Verified with show commands

### Protocol Verification
- **OSPF Neighbors**: All expected adjacencies established
- **Route Learning**: Internal routes propagated correctly
- **Default Route**: Distributed throughout internal network
- **CHAP Authentication**: Successful ISP link establishment

### Security Verification
- **ACL Enforcement**: Traffic restrictions working as designed
- **Port Security**: MAC address learning and violation protection active
- **Management Access**: Telnet restrictions enforced

## Design Rationale

### Network Design Decisions
- **VLSM Implementation**: Efficient IP address allocation for varying department sizes
- **Single OSPF Area**: Appropriate for network scope, reduces complexity
- **Centralised Services**: DHCP and NAT on gateway router for easier management
- **VLAN Segmentation**: Isolates departmental traffic and enables targeted security policies

### Security Implementation
- **ACL-based Policies**: Granular control over inter-department and internet access
- **Management VLAN Separation**: Administrative traffic isolated from user VLANs
- **Authentication**: PPP/CHAP provides ISP link security

---

*This network demonstrates practical networking skills including routing protocols, VLANs, security policies, and service configuration using production networking concepts.*
