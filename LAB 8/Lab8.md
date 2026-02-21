# LAB 8: Server Configuration – DHCP, DNS, and Web Server in Cisco Packet Tracer

---

## OBJECTIVES

1. To understand the working mechanism of Dynamic Host Configuration Protocol (DHCP) for automatic IP address assignment.
2. To configure a Domain Name System (DNS) server to translate domain names into IP addresses.
3. To set up and configure a Web Server (HTTP) to host a website and access it through client PCs using a web browser.

---

## THEORY

### 1. DHCP (Dynamic Host Configuration Protocol)

DHCP is a network management protocol used in TCP/IP networks.

**Operation:**  
DHCP automatically assigns an IP address along with subnet mask, default gateway, and DNS server information to client devices. This eliminates the need for manual IP configuration and prevents IP conflicts.

**Application:**  
Used in enterprise and home networks to efficiently manage IP allocation and simplify administration.

---

### 2. DNS (Domain Name System)

DNS is a hierarchical and decentralized naming system used to translate human-readable domain names into numerical IP addresses.

**Operation:**  
When a user types a domain name (e.g., www.hcoe.com), the DNS server resolves it into the corresponding IP address (e.g., 192.168.1.2), allowing devices to communicate.

---

### 3. Web Server (HTTP)

A Web Server stores and delivers web content to client browsers.

**Operation:**  
When a client enters a URL, the browser sends a request using HTTP protocol. The server responds by sending the HTML file, which is displayed in the browser.

---

## NETWORK TOPOLOGY

A topology was created using:

- One **Server-PT (Server0)**
- One **2960-24TT Switch (Switch0)**
- Two client PCs (PC0 and PC1)

The server acts as a multi-functional device providing DHCP, DNS, and Web services to the network.

All devices are connected within the same LAN (192.168.1.0/24).

---

## IP ADDRESSING SCHEME

| Device  | Interface       | IP Address      | Subnet Mask       | Default Gateway | DNS Server     | Allocation Method |
|----------|----------------|----------------|-------------------|----------------|---------------|-------------------|
| Server0 | FastEthernet0  | 192.168.1.2     | 255.255.255.0     | 0.0.0.0        | 127.0.0.1      | Static            |
| PC0     | FastEthernet0  | 192.168.1.3     | 255.255.255.0     | 0.0.0.0        | 192.168.1.2    | DHCP              |
| PC1     | FastEthernet0  | 192.168.1.4     | 255.255.255.0     | 0.0.0.0        | 192.168.1.2    | DHCP              |

---

## CONFIGURATION

### 1. Server Static IP Configuration

Server0 was assigned a static IP address to ensure it remains reachable.

- IP Address: 192.168.1.2
- Subnet Mask: 255.255.255.0

---

### 2. DHCP Configuration

DHCP service was enabled on Server0 with the following settings:

- Service: ON
- Pool Name: LAN_POOL
- Default Gateway: 192.168.1.1
- DNS Server: 192.168.1.2
- Start IP Address: 192.168.1.10
- Maximum Number of Users: 50

Client PCs were configured to obtain IP addresses automatically using DHCP.

---

### 3. DNS and Web Server Configuration

#### HTTP Service

- HTTP: Enabled
- HTTPS: Enabled

The `index.html` file was edited to display:


Welcome From Arpan


---

#### DNS Service

DNS service was enabled and the following record was added:

- Name: www.hcoe.com
- Type: A Record
- Address: 192.168.1.2

This allows the domain name to resolve to the server’s IP address.

---

## VERIFICATION

### 1. DHCP Verification

- PC0 and PC1 were set to DHCP mode.
- IP addresses were assigned automatically.
- DNS server address was received correctly.
- No manual configuration was required.

---

### 2. DNS Verification

From PC0, the following command was executed:


ping www.hcoe.com


The DNS server successfully resolved the domain name to 192.168.1.2 and replies were received without packet loss.

---

### 3. Web Server Verification

The web browser on PC0 was opened and the URL:


http://www.hcoe.com


was entered.

The custom HTML page hosted on Server0 was displayed successfully.

---

## RESULT

The server was successfully configured to provide DHCP, DNS, and Web services.

- Client PCs obtained IP addresses dynamically.
- Domain name was resolved correctly.
- The hosted web page was accessed successfully via browser.

All configurations were verified and functioned as expected.

---

## DISCUSSION AND CONCLUSION

During this lab session, a centralized server was configured to provide DHCP, DNS, and HTTP services. The client PCs obtained IP addresses dynamically from the DHCP pool, eliminating manual IP configuration.

The DNS server successfully translated the domain name `www.hcoe.com` into the IP address 192.168.1.2, enabling seamless connectivity. The Web Server delivered the custom HTML page when accessed via the browser.

Hence, the lab was completed successfully with proper understanding and implementation of Server Configuration including DHCP, DNS, and Web Server using Cisco Packet Tracer.