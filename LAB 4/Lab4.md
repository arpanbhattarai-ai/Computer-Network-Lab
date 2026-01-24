# LAB 4: Subnetting and Supernetting Using Cisco Packet Tracer

---

## OBJECTIVES

1. To understand logical division of IP networks through subnetting.  
2. To understand aggregation of networks through supernetting (CIDR).  
3. To design and implement subnetting and supernetting topologies in Cisco Packet Tracer.  
4. To verify communication between different subnets using ping.  

---

## THEORY

### 1. Subnetting

Subnetting is the process of dividing a single large network into multiple smaller logical networks called subnets. It is achieved by borrowing bits from the host portion of an IP address to create additional network identifiers.

**Operation:**  
A subnet mask is used to extend the network portion of the address. For example, borrowing 2 bits from a Class C /24 network results in 4 subnets. Routers use the subnet mask to determine which subnet an IP address belongs to.

**Application:**  
Subnetting improves network performance and security by reducing broadcast traffic and allowing efficient IP address utilization.

---

### 2. Supernetting

Supernetting, also known as Classless Inter-Domain Routing (CIDR), is the process of combining multiple smaller networks into a single larger network.

**Operation:**  
The subnet mask is modified by moving the network boundary to the left, allowing multiple contiguous networks to be summarized into one routing entry.

**Application:**  
Supernetting reduces routing table size and improves routing efficiency in large-scale networks.

---

## NETWORK DESIGN

### 1. Subnetting Design

**Base Network:** 192.168.1.0 /24  
**Required Subnets:** 4  
**Borrowed Bits:** 2  
**New Subnet Mask:** /26 → 255.255.255.192  
**Block Size:** 64 IP addresses per subnet  

#### Subnet Calculation Table

| Subnet | Network ID     | 1st Host       | Last Host      | Broadcast ID   |
|--------|----------------|----------------|----------------|----------------|
| 1      | 192.168.1.0    | 192.168.1.1    | 192.168.1.62   | 192.168.1.63  |
| 2      | 192.168.1.64   | 192.168.1.65   | 192.168.1.126  | 192.168.1.127 |
| 3      | 192.168.1.128  | 192.168.1.129  | 192.168.1.190  | 192.168.1.191 |
| 4      | 192.168.1.192  | 192.168.1.193  | 192.168.1.254  | 192.168.1.255 |

---

### Subnetting Topology Description

A router is used to connect two subnets:

- **Subnet 1:** 192.168.1.0 /26  
- **Subnet 2:** 192.168.1.64 /26  

Switch0 connects PCs (PC0, PC1, PC2) in Subnet 1.  
Switch1 connects PCs (PC3, PC4, PC5) in Subnet 2.  
Both switches are connected to Router0.

---

### Subnetting IP Configuration Table

| Device | IPv4 Address     | Subnet Mask        | Default Gateway |
|--------|------------------|--------------------|-----------------|
| Router0 (Fa0/0) | 192.168.1.1  | 255.255.255.192 | N/A |
| Router0 (Fa0/1) | 192.168.1.65 | 255.255.255.192 | N/A |
| PC0 | 192.168.1.2 | 255.255.255.192 | 192.168.1.1 |
| PC1 | 192.168.1.3 | 255.255.255.192 | 192.168.1.1 |
| PC2 | 192.168.1.4 | 255.255.255.192 | 192.168.1.1 |
| PC3 | 192.168.1.66 | 255.255.255.192 | 192.168.1.65 |
| PC4 | 192.168.1.67 | 255.255.255.192 | 192.168.1.65 |
| PC5 | 192.168.1.68 | 255.255.255.192 | 192.168.1.65 |

---

### Ping Verification – Subnetting

- Ping from **PC0 → PC2** (Same Subnet) → Successful  
- Ping from **PC0 → PC5** (Different Subnet via Router) → Successful  

---

## 2. Supernetting Design

### Supernet Network

To combine four Class C networks:

- **Supernet Address:** 192.168.0.0 /22  
- **Subnet Mask:** 255.255.252.0  

This supernet includes:

- 192.168.0.0  
- 192.168.1.0  
- 192.168.2.0  
- 192.168.3.0  

---

### Supernetting Topology Description

One router connects a switch, which connects four PCs (PC6–PC9).  
All PCs belong to different networks but share the same supernet mask.

---

### Supernetting IP Configuration Table

| Device | IPv4 Address   | Subnet Mask     | Default Gateway |
|--------|---------------|-----------------|-----------------|
| Router0 (Fa0/0) | 192.168.0.1 | 255.255.252.0 | N/A |
| PC6 | 192.168.0.10 | 255.255.252.0 | 192.168.0.1 |
| PC7 | 192.168.1.10 | 255.255.252.0 | 192.168.0.1 |
| PC8 | 192.168.2.10 | 255.255.252.0 | 192.168.0.1 |
| PC9 | 192.168.3.10 | 255.255.252.0 | 192.168.0.1 |

---

### Ping Verification – Supernetting

- Ping from **PC6 → PC9** → Successful  

---

## RESULT

The networks were successfully configured.  
Ping tests confirmed:

- Communication within the same subnet  
- Communication across different subnets via router  
- Successful connectivity in the supernetted network  

This verifies correct implementation of both subnetting and supernetting.

---

## DISCUSSION & CONCLUSION

In this lab, subnetting and supernetting were implemented to understand efficient IP address management and routing design. Subnetting allowed division of a larger network into smaller logical networks, improving address utilization and reducing broadcast traffic. Supernetting enabled multiple networks to be summarized into a single routing entry, simplifying routing tables.

Overall, the lab provided practical understanding of IP addressing, subnet mask calculation, router configuration, and packet flow verification using Cisco Packet Tracer.

---

