# **LAB 4** ~ Campus Network Design and Implementation

A multi-campus university network designed and implemented using **Cisco Packet Tracer**, featuring VLAN segmentation, inter-VLAN routing, RIPv2, static routing, DHCP, and internal/external server connectivity.

---

## 1. Project Overview

This project focuses on designing and implementing a scalable campus network infrastructure for **Albion University**, which operates across two campuses located approximately 20 miles apart.

The network connects multiple faculties, administrative departments, student laboratories, IT infrastructure, and external cloud-hosted services.

The main objective is to establish reliable communication between departments and campuses while maintaining proper network segmentation, efficient IP address management, and network security.

**Platform:** Cisco Packet Tracer  
**Project Type:** Enterprise / Campus Network Design  
**Network Type:** Multi-Campus Network

---

## 2. Case Study

The following image contains the original case study and network requirements.

![Albion University Case Study](screenshots/case-study.png)

---

## 3. Network Architecture

The network consists of two campuses and an external cloud network.

### Main Campus

**Building A - Administration and Business**
- Management department
- Human Resources department
- Finance department
- Faculty of Business
- Separate VLANs for each department
- Router-based DHCP for automatic IP allocation

**Building B - Engineering and Design**
- Faculty of Engineering and Computing
- Faculty of Art and Design
- Dedicated VLANs for departmental network segmentation

**Building C - IT and Student Facilities**
- Student computer laboratories
- IT department
- Internal university web server
- Additional internal servers

### Branch Campus

The smaller campus accommodates the Faculty of Health and Sciences.

- Dedicated staff network
- Separate student laboratory network
- Independent VLANs and IP subnets
- Connectivity to the main campus through WAN links

### External Cloud Network

- External cloud network connectivity
- University email server hosted externally
- Static routing for external server communication

---

## 4. Key Features

- **VLAN Segmentation:** Separate VLANs for individual departments and faculties.
- **Inter-VLAN Routing:** Enables communication between different departmental networks.
- **RIPv2 Dynamic Routing:** Exchanges routing information between internal campus routers.
- **Static Routing:** Establishes connectivity with the external cloud network.
- **DHCP Configuration:** Automatically assigns IP addresses to devices in Building A.
- **Trunk Links:** Carry multiple VLANs between network devices.
- **Network Security:** Implements VLAN isolation and appropriate switch security settings.
- **Multi-Campus Connectivity:** Connects the main and branch campuses.
- **Internal Web Server:** Hosts university web services.
- **External Email Server:** Provides email services through the cloud.
- **Network Scalability:** Allows additional departments and devices to be incorporated.

---

## 5. VLAN and IP Addressing Plan

Each department and faculty is assigned an independent VLAN and IPv4 subnet.

| VLAN ID | Department / Faculty | Network Address | Subnet Mask |
|:---:|---|---|---|
| 10 | Administration | 192.168.1.0/24 | 255.255.255.0 |
| 20 | Finance | 192.168.2.0/24 | 255.255.255.0 |
| 30 | Human Resources | 192.168.3.0/24 | 255.255.255.0 |
| 40 | Business | 192.168.4.0/24 | 255.255.255.0 |
| 50 | Engineering & Computing | 192.168.5.0/24 | 255.255.255.0 |
| 60 | Art & Design | 192.168.6.0/24 | 255.255.255.0 |
| 70 | Student Laboratory | 192.168.7.0/24 | 255.255.255.0 |
| 80 | IT Department | 192.168.8.0/24 | 255.255.255.0 |
| 90 | Health & Sciences Staff | 192.168.9.0/24 | 255.255.255.0 |
| 100 | Health & Sciences Student Lab | 192.168.10.0/24 | 255.255.255.0 |

Each VLAN operates within its own broadcast domain to improve network organization and traffic isolation.

---

## 6. Routing and Network Services

### Routing Protocols

- **RIPv2:** Used for dynamic route exchange between internal campus routers.
- **Static Routing:** Used for connectivity between the internal network and external cloud infrastructure.
- **Inter-VLAN Routing:** Enables communication between departmental VLANs through Layer 3 routing.

### Network Services

- DHCP for automatic IP address allocation in Building A.
- Internal university web server hosted in the IT department.
- Additional internal servers for university services.
- External cloud-hosted email server.
- Inter-campus communication between the main and branch campuses.

---

## 7. Network Security

The network incorporates the following security and segmentation practices:

- VLAN-based departmental isolation.
- Appropriate switch port assignments.
- Trunk configuration for carrying multiple VLANs.
- Switch security configurations.
- Separation of staff and student networks.
- Controlled routing between different network segments.

---

## 8. Device Configuration Files

Individual device configurations are maintained in separate `.txt` files for easier readability, troubleshooting, and reference.

### Router Configurations

| Device | Configuration File |
|---|---|
| Main Campus Router | [main-campus-router.txt](configurations/routers/main-campus-router.txt) |
| Branch Campus Router | [branch-campus-router.txt](configurations/routers/branch-campus-router.txt) |
| Cloud Router | [cloud-router.txt](configurations/routers/cloud-router.txt) |

### Switch Configurations

| Device | Configuration File |
|---|---|
| Main Campus Layer 3 Switch | [main-campus-l3-switch.txt](configurations/switches/main-campus-l3-switch.txt) |
| Building A Switches | [building-a-switches.txt](configurations/switches/building-a-switches.txt) |
| Building B Switches | [building-b-switches.txt](configurations/switches/building-b-switches.txt) |
| Building C Switches | [building-c-switches.txt](configurations/switches/building-c-switches.txt) |
| Branch Campus Switch | [branch-campus-switch.txt](configurations/switches/branch-campus-switch.txt) |

### Server Configurations

| Server | Configuration File |
|---|---|
| Internal Web Server | [web-server.txt](configurations/servers/web-server.txt) |
| External Email Server | [email-server.txt](configurations/servers/email-server.txt) |
| DHCP Configuration | [dhcp-configuration.txt](configurations/servers/dhcp-configuration.txt) |

---

## 9. Final Network Topology

The complete network topology was designed and implemented using Cisco Packet Tracer.

The topology illustrates:

- Main and branch campus connectivity.
- Department-wise VLAN segmentation.
- Router and switch interconnections.
- Internal and external server placement.
- Cloud network connectivity.

![Albion University Final Network Topology](topology/topology.png)

---

## 10. Testing and Verification

The following tests can be performed to verify network functionality.

| Test | Expected Result |
|---|---|
| DHCP Address Assignment | Building A devices receive dynamic IP addresses. |
| VLAN Connectivity | Devices communicate within their assigned VLANs. |
| Inter-VLAN Communication | Authorized communication between VLANs works. |
| RIPv2 Routing | Internal routers exchange network routes. |
| Inter-Campus Connectivity | Main and branch campuses communicate. |
| Internal Web Server | University web server is reachable from permitted networks. |
| External Email Server | Email server is reachable through cloud routing. |
| Static Routing | External network connectivity works correctly. |

### Useful Verification Commands

```bash
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
show ip protocols
show running-config
show ip dhcp binding
ping <destination-ip>
traceroute <destination-ip>
