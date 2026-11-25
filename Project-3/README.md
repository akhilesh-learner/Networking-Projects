# **LAB 2** ~ Vic Modern Hotel – Enterprise Network Design and Implementation

## 📌 Project Overview

This is my 3rd project which focuses on designing and implementing an **Enterprise Network Infrastructure for Vic Modern Hotel** using **Cisco Packet Tracer**.

The hotel consists of three floors, each containing different departments with specific networking requirements. The network is designed to provide secure, reliable, and efficient communication between all departments using VLAN segmentation, inter-VLAN routing, OSPF, DHCP, wireless connectivity, and also some network security mechanisms.

The implementation includes:

- 3 Cisco Routers
- 3 Cisco Layer 2 Switches
- 8 Departmental VLANs
- 3 Wireless Access Points (Wi-Fi)
- 8 Departmental Printers
- Wired and Wireless End Devices
- Serial DCE/DTE Router Connections for Routers

## Scenario

![Question](Screenshots/lab-3-question.PNG)

## 🎯 Project Objectives

- Design and implement a three-floor enterprise network.
- Configure three routers to interconnect all hotel floors.
- Establish serial connections between routers using DCE/DTE cables.
- Implement departmental VLANs for network segmentation.
- Configure inter-VLAN routing using Router-on-a-Stick.
- Implement OSPF as the dynamic routing protocol.
- Configure DHCP services on each floor router.
- Provide wireless connectivity for laptops, tablets, and smartphones.
- Connect printers to their respective departmental networks.
- Configure SSH for secure remote router administration.
- Implement switch port security using sticky MAC address learning.
- Restrict the IT department's Fa0/1 switch port to the authorized Test-PC using shutdown violation mode.

---

## 🏢 Network Architecture

The hotel network is divided into three floors.

### 🟣 First Floor

The first floor consists of three departments:

| Department | VLAN ID | Network Address |
|---|---:|---|
| Reception | 80 | 192.168.8.0/24 |
| Store | 70 | 192.168.7.0/24 |
| Logistics | 60 | 192.168.6.0/24 |

**Network Devices:**
- F1-Router
- F1-Switch (Cisco 2960)
- Wireless Access Point
- Departmental PCs and Printers
- Laptops, Tablets, and Smartphones

### 🟢 Second Floor

The second floor consists of three departments:

| Department | VLAN ID | Network Address |
|---|---:|---|
| Finance | 50 | 192.168.5.0/24 |
| HR | 40 | 192.168.4.0/24 |
| Sales/Marketing | 30 | 192.168.3.0/24 |

**Network Devices:**
- F2-Router
- F2-Switch (Cisco 2960)
- Wireless Access Point
- Departmental PCs and Printers
- Laptops, Tablets, and Smartphones

### 🔵 Third Floor

The third floor consists of two departments:

| Department | VLAN ID | Network Address |
|---|---:|---|
| Admin | 20 | 192.168.2.0/24 |
| IT | 10 | 192.168.1.0/24 |

**Network Devices:**
- F3-Router
- F3-Switch (Cisco 2960)
- Wireless Access Point
- Departmental PCs and Printers
- Laptops, Tablets, and Smartphones
- Dedicated Test-PC for SSH and Port Security Verification

---

## 🗺️ Network Topology

The network follows a three-floor enterprise architecture.

Each floor has a dedicated router and managed switch. The three routers are interconnected using serial DCE/DTE connections, forming a triangular topology.

The switches provide connectivity to departmental devices, printers, and wireless access points.

![Vic Modern Hotel Network Topology](Screenshots/lab-3-topology-design.PNG)

---

## 🌐 IP Addressing Scheme

### Departmental LAN Addressing

Each department is assigned a separate `/24` network.

| Floor | Department | VLAN | Network Address | Subnet Mask |
|---|---|---:|---|---|
| First | Reception | 80 | 192.168.8.0 | 255.255.255.0 |
| First | Store | 70 | 192.168.7.0 | 255.255.255.0 |
| First | Logistics | 60 | 192.168.6.0 | 255.255.255.0 |
| Second | Finance | 50 | 192.168.5.0 | 255.255.255.0 |
| Second | HR | 40 | 192.168.4.0 | 255.255.255.0 |
| Second | Sales/Marketing | 30 | 192.168.3.0 | 255.255.255.0 |
| Third | Admin | 20 | 192.168.2.0 | 255.255.255.0 |
| Third | IT | 10 | 192.168.1.0 | 255.255.255.0 |

### Router-to-Router Serial Addressing

The three routers are interconnected using three point-to-point serial DCE links.

| Router Connection | Network Address | Subnet Mask |
|---|---|---|
| F2-Router ↔ F3-Router | 10.10.10.0/30 | 255.255.255.252 |
| F3-Router ↔ F1-Router | 10.10.10.4/30 | 255.255.255.252 |
| F2-Router ↔ F1-Router | 10.10.10.8/30 | 255.255.255.252 |

Each `/30` subnet provides two usable IP addresses for router interfaces.

---

