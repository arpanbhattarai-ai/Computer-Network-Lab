# LAB 3: Study and Simulation of Basic Networking Devices Using Cisco Packet Tracer

## OBJECTIVE:
- To study the working of hub, switch, bridge, router, and repeater.  
- To understand the OSI layers of different networking devices.  
- To design and simulate a network using Cisco Packet Tracer.  
- To verify communication between computers using ping.  

---

## THEORY:

### 1. Hub
A hub is a basic networking device used to connect multiple computers in a network. It operates at the **Physical Layer (Layer 1)** of the OSI model. When a hub receives data from any connected device, it broadcasts the data to all other devices. Due to this broadcasting nature, bandwidth is shared among all devices, which may lead to collisions and reduced network efficiency. In this experiment, the hub demonstrates how data is transmitted without filtering.

### 2. Switch
A switch is an intelligent networking device used to connect devices within a Local Area Network (LAN). It operates at the **Data Link Layer (Layer 2)** of the OSI model. The switch forwards data only to the intended destination by using MAC addresses, which improves network performance and reduces collisions. In the experiment, the switch allows efficient communication between multiple PCs.

### 3. Bridge
A bridge is used to connect two or more LAN segments and works at the **Data Link Layer (Layer 2)**. It filters network traffic by learning MAC addresses and allows only required data to pass between segments. This reduces unnecessary traffic and improves network performance. In this experiment, the bridge connects two switches and controls data flow between them.

### 4. Router
A router is a **Network Layer (Layer 3)** device used to connect two or more different IP networks and enable communication between them. Unlike switches, which work within the same network, a router forwards data packets between networks based on IP addresses.

A router has multiple interfaces, and each interface is assigned a unique IP address belonging to the network it connects to. These interface IP addresses act as the default gateway for the devices in their respective networks. When a device wants to communicate with another network, it sends the data to its default gateway, and the router forwards the packet to the correct destination network.

In this experiment, the router connects two different networks:
- **192.168.1.0/24**
- **10.10.10.0/24**

The router is configured with:
- **192.168.1.1** on LAN 1  
- **10.10.10.1** on LAN 2  

Thus, the router enables communication between the two networks by routing packets through its interfaces.

### 5. Repeater
A repeater is a device used to extend the range of a network. It operates at the **Physical Layer (Layer 1)** of the OSI model. The repeater regenerates and retransmits weak signals to maintain signal strength over long distances. In this experiment, the repeater ensures reliable signal transmission between network segments.

---

## CONFIGURATION:

### 1. Hub Configuration

| Device Name | Interface      | IP Address   | Subnet Mask   |
|-------------|---------------|--------------|---------------|
| PC0         | FastEthernet0 | 192.168.1.1  | 255.255.255.0 |
| PC1         | FastEthernet0 | 192.168.1.2  | 255.255.255.0 |
| PC2         | FastEthernet0 | 192.168.1.3  | 255.255.255.0 |
| PC3         | FastEthernet0 | 192.168.1.4  | 255.255.255.0 |

---

### 2. Switch Configuration

| Device Name | Interface      | IP Address   | Subnet Mask   |
|-------------|---------------|--------------|---------------|
| PC0         | FastEthernet0 | 192.168.1.1  | 255.255.255.0 |
| PC1         | FastEthernet0 | 192.168.1.2  | 255.255.255.0 |
| PC2         | FastEthernet0 | 192.168.1.3  | 255.255.255.0 |
| PC3         | FastEthernet0 | 192.168.1.4  | 255.255.255.0 |

---

### 3. Bridge Configuration

| Device Name | IP Address   | Subnet Mask   |
|-------------|--------------|---------------|
| Switch0     | 192.168.1.2  | 255.255.255.0 |
| Switch1     | 10.10.10.2   | 255.255.255.0 |
| Bridge0     | 192.168.1.1  | 255.255.255.0 |

---

### 4. Router Configuration

| Device Name | Interface       | IP Address   | Subnet Mask   | Gateway     |
|-------------|-----------------|--------------|---------------|-------------|
| Router0     | Gig0/0 (LAN 1)  | 192.168.1.1  | 255.255.255.0 | N/A         |
| Router0     | Gig0/1 (LAN 2)  | 10.10.10.1   | 255.255.255.0 | N/A         |
| PC-LAN1     | FastEthernet0   | 192.168.1.2  | 255.255.255.0 | 192.168.1.1 |
| PC-LAN2     | FastEthernet0   | 10.10.10.2   | 255.255.255.0 | 10.10.10.1 |

---

### 5. Repeater Configuration

| Device Name | Connection Type            | Status |
|-------------|----------------------------|--------|
| Repeater0   | Port 0 to Left Segment     | Active |
| Repeater0   | Port 1 to Right Segment    | Active |

---

## RESULT:
The network was successfully designed and simulated using Cisco Packet Tracer. Communication between devices was verified using the **ping** command, and all packets were transmitted successfully, confirming correct configuration of hub, switch, bridge, router, and repeater.

---

## CONCLUSION:
This lab provided practical understanding of basic networking devices and their roles in data communication. The simulation demonstrated how each device operates at different OSI layers and how proper configuration enables successful network communication.

