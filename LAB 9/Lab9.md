# LAB 9: Wireless Network Setup and Packet Analysis using Cisco Packet Tracer

---

## OBJECTIVES

1. To understand the working mechanism of a Wireless Local Area Network (WLAN) and the configuration of a Wireless Router.
2. To configure Service Set Identifier (SSID) and WPA2 security protocols to secure the wireless network.
3. To establish connectivity between client laptops and the Wireless Router.
4. To verify the connection using packet analysis tools (Ping).

---

## THEORY

### 1. WLAN (Wireless Local Area Network)

A WLAN is a wireless computer network that links two or more devices using wireless communication to form a local area network (LAN) within a limited area such as a home, school, or laboratory.

**Operation:**  
WLAN uses high-frequency radio waves (2.4 GHz or 5 GHz) to transmit data between devices and a wireless router or access point, eliminating the need for physical cables.

---

### 2. SSID (Service Set Identifier)

The SSID is the primary name associated with an 802.11 wireless local area network.

**Operation:**  
It acts as a unique identifier that distinguishes one WLAN from another. Client devices scan for available SSIDs to identify and connect to the correct wireless network.

---

### 3. WPA2 (Wi-Fi Protected Access 2)

WPA2 is a wireless security protocol that protects wireless networks from unauthorized access.

**Operation:**  
WPA2-Personal uses AES encryption and requires users to enter a Pre-Shared Key (PSK) to authenticate with the network.

---

## NETWORK TOPOLOGY

A topology was created using:

- One **Wireless Router (WRT300N named Wireless Router0)**
- Two client devices: **Laptop0** and **Laptop1**

The Wireless Router acts as the central access point, broadcasting the wireless signal to the laptops.

---

## IP CONFIGURATION TABLE

| Device            | Interface     | IP Address      | Subnet Mask       | Default Gateway | Allocation Method |
|------------------|--------------|----------------|-------------------|----------------|------------------|
| Wireless Router0 | LAN/Wireless | 192.168.0.1     | 255.255.255.0     | -              | Static           |
| Laptop0          | Wireless0    | 192.168.0.102   | 255.255.255.0     | 192.168.0.1    | DHCP             |
| Laptop1          | Wireless0    | 192.168.0.103   | 255.255.255.0     | 192.168.0.1    | DHCP             |

The Wireless Router was configured to act as a DHCP server, automatically assigning IP addresses to connected clients.

---

## CONFIGURATION PROCEDURE

### 1. Router Setup

- Accessed the GUI tab of the Wireless Router.
- Under **Wireless Settings**, the SSID was set to:


HCOE


- Under **Wireless Security**, WPA2-Personal was selected.
- Encryption type: AES
- Pre-Shared Key:


hcoe@123


---

### 2. Client Connection

On Laptop0:

- Opened the **PC Wireless** application.
- Navigated to the **Connect** tab.
- The system scanned for available wireless networks.
- The SSID **HCOE** was detected.
- Selected the network and clicked **Connect**.

---

### 3. Authentication

- Entered the Pre-Shared Key:


hcoe@123


- Authentication was successful.

---

### 4. IP Assignment

After successful authentication:

- The laptops automatically requested IP addresses from the router.
- IP addresses were assigned dynamically via DHCP.
- Default Gateway and network settings were configured automatically.

---

## TESTING

### Connectivity Verification

To verify connectivity and packet flow:

On Laptop0, opened Command Prompt and entered:


ping 192.168.0.103


Replies were received successfully from Laptop1.

Ping statistics showed:
- 4 packets sent
- 4 packets received
- 0% packet loss

This confirms successful wireless communication.

---

## RESULT

The wireless network was successfully configured.

- SSID was broadcast correctly.
- WPA2 security protected the network.
- Client laptops authenticated successfully.
- IP addresses were assigned dynamically.
- Connectivity between laptops was verified using ping.

---

## DISCUSSION AND CONCLUSION

During this lab session, a wireless network was successfully established using a WRT300N router. The SSID "HCOE" was configured and secured using WPA2-Personal encryption with a pre-shared key.

The client laptops were able to detect the wireless network, authenticate using the correct credentials, and obtain IP addresses dynamically via DHCP. Connectivity was verified using the ping command, which showed 0% packet loss.

Hence, the lab was completed successfully with proper knowledge and implementation of Wireless Network Setup and Packet Analysis using Cisco Packet Tracer.