## 🔀 VLAN Implementation

**Virtual Local Area Networks (VLANs)** are implemented to logically separate the hotel departments based on the given requirements.

Each department is assigned a unique VLAN ID and IP subnet.

| VLAN ID | Department | Floor |
|---:|---|---|
| 10 | IT | Third |
| 20 | Admin | Third |
| 30 | Sales/Marketing | Second |
| 40 | HR | Second |
| 50 | Finance | Second |
| 60 | Logistics | First |
| 70 | Store | First |
| 80 | Reception | First |

**Benefits of VLAN Implementation:**

- Departmental network segmentation.
- Reduced broadcast domains.
- Improved network organization.
- Better network management.
- Easier implementation of access control policies.

## 🔄 Inter-VLAN Routing

Inter-VLAN routing enables communication between devices belonging to different departmental VLANs.

The floor routers provide routing between VLANs configured on their respective floor switches.

**Router-on-a-Stick** is implemented using router subinterfaces associated with the corresponding VLAN IDs.

### Default Gateway Addressing

| VLAN | Network | Default Gateway |
|---:|---|---|
| 80 | 192.168.8.0/24 | 192.168.8.1 |
| 70 | 192.168.7.0/24 | 192.168.7.1 |
| 60 | 192.168.6.0/24 | 192.168.6.1 |
| 50 | 192.168.5.0/24 | 192.168.5.1 |
| 40 | 192.168.4.0/24 | 192.168.4.1 |
| 30 | 192.168.3.0/24 | 192.168.3.1 |
| 20 | 192.168.2.0/24 | 192.168.2.1 |
| 10 | 192.168.1.0/24 | 192.168.1.1 |

---

## 🧭 Dynamic Routing – OSPF

**Open Shortest Path First (OSPF)** is implemented as the dynamic routing protocol to enable communication between the three floor routers.

OSPF allows routers to dynamically exchange routing information and learn about remote departmental networks.

### OSPF Implementation

- Configure OSPF on all three routers.
- Advertise all departmental LAN networks.
- Advertise router-to-router serial networks.
- Establish OSPF neighbor relationships.
- Verify dynamically learned routes.

All routers participate in **OSPF Area 0**.

**Verification Commands:**

```bash
show ip ospf neighbor
show ip route
show ip protocols
```

---

## 📡 DHCP Configuration

**Dynamic Host Configuration Protocol (DHCP)** is configured on each floor router.

Each router acts as the DHCP server for the VLANs on its respective floor.

DHCP dynamically assigns:

- IP addresses.
- Subnet masks.
- Default gateways.
- DNS server addresses.

### DHCP Server Distribution

| Router | DHCP Networks |
|---|---|
| F1-Router | Reception, Store, Logistics |
| F2-Router | Finance, HR, Sales/Marketing |
| F3-Router | Admin, IT |

All end devices are configured to obtain their IP addresses dynamically.

**Verification Commands:**

```bash
show ip dhcp binding
show ip dhcp pool
```

On end devices:

```bash
ipconfig
```

---

## 📶 Wireless Network Implementation

Each floor is equipped with a wireless access point connected to its respective floor switch.

Wireless connectivity is provided for:

- Laptops.
- Tablets.
- Smartphones.

Wireless devices connect to the corresponding floor wireless network and obtain IP addresses dynamically through DHCP.

---

## 🖨️ Printer Connectivity

Each department is provided with a dedicated network printer.

| Floor | Department | Printer |
|---|---|---|
| First | Reception | Printer2 |
| First | Store | Printer1 |
| First | Logistics | Printer0 |
| Second | Finance | Printer3 |
| Second | HR | Printer4 |
| Second | Sales/Marketing | Printer5 |
| Third | Admin | Printer7 |
| Third | IT | Printer8 |

All printers are connected to their respective departmental networks.

---

## 🔐 SSH Remote Management

**Secure Shell (SSH)** is configured on all three routers to provide encrypted remote administrative access.

SSH provides a secure alternative to Telnet by encrypting communication between administrators and network devices.

### SSH Implementation

- Configure router hostnames.
- Set domain names.
- Generate RSA cryptographic keys.
- Create local administrator credentials.
- Enable SSH version 2.
- Configure VTY lines for SSH access.
- Enable local authentication.

### SSH Verification

The dedicated Test-PC in the IT department is used to verify remote router access.

```bash
ssh -l <username> <router-management-ip>
```

Successful authentication confirms that SSH remote management is operational.

---

## 🛡️ Switch Port Security

Port security is implemented on the IT department switch (**F3-Switch**) to restrict unauthorized devices from accessing the network through the designated switch port.

The Test-PC is connected to **FastEthernet0/1 (Fa0/1)**.

### Port Security Configuration Requirements

| Feature | Configuration |
|---|---|
| Switch | F3-Switch |
| Interface | FastEthernet0/1 |
| Maximum MAC Addresses | 1 |
| MAC Learning | Sticky |
| Violation Mode | Shutdown |
| Authorized Device | Test-PC |

