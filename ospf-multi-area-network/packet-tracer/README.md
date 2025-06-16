# Packet Tracer Simulation Files

## Network Simulation

**File**: `ospf-multi-area-network.pkt`

This Packet Tracer file contains the complete working multi-area OSPF network simulation demonstrating hierarchical routing design and departmental segmentation.

## What's Included

### Network Devices
* **R1-Core**: Cisco ISR4321 router with inter-VLAN routing (Areas 0,1)
* **R2-Gateway**: Cisco ISR4321 router with internet gateway services (Areas 0,2)
* **R3-Branch**: Cisco ISR4321 router with branch office connectivity (Areas 0,3)
* **R4-ISP**: Cisco ISR4321 router simulating ISP connectivity
* **SW1-Core**: Cisco Catalyst 3650 switch with core departmental VLANs
* **SW2-Branch**: Cisco Catalyst 2960 switch with branch office VLANs

### End Devices
* **Dept-A Workstations**: Connected to VLAN 990 (Core office)
* **Dept-B Workstation**: Connected to VLAN 902 (Branch office)
* **Simulated Web Servers**: ISP loopback interfaces

## Functional Features

### Protocols Demonstrated
* **Multi-Area OSPF** with Area 0 backbone and Areas 1,2,3
* **Area Border Routers** connecting multiple OSPF areas
* **802.1Q VLAN trunking** between routers and switches
* **Static routing** for ISP connectivity
* **Inter-area route summarisation** and LSA propagation

### Security Features
* **Access Control Lists** enforcing departmental policies
* **Port security** with MAC address learning on access ports
* **Password protection** on all management interfaces
* **VLAN segmentation** isolating departmental traffic
* **Management VLAN** separation (VLAN 99)

## Testing Capabilities

### Connectivity Tests
* **Inter-area communication** between OSPF areas
* **Internet access** through gateway router
* **Ping tests** to verify ACL enforcement
* **VLAN isolation** between departments

### Protocol Verification
* **OSPF neighbor states** and area adjacencies
* **OSPF database** showing area-specific LSAs
* **Inter-area routing** (O IA routes) in routing tables
* **Default route distribution** throughout areas
* **VLAN assignments** and trunk operation
* **Port security status** and learned MAC addresses

## Usage Instructions

1. **Open the file** in Cisco Packet Tracer (version 8.0 or later recommended)
2. **Test connectivity** by pinging between devices in different areas
3. **Use CLI commands** to verify OSPF operation and area separation
4. **Examine routing tables** to see inter-area route propagation
5. **Modify configurations** to experiment with different area designs

## Network Topology

The simulation demonstrates a realistic multi-location enterprise network with:
* **Multi-area OSPF design** with hierarchical area structure
* **Area-based segmentation** for scalability and performance
* **Departmental VLANs** across multiple locations
* **Centralised internet gateway** with static routing to ISP
* **Security policies** controlling inter-department communication

*This simulation provides hands-on experience with advanced OSPF concepts, area design, and enterprise network segmentation in a controlled lab environment.*
