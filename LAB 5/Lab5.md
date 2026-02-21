# LAB 5: Configuration of Static Routes and Default Routes Using Cisco Packet Tracer

---

## OBJECTIVES

1. To understand manual routing using Static Routing.
2. To understand the concept of Default Routing as a gateway of last resort.
3. To design and implement a routed topology in Cisco Packet Tracer.
4. To verify communication between two different networks using ping.

---

## THEORY

### 1. Static Routing

Static routing is the process of manually adding routing entries into a router’s routing table. In this method, the network administrator defines the exact path that packets must follow to reach a specific destination network.

**Operation:**  
When a packet arrives, the router checks its routing table. If a manually configured route matches the destination network, the packet is forwarded to the specified next-hop router. Static routes do not update automatically if network changes occur.

**Application:**  
Static routing is commonly used in small networks where topology remains stable. It provides better control and security but requires manual maintenance.

---

### 2. Default Routing

Default routing is a special type of static routing that acts as a fallback route. It is also known as the "gateway of last resort."

**Operation:**  
If a router receives a packet for a destination not listed in its routing table, it forwards the packet using the default route to a predefined next-hop address.

**Application:**  
Default routing is mainly used in stub networks or when connecting to an ISP. It reduces routing table size and simplifies configuration.

---

## NETWORK DESIGN

### Topology Description

A topology was created using two routers:

- **Router Arpan**
- **Router1**

Both routers are connected through a serial link forming the inter-network connection.

- Switch0 connects PC0 and PC1 to **Router Arpan**, forming Network 1.
- Switch1 connects PC2 and PC3 to **Router1**, forming Network 2.

Each LAN belongs to a different IP network.

---

## IP ADDRESSING SCHEME

### Network 1 (Connected to Router Arpan)

- Network Address: 192.168.1.0 /24
- Default Gateway: 192.168.1.1

| Device | IPv4 Address | Subnet Mask | Default Gateway |
|--------|-------------|-------------|-----------------|
| Router Arpan (G0/1) | 192.168.1.1 | 255.255.255.0 | N/A |
| PC0 | 192.168.1.2 | 255.255.255.0 | 192.168.1.1 |
| PC1 | 192.168.1.3 | 255.255.255.0 | 192.168.1.1 |

---

### Network 2 (Connected to Router1)

- Network Address: 192.168.2.0 /24
- Default Gateway: 192.168.2.1

| Device | IPv4 Address | Subnet Mask | Default Gateway |
|--------|-------------|-------------|-----------------|
| Router1 (G0/1) | 192.168.2.1 | 255.255.255.0 | N/A |
| PC2 | 192.168.2.2 | 255.255.255.0 | 192.168.2.1 |
| PC3 | 192.168.2.3 | 255.255.255.0 | 192.168.2.1 |

---

### Inter-Router Network

- Network Address: 10.0.0.0 /8

| Device | IPv4 Address | Subnet Mask |
|--------|-------------|-------------|
| Router Arpan (G0/0) | 10.0.0.1 | 255.0.0.0 |
| Router1 (G0/0) | 10.0.0.2 | 255.0.0.0 |

---

## ROUTING IMPLEMENTATION

Static routes were added on both routers so that each router could recognize the remote LAN network.

Additionally, a default route was configured to demonstrate how unknown traffic can be forwarded through a single exit path.

After routing configuration, both routers successfully updated their routing tables and became aware of the remote network.

---

## PING VERIFICATION

### Static Route Testing

- Ping from **PC1 (192.168.1.3)** to **PC3 (192.168.2.3)** → Successful  
- Ping from **PC3 to PC1** → Successful  

This confirms correct static routing configuration.

---

### Default Route Testing

After configuring default routing:

- Ping between networks remained successful.
- Unknown traffic was properly forwarded using the default route.

---

## RESULT

The network was successfully configured using both static routing and default routing techniques.

Ping tests confirmed:

- Proper communication within the same LAN
- Proper communication between two different LANs
- Correct packet forwarding through routers

This verifies correct implementation of static and default routing in Cisco Packet Tracer.

---

## DISCUSSION & CONCLUSION

In this lab, static routing and default routing were implemented to understand manual path selection in networking.

Static routing allowed precise control over packet flow between two networks. It demonstrated how routers use routing tables to make forwarding decisions.

Default routing simplified the routing table by providing a fallback path for unknown destinations. This is particularly useful in stub networks and internet connections.

The successful ping results confirmed proper IP addressing, gateway configuration, and routing table implementation.

Overall, this lab provided practical knowledge of routing behavior, inter-network communication, and packet forwarding mechanisms using Cisco Packet Tracer.