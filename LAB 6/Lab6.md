# LAB 6: Dynamic Routing Configuration – RIP, EIGRP, OSPF, and BGP

---

## OBJECTIVES

1. To understand the working principles of dynamic routing protocols including RIP, EIGRP, OSPF, and BGP.
2. To configure these protocols on routers using Cisco Packet Tracer.
3. To observe automatic route discovery and routing table updates.
4. To verify communication between different networks using ping testing.

---

## HARDWARE AND SOFTWARE REQUIREMENTS

- Cisco Packet Tracer (Version 6.2 or higher)
- Windows PC / Laptop

---

## THEORY

Dynamic routing protocols allow routers to automatically exchange routing information and update routing tables without manual configuration of individual routes. Unlike static routing, dynamic routing adapts to network topology changes.

### 1. RIP (Routing Information Protocol)

RIP is a distance-vector routing protocol that uses hop count as its primary metric.

**Operation:**  
RIP sends the entire routing table to directly connected neighbors every 30 seconds. It limits the hop count to 15; 16 is considered unreachable.

**Application:**  
Used in small networks where simplicity is required, though it has slow convergence times.

---

### 2. EIGRP (Enhanced Interior Gateway Routing Protocol)

EIGRP is an advanced distance-vector protocol (often called hybrid) developed by Cisco.

**Operation:**  
It uses the Diffusing Update Algorithm (DUAL) to calculate the shortest path. It sends partial updates only when topology changes occur rather than full periodic updates.

**Application:**  
Used in Cisco-based enterprise networks requiring fast convergence and efficient bandwidth usage.

---

### 3. OSPF (Open Shortest Path First)

OSPF is a link-state routing protocol that maintains a map of the network topology.

**Operation:**  
It uses the Dijkstra algorithm (Shortest Path First) to calculate the best path. Routers exchange Link State Advertisements (LSAs) to build a topology database.

**Application:**  
Used in large, scalable enterprise networks because it supports hierarchical design using Areas (e.g., Area 0).

---

### 4. BGP (Border Gateway Protocol)

BGP is a path-vector protocol used to exchange routing information between different autonomous systems (AS).

**Operation:**  
It makes routing decisions based on paths, network policies, or rule-sets configured by a network administrator rather than just technical metrics.

**Application:**  
It is the primary protocol used to route traffic across the Internet (ISP to ISP).

---

## NETWORK TOPOLOGY

A topology was created using Router0 and Router1 connected via a serial/WAN link.

- Switch0 connects PC0 and PC1 to Router0 (Network 192.168.1.0/24).
- Switch1 connects PC2 and PC3 to Router1 (Network 192.168.2.0/24).

The inter-router network uses the 10.0.0.0 network for WAN communication.

---

## IP CONFIGURATION TABLE

| Device  | Interface | IP Address     | Subnet Mask       |
|----------|------------|----------------|-------------------|
| Router0  | Gig0/1     | 192.168.1.1    | 255.255.255.0     |
| Router0  | Gig0/0     | 10.0.0.1       | 255.0.0.0         |
| Router1  | Gig0/1     | 192.168.2.1    | 255.255.255.0     |
| Router1  | Gig0/0     | 10.0.0.2       | 255.0.0.0         |
| PC0      | FastEthernet0 | 192.168.1.2 | 255.255.255.0     |
| PC1      | FastEthernet0 | 192.168.1.3 | 255.255.255.0     |
| PC2      | FastEthernet0 | 192.168.2.2 | 255.255.255.0     |
| PC3      | FastEthernet0 | 192.168.2.3 | 255.255.255.0     |

---

## IMPLEMENTATION OF DYNAMIC ROUTING PROTOCOLS

### 1. RIP Configuration Commands

**Router0:**

Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.1.0
Router(config-router)# network 10.0.0.0
Router(config-router)# no auto-summary

**Router1:**

Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.2.0
Router(config-router)# network 10.0.0.0
Router(config-router)# no auto-summary


---

### 2. EIGRP Configuration Commands

**Router0:**

Router(config)# router eigrp 100
Router(config-router)# network 192.168.1.0 0.0.0.255
Router(config-router)# network 10.0.0.0 0.0.0.255
Router(config-router)# no auto-summary


**Router1:**

Router(config)# router eigrp 100
Router(config-router)# network 192.168.2.0 0.0.0.255
Router(config-router)# network 10.0.0.0 0.0.0.255
Router(config-router)# no auto-summary


---

### 3. OSPF Configuration Commands

**Router0:**

Router(config)# router ospf 1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 10.0.0.0 0.0.0.255 area 0


**Router1:**

Router(config)# router ospf 1
Router(config-router)# network 192.168.2.0 0.0.0.255 area 0
Router(config-router)# network 10.0.0.0 0.0.0.255 area 0


---

### 4. BGP Configuration Commands

**Router0 (AS 65001):**

Router(config)# router bgp 65001
Router(config-router)# neighbor 10.0.0.2 remote-as 65002
Router(config-router)# network 192.168.1.0 mask 255.255.255.0


**Router1 (AS 65002):**

Router(config)# router bgp 65002
Router(config-router)# neighbor 10.0.0.1 remote-as 65001
Router(config-router)# network 192.168.2.0 mask 255.255.255.0


---

## RESULT

The network was successfully configured using the various dynamic routing protocols. 

To verify connectivity, a ping request was sent from PC0 (192.168.1.2) to PC2 (192.168.2.2). For each protocol configured (RIP, EIGRP, OSPF, and BGP), the routing tables were updated automatically, and all packets were sent and received successfully, validating correct configuration.

---

## DISCUSSION AND CONCLUSION

During this lab session, the concept of dynamic routing was implemented to understand how routers automatically exchange routing information and update their routing tables without manual intervention. By configuring RIP, EIGRP, OSPF, and BGP individually, we were able to observe differences in routing behavior, convergence speed, and protocol functionality.

RIP demonstrated basic distance-vector routing with periodic updates and hop-count limitations. EIGRP showed faster convergence and efficient bandwidth usage due to the Diffusing Update Algorithm (DUAL). OSPF provided an understanding of link-state routing where routers build a topology database and calculate the shortest path using the SPF algorithm. BGP introduced inter-autonomous system routing and policy-based path selection, which is widely used across the Internet.

Successful ping tests confirmed that all routing protocols were functioning correctly and that routing tables were updated dynamically. Hence, the lab was completed successfully with proper understanding and implementation of dynamic routing protocols using Cisco Packet Tracer.