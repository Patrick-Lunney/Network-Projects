# Packet Tracer Simulation Files

## Network Simulation

**File**: `ospf-multi-vlan-network.pkt`

This Packet Tracer file contains the complete working network simulation demonstrating all implemented features.

## What's Included

### Network Devices
- **R1-Core**: Cisco ISR4321 router with inter-VLAN routing
- **R2-Gateway**: Cisco ISR4321 router with NAT/DHCP services  
- **R3-ISP**: Cisco ISR4321 router simulating ISP connectivity
- **SW1-Access**: Cisco Catalyst 3650 switch with VLAN configuration

### End Devices
- **Department A Workstations**: Connected to VLAN 990
- **Department B Workstation**: Connected to VLAN 902
- **Simulated Web Servers**: ISP loopback interfaces

## Functional Features

### Protocols Demonstrated
- **OSPF routing** with neighbor relationships
- **PPP/CHAP authentication** on ISP link
- **802.1Q VLAN trunking** between router and switch
- **DHCP services** with automatic IP assignment
- **NAT overloading** with pool separation

### Security Features
- **Access Control Lists** enforcing department policies
- **Port security** with MAC address learning
- **Password protection** on all management interfaces
- **VLAN segmentation** isolating departmental traffic

## Testing Capabilities

### Connectivity Tests
- **Inter-VLAN communication** with policy restrictions
- **Internet access** through NAT translation
- **Ping tests** to verify ACL enforcement
- **DHCP lease verification** on workstations

### Protocol Verification
- **OSPF neighbor states** and routing table inspection
- **NAT translation tables** showing address mapping
- **VLAN assignments** and trunk operation
- **Port security status** and learned MAC addresses

## Usage Instructions

1. **Open the file** in Cisco Packet Tracer (version 8.0 or later recommended)
2. **Test connectivity** by pinging between devices from different VLANs
3. **Use CLI commands** to verify protocol operation and routing
4. **Modify configurations** to experiment with different scenarios

## Network Topology

The simulation demonstrates a realistic small enterprise network with:
- **Hierarchical design** with core and access layers
- **Departmental segmentation** using VLANs
- **Centralised services** for DHCP and internet access
- **Security policies** controlling inter-department communication

---

*This simulation provides hands-on experience with enterprise networking protocols and configuration in a controlled lab environment.*
