# LAB 7: Configuration of Switch, VLAN Configuration and Inter-VLAN Routing

---

## OBJECTIVES

1. To understand the concept of Virtual Local Area Networks (VLANs) and their role in network segmentation.
2. To configure VLANs on a Cisco Switch and assign specific ports to different VLANs.
3. To implement trunking using IEEE 802.1Q protocol.
4. To implement Inter-VLAN routing using the Router-on-a-Stick method.
5. To verify communication between different VLANs.

---

## THEORY

### 1. VLAN (Virtual Local Area Network)

A VLAN is a logical grouping of devices within the same broadcast domain. It partitions a physical switch into multiple logical networks.

**Operation:**  
Devices in one VLAN cannot communicate directly with devices in another VLAN without a Layer 3 device (Router). VLANs reduce broadcast traffic and improve network segmentation.

**Application:**  
VLANs are used to improve network security, organize departments logically, and enhance network performance.

---

### 2. Trunking (802.1Q)

Trunking is a method used to carry traffic for multiple VLANs over a single physical link between a switch and a router.

**Operation:**  
It uses the IEEE 802.1Q standard to insert a VLAN tag into the Ethernet frame header, identifying which VLAN the frame belongs to.

---

### 3. Inter-VLAN Routing (Router-on-a-Stick)

Since VLANs are separate broadcast domains, a router is required to forward traffic between them.

**Operation:**  
A single physical interface on the router is divided into multiple virtual sub-interfaces. Each sub-interface is assigned:
- An encapsulation type (dot1q)
- A VLAN ID
- An IP address that acts as the Default Gateway for that VLAN

---

## NETWORK TOPOLOGY

A topology was created using:

- **Router0 (1941)**
- **Cisco 2950-24 Switch (hostname: Arpan)**

The switch connects four PCs.

### VLAN Assignment:

- **VLAN 10 (Name: computer)**
  - PC0
  - PC1

- **VLAN 20 (Name: Electronics)**
  - PC2
  - PC3

The connection between the Switch and Router0 is configured as a **Trunk link**.

---

## IP CONFIGURATION TABLE

| Device  | Interface      | IP Address       | Subnet Mask       | Default Gateway | VLAN |
|----------|---------------|------------------|-------------------|----------------|------|
| Router0 | G0/0.10      | 192.168.10.1     | 255.255.255.0     | N/A            | 10   |
| Router0 | G0/0.20      | 192.168.20.1     | 255.255.255.0     | N/A            | 20   |
| PC0     | FastEthernet0| 192.168.10.2     | 255.255.255.0     | 192.168.10.1   | 10   |
| PC1     | FastEthernet0| 192.168.10.3     | 255.255.255.0     | 192.168.10.1   | 10   |
| PC2     | FastEthernet0| 192.168.20.2     | 255.255.255.0     | 192.168.20.1   | 20   |
| PC3     | FastEthernet0| 192.168.20.3     | 255.255.255.0     | 192.168.20.1   | 20   |

---

## CONFIGURATION

### 1. Switch Configuration Commands (VLANs and Ports)


Switch(config)# hostname Arpan
Arpan(config)# vlan 10
Arpan(config-vlan)# name computer
Arpan(config-vlan)# exit
Arpan(config)# vlan 20
Arpan(config-vlan)# name Electronics
Arpan(config-vlan)# exit


### Assigning Ports to VLANs:


Arpan(config)# interface range fa0/2-3
Arpan(config-if-range)# switchport mode access
Arpan(config-if-range)# switchport access vlan 10
Arpan(config-if-range)# exit

Arpan(config)# interface range fa0/4-5
Arpan(config-if-range)# switchport mode access
Arpan(config-if-range)# switchport access vlan 20
Arpan(config-if-range)# exit


### Configuring Trunk Link to Router:


Arpan(config)# interface fa0/1
Arpan(config-if)# switchport mode trunk


---

### 2. Router Configuration Commands (Inter-VLAN Routing)

### Configuring Sub-interface for VLAN 10:


Router0(config)# interface g0/0.10
Router0(config-subif)# encapsulation dot1q 10
Router0(config-subif)# ip address 192.168.10.1 255.255.255.0


### Configuring Sub-interface for VLAN 20:


Router0(config)# interface g0/0.20
Router0(config-subif)# encapsulation dot1q 20
Router0(config-subif)# ip address 192.168.20.1 255.255.255.0


---

## TESTING AND VERIFICATION

After configuration:

- The command `show vlan brief` was used to verify VLAN creation.
- VLAN 10 displayed "computer".
- VLAN 20 displayed "Electronics".

### Ping Testing:

- Ping from PC0 → PC1 (Same VLAN) → Successful
- Ping from PC0 → PC2 (Different VLAN) → Successful after Inter-VLAN routing

This confirms proper VLAN segmentation and successful Inter-VLAN communication.

---

## RESULT

The VLANs were successfully created on the switch, and ports were assigned correctly. Trunking was properly configured using IEEE 802.1Q.

Inter-VLAN routing was successfully implemented using the Router-on-a-Stick method. Devices in different VLANs were able to communicate through the router.

---

## DISCUSSION AND CONCLUSION

During this lab session, VLANs were implemented to segment the network into logical groups ("computer" and "Electronics"). Initially, devices in different VLANs could not communicate because VLANs are separate broadcast domains.

By configuring trunking and implementing Inter-VLAN routing using Router-on-a-Stick with 802.1Q encapsulation, communication between VLAN 10 and VLAN 20 was successfully established.

Hence, the lab was completed with proper knowledge and implementation of VLAN configuration and Inter-VLAN routing using Cisco Packet Tracer.