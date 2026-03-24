# Project Title: Build a branch office network with 1 router, 1 switch, and configure 3 VLANs. Setup DHCP for all VLANs. Configure a default route to connect to headquarters. Add a DNS server. Use superneng to summarize routes. Verify with network commands.

---

## OBJECTIVES

1. To design and implement a branch office network using VLAN segmentation.  
2. To configure inter-VLAN routing using the Router-on-a-Stick method.  
3. To configure DHCP on the router for automatic IP address allocation across multiple VLANs.  
4. To set up a DNS server for domain name resolution.  
5. To configure a default route to simulate connectivity to a headquarters network.  
6. To implement route summarization (supernetting) for efficient routing.  
7. To verify network functionality using Cisco IOS commands.

---

## THEORY

### 1. VLAN (Virtual Local Area Network)

A VLAN is a logical segmentation of a network that divides a single physical switch into multiple broadcast domains. Devices within the same VLAN can communicate directly, while communication between different VLANs requires a Layer 3 device such as a router. VLANs improve network performance, enhance security, and allow logical grouping of devices based on organizational requirements.

---

### 2. Trunking (IEEE 802.1Q)

Trunking enables multiple VLANs to share a single physical link between a switch and a router. IEEE 802.1Q tagging is used to identify VLAN information within Ethernet frames, allowing the router to differentiate traffic from multiple VLANs.

---

### 3. Inter-VLAN Routing (Router-on-a-Stick)

Inter-VLAN routing is achieved using the Router-on-a-Stick method, where a single router interface is divided into multiple subinterfaces. Each subinterface is assigned a VLAN ID using encapsulation dot1Q and configured with an IP address that acts as the default gateway for that VLAN.

---

### 4. Dynamic Host Configuration Protocol (DHCP)

DHCP automatically assigns IP addresses, subnet masks, default gateways, and DNS server addresses to client devices. This reduces manual configuration and ensures efficient IP address management across the network.

---

### 5. Domain Name System (DNS)

DNS translates human-readable domain names into IP addresses. A DNS server stores mappings between domain names and IP addresses, enabling users to access network resources using hostnames instead of numeric addresses.

---

### 6. Static Routing and Default Route

Static routing involves manually configuring routes in the router’s routing table. A default route (0.0.0.0/0) is used to forward packets destined for unknown networks. In this lab, the default route simulates connectivity to a headquarters network.

---

### 7. Route Summarization (Supernetting)

Route summarization combines multiple network prefixes into a single route. This reduces the routing table size and improves efficiency. In this project, multiple VLAN subnets are summarized into one network before being forwarded toward headquarters.

---

## NETWORK TOPOLOGY

The network topology consists of:

- Router (R1 – Cisco 1941)  
- Switch (SW1 – Layer 2 Switch)  
- Nine PCs distributed across three VLANs  
- One Server configured as DNS server  

The router is connected to the switch via a trunk link and uses Router-on-a-Stick configuration to enable inter-VLAN routing.

---

## VLAN ASSIGNMENT

- VLAN 10 – SALES  
  - PC0, PC1, PC2  

- VLAN 20 – HR  
  - PC3, PC4, PC5  

- VLAN 30 – IT  
  - PC6, PC7, PC8  

---

## IP CONFIGURATION TABLE

| Device | Interface | IP Address | Subnet Mask | Default Gateway | DNS |
|--------|----------|------------|------------|----------------|-----|
| R1     | G0/0.10  | 192.168.10.1 | 255.255.255.0 | N/A | N/A |
| R1     | G0/0.20  | 192.168.20.1 | 255.255.255.0 | N/A | N/A |
| R1     | G0/0.30  | 192.168.30.1 | 255.255.255.0 | N/A | N/A |
| Server | Fa0      | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 | 192.168.10.10 |
| PCs    | DHCP     | Automatic | Automatic | Automatic | Automatic |

---

## CONFIGURATION

### 1. Switch Configuration

```bash
enable
configure terminal

vlan 10
 name SALES
vlan 20
 name HR
vlan 30
 name IT
exit

interface range fa0/1 - 3
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 no shutdown
exit

interface range fa0/4 - 6
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 no shutdown
exit

interface range fa0/7 - 9
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
 no shutdown
exit

interface fa0/10
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 no shutdown
exit

interface fa0/11
 switchport mode access
 switchport access vlan 10
 no shutdown
```

---

### 2. Router Configuration

```bash
enable
configure terminal
hostname R1

interface g0/0
no shutdown

interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0

interface g0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
```

---

### 3. DHCP Configuration

```bash
ip dhcp excluded-address 192.168.10.1
ip dhcp excluded-address 192.168.20.1
ip dhcp excluded-address 192.168.30.1

ip dhcp pool VLAN10
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 192.168.10.10
exit

ip dhcp pool VLAN20
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
 dns-server 192.168.10.10
exit

ip dhcp pool VLAN30
 network 192.168.30.0 255.255.255.0
 default-router 192.168.30.1
 dns-server 192.168.10.10
exit
```

---

### 4. Default Route

```bash
ip route 0.0.0.0 0.0.0.0 g0/0.10
```

---

### 5. Route Summarization

```bash
ip route 192.168.0.0 255.255.0.0 10.0.0.1
```

---

### 6. DNS Configuration

- Static IP: 192.168.10.10  
- Gateway: 192.168.10.1  
- DNS enabled  
- Record: google.com → 8.8.8.8  

---

## TESTING AND VERIFICATION

- show vlan brief  
- show ip route  
- show ip dhcp binding  

### Ping Tests

- PC → Gateway → Successful  
- Inter-VLAN → Successful  
- ping google.com → DNS resolution successful  

---

## RESULT

The network was successfully configured with VLAN segmentation, inter-VLAN routing, DHCP, DNS, and static routing. All devices received IP addresses automatically, and communication between VLANs was achieved.

---

## CONCLUSION

This lab demonstrated the successful implementation of a branch office network using VLANs, routing, DHCP, DNS, and static routing. It provides practical understanding of real-world network configuration using Cisco Packet Tracer.