Sticky MAC address learning dynamically learns and stores the authorized device's MAC address.

If an unauthorized device attempts to access the protected port, the switch detects a security violation and places the interface into an error-disabled state.

### Port Security Verification

```bash
show port-security interface fa0/1
show port-security address
show interfaces fa0/1 status
```

---

## 🧪 Network Testing and Verification

The following tests are used to verify the network implementation.

| Test | Verification Command / Method | Expected Result |
|---|---|---|
| VLAN Configuration | `show vlan brief` | Required VLANs are present |
| Trunk Configuration | `show interfaces trunk` | Required trunk links are operational |
| Router Interfaces | `show ip interface brief` | Configured interfaces are up |
| OSPF Neighbors | `show ip ospf neighbor` | Router adjacencies established |
| Routing Table | `show ip route` | Remote networks learned dynamically |
| DHCP Allocation | `ipconfig` | Devices receive dynamic IP addresses |
| Inter-VLAN Communication | `ping` | Different departmental VLANs communicate |
| Inter-Floor Communication | `ping` | Devices across floors communicate |
| Printer Connectivity | `ping` | Printers are reachable |
| Wireless Connectivity | Wireless association and `ipconfig` | Wireless clients connect successfully |
| SSH Connectivity | SSH from Test-PC | Secure router login succeeds |
| Port Security | `show port-security interface fa0/1` | Sticky MAC and shutdown mode configured |

### Connectivity Test Scenarios

1. Reception PC communicating with Store PC.
2. Logistics PC communicating with Finance PC.
3. HR PC communicating with Sales/Marketing PC.
4. Admin PC communicating with IT PC.
5. First-floor devices communicating with second-floor devices.
6. Second-floor devices communicating with third-floor devices.
7. Wireless devices communicating with wired departmental devices.
8. Test-PC establishing SSH sessions with all three routers.

Port security should also be tested by connecting an unauthorized device to the protected Fa0/1 port and verifying that the interface enters the error-disabled state.

---

## 🛠️ Technologies and Tools Used

| Technology | Purpose |
|---|---|
| Cisco Packet Tracer | Network design and simulation |
| Cisco Routers (2901/2911) | Inter-floor routing |
| Cisco Catalyst 2960 Switches | LAN connectivity and VLAN implementation |
| VLANs | Departmental network segmentation |
| IEEE 802.1Q | VLAN trunking |
| Router-on-a-Stick | Inter-VLAN routing |
| OSPF | Dynamic routing |
| DHCP | Dynamic IP address allocation |
| SSH | Secure remote administration |
| Port Security | Unauthorized device prevention |
| Wireless Access Points | Wireless connectivity |
| Serial DCE/DTE | Router interconnection |

---

## 📁 Project Repository Structure

```text
Vic-Modern-Hotel-Network/
│
├── README.md
│
├── topology/
│   └── lab-3-topology-design.PNG
│
├── packet-tracer/
│   └── Vic-Modern-Hotel-Network.pkt
│
├── configurations/
│   ├── F1-Router.txt
│   ├── F2-Router.txt
│   ├── F3-Router.txt
│   ├── F1-Switch.txt
│   ├── F2-Switch.txt
│   └── F3-Switch.txt
│
└── screenshots/
    ├── network-topology.png
    ├── vlan-configuration.png
    ├── ospf-neighbors.png
    ├── routing-table.png
    ├── dhcp-verification.png
    ├── ssh-verification.png
    └── port-security.png
```

---

## 🚀 Want to use this Project? Here's how you do that!

1. Clone or download this repository.

```bash
git clone <your-repository-url>
```

2. Install and open **Cisco Packet Tracer**.

3. Navigate to the `packet-tracer` directory.

4. Open `Vic-Modern-Hotel-Network.pkt`.

5. Wait for the network topology to load (or you fast-forwardd also).

6. Inspect the router, switch, VLAN, DHCP, OSPF, and security configurations.

7. Perform connectivity tests using the end devices.

8. Verify SSH remote access and switch port security using the dedicated Test-PC (same PC which is used in IT dept. PC).

---

## 📈 Project Outcomes - Learnings 

The Vic Modern Hotel network design demonstrates the implementation of a multi-floor enterprise network with departmental segmentation and centralized connectivity.

The project covers several important networking concepts:

- Multi-router network design.
- VLAN-based departmental segmentation.
- Inter-VLAN routing.
- Dynamic routing using OSPF.
- Dynamic IP allocation through DHCP.
- Wired and wireless network connectivity.
- Secure router administration using SSH.
- Layer 2 switch security using sticky MAC address learning.

The resulting network provides a structured foundation for communication between all hotel departments while incorporating essential network management and security practices.

---

## 👨‍💻 Author

**Project:** Vic Modern Hotel – Enterprise Network Design and Implementation

**Platform:** Cisco Packet Tracer

**Category:** Computer Networking | Enterprise Network Design | Network Security

---

⭐ If you find this project useful, feel free to explore the repository and learn more about enterprise network design and implementation and also let's connect together to explore many more!