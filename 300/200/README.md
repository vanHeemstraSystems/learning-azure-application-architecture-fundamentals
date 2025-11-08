# 200 - Azure Networking Fundamentals

Networking is fundamental for Cloud Engineering. This is a comprehensive networking study guide for you that covers both fundamental networking concepts and Azure-specific networking.​​​​​​​​​​​​​​​​

## What’s Included:

### **Part 1: Networking Fundamentals**

- **IP Addressing Basics**: Understanding octets, classes, public vs private IPs
- **Subnetting and CIDR**: Complete guide with calculation formulas, examples, and quick reference tables
- **OSI and TCP/IP Models**: All 7 layers explained with protocols
- **Routing and Protocols**: DNS, DHCP, NAT, routing tables

### **Part 2: Azure-Specific Networking**

- **Azure Virtual Networks**: Address planning, best practices
- **Azure Subnetting**: The critical “5 reserved IPs” rule and dedicated subnets
- **Network Security**: NSGs, ASGs, Azure Firewall, DDoS Protection, Private Link
- **Hybrid Connectivity**: VPN Gateway, ExpressRoute, VNet Peering
- **Load Balancing**: All Azure load balancing options compared

### **Part 3: Learning Resources**

Complete list of official Microsoft documentation, training paths, and tools specifically for:

- Azure Virtual Networks
- IP Address planning
- Network security
- **AZ-700** certification (Azure Network Engineer Associate)

### **Part 4: Practical Exercises**

Hands-on scenarios for:

- Subnet calculations
- VNet design
- NSG rule creation
- Hub-spoke topology design

### **Part 5: Certification Path**

Recommended progression:

1. **AZ-900** (Fundamentals) →
1. **AZ-104** (Administrator) →
1. **AZ-700** (Network Engineer Associate)

## Key Highlights for Your Technical Test:

**Critical Concepts**:

- ✅ Octet significance in IP addresses (192.168.1.100)
- ✅ CIDR notation (/24, /26, etc.) - NOT “clans” 😊
- ✅ Azure reserves **5 IPs per subnet** (this is crucial!)
- ✅ Subnetting calculations and planning
- ✅ Hub-spoke topology (common in enterprise Azure)

**Quick Reference Tables** included for:

- All CIDR blocks (/32 to /8)
- Subnet mask conversions
- Common port numbers
- Azure CLI and PowerShell commands

# Azure Networking Study Guide for Cloud Engineers

A comprehensive guide covering networking fundamentals and Azure-specific networking concepts essential for Cloud Engineers working with Microsoft Azure.

## Table of Contents

- [Part 1: Networking Fundamentals](#part-1-networking-fundamentals)
  - [IP Addressing Basics](#ip-addressing-basics)
  - [Subnetting and CIDR Notation](#subnetting-and-cidr-notation)
  - [OSI and TCP/IP Models](#osi-and-tcpip-models)
  - [Routing and Protocols](#routing-and-protocols)
- [Part 2: Azure Networking](#part-2-azure-networking)
  - [Azure Virtual Networks (VNets)](#azure-virtual-networks-vnets)
  - [Subnetting in Azure](#subnetting-in-azure)
  - [Network Security](#network-security)
  - [Hybrid Connectivity](#hybrid-connectivity)
  - [Load Balancing and Traffic Management](#load-balancing-and-traffic-management)
- [Part 3: Learning Resources](#part-3-learning-resources)
- [Part 4: Practical Exercises](#part-4-practical-exercises)
- [Part 5: Certification Paths](#part-5-certification-paths)

-----

## Part 1: Networking Fundamentals

### IP Addressing Basics

#### Understanding IPv4 Addresses

An IPv4 address consists of **4 octets** (8 bits each), totaling 32 bits:

**Example**: `192.168.1.100`

- **192** = First octet (8 bits)
- **168** = Second octet (8 bits)
- **1** = Third octet (8 bits)
- **100** = Fourth octet (8 bits)

**Binary representation**:

```
192.168.1.100 in decimal
11000000.10101000.00000001.01100100 in binary
```

#### IP Address Components

Every IP address has two parts:

1. **Network Portion**: Identifies the network
1. **Host Portion**: Identifies the specific device on that network

#### IP Address Classes (Traditional)

|Class|Range                      |Default Subnet Mask|Network Bits|Host Bits|Use Case             |
|-----|---------------------------|-------------------|------------|---------|---------------------|
|A    |1.0.0.0 - 126.255.255.255  |255.0.0.0 (/8)     |8           |24       |Large networks       |
|B    |128.0.0.0 - 191.255.255.255|255.255.0.0 (/16)  |16          |16       |Medium networks      |
|C    |192.0.0.0 - 223.255.255.255|255.255.255.0 (/24)|24          |8        |Small networks       |
|D    |224.0.0.0 - 239.255.255.255|N/A                |N/A         |N/A      |Multicast            |
|E    |240.0.0.0 - 255.255.255.255|N/A                |N/A         |N/A      |Reserved/Experimental|

**Special Addresses**:

- `127.0.0.1` - Loopback address (localhost)
- `0.0.0.0` - Default route or unspecified address
- `255.255.255.255` - Broadcast address

#### Private IP Address Ranges (RFC 1918)

These addresses are NOT routable on the public internet:

|Class|Range                        |CIDR          |Number of Addresses|
|-----|-----------------------------|--------------|-------------------|
|A    |10.0.0.0 - 10.255.255.255    |10.0.0.0/8    |16,777,216         |
|B    |172.16.0.0 - 172.31.255.255  |172.16.0.0/12 |1,048,576          |
|C    |192.168.0.0 - 192.168.255.255|192.168.0.0/16|65,536             |

**When to use**:

- Internal corporate networks
- Home networks
- Azure Virtual Networks (VNets)
- Private cloud environments

#### Public vs Private IP Addresses

**Public IP Addresses**:

- Globally unique
- Routable on the internet
- Assigned by ISPs
- Used for internet-facing resources

**Private IP Addresses**:

- Used within private networks
- Not routable on the internet
- Can be reused in different private networks
- Require NAT (Network Address Translation) to access the internet

### Subnetting and CIDR Notation

#### What is Subnetting?

**Subnetting** is the process of dividing a large network into smaller, manageable sub-networks (subnets).

**Benefits**:

- **Improved security**: Isolate different departments or security zones
- **Better performance**: Reduce broadcast traffic
- **Efficient IP usage**: Allocate only what’s needed
- **Simplified management**: Organize networks logically

#### Understanding Subnet Masks

A **subnet mask** determines which portion of an IP address is the network and which is the host.

**Example**:

```
IP Address:    192.168.1.100
Subnet Mask:   255.255.255.0
Network:       192.168.1.0
Host:          100
```

**Binary View**:

```
IP:            11000000.10101000.00000001.01100100
Subnet Mask:   11111111.11111111.11111111.00000000
               ^^^^^^^^ ^^^^^^^^ ^^^^^^^^ ^^^^^^^^
               Network  Network  Network  Host
```

#### CIDR Notation (Classless Inter-Domain Routing)

**CIDR** notation expresses IP addresses and subnet masks more efficiently.

**Format**: `IP_Address/Prefix_Length`

**Example**: `192.168.1.0/24`

- `/24` means the first 24 bits are the network portion
- Equivalent to subnet mask `255.255.255.0`
- Provides 256 total addresses (254 usable)

#### Common CIDR Blocks

|CIDR|Subnet Mask    |Number of IPs|Usable IPs|Common Use          |
|----|---------------|-------------|----------|--------------------|
|/32 |255.255.255.255|1            |1         |Single host         |
|/31 |255.255.255.254|2            |2         |Point-to-point links|
|/30 |255.255.255.252|4            |2         |Point-to-point links|
|/29 |255.255.255.248|8            |6         |Very small networks |
|/28 |255.255.255.240|16           |14        |Small networks      |
|/27 |255.255.255.224|32           |30        |Small departments   |
|/26 |255.255.255.192|64           |62        |Medium departments  |
|/25 |255.255.255.128|128          |126       |Large departments   |
|/24 |255.255.255.0  |256          |254       |Standard subnet     |
|/23 |255.255.254.0  |512          |510       |Large subnet        |
|/22 |255.255.252.0  |1,024        |1,022     |Very large subnet   |
|/21 |255.255.248.0  |2,048        |2,046     |Extra large subnet  |
|/20 |255.255.240.0  |4,096        |4,094     |Huge subnet         |
|/16 |255.255.0.0    |65,536       |65,534    |Class B equivalent  |
|/8  |255.0.0.0      |16,777,216   |16,777,214|Class A equivalent  |

#### Reserved Addresses in Each Subnet

Every subnet has two reserved addresses:

1. **Network Address** (first IP): Identifies the subnet itself
1. **Broadcast Address** (last IP): Sends to all hosts in subnet

**Example for 192.168.1.0/24**:

- Network Address: `192.168.1.0`
- First Usable: `192.168.1.1`
- Last Usable: `192.168.1.254`
- Broadcast: `192.168.1.255`

#### Subnetting Example

**Scenario**: You have a Class C network `192.168.1.0/24` and need to divide it into 4 subnets.

**Solution**:

- Need 4 subnets = 2² subnets
- Borrow 2 bits from host portion
- New subnet mask: /26 (24 + 2)

**Resulting Subnets**:

|Subnet|Network Address |Range      |Broadcast    |Usable IPs|
|------|----------------|-----------|-------------|----------|
|1     |192.168.1.0/26  |.1 - .62   |192.168.1.63 |62        |
|2     |192.168.1.64/26 |.65 - .126 |192.168.1.127|62        |
|3     |192.168.1.128/26|.129 - .190|192.168.1.191|62        |
|4     |192.168.1.192/26|.193 - .254|192.168.1.255|62        |

#### CIDR Calculation Formula

**Calculate number of hosts**:

```
Number of IPs = 2^(32 - prefix_length)
Usable IPs = 2^(32 - prefix_length) - 2
```

**Example**: `/26` CIDR block

```
Total IPs = 2^(32-26) = 2^6 = 64
Usable IPs = 64 - 2 = 62
```

#### Quick Reference: Powers of 2

|Exponent|Result|Bits|
|--------|------|----|
|2^1     |2     |/31 |
|2^2     |4     |/30 |
|2^3     |8     |/29 |
|2^4     |16    |/28 |
|2^5     |32    |/27 |
|2^6     |64    |/26 |
|2^7     |128   |/25 |
|2^8     |256   |/24 |
|2^9     |512   |/23 |
|2^10    |1,024 |/22 |
|2^11    |2,048 |/21 |
|2^12    |4,096 |/20 |
|2^13    |8,192 |/19 |
|2^14    |16,384|/18 |
|2^15    |32,768|/17 |
|2^16    |65,536|/16 |

### OSI and TCP/IP Models

#### OSI Model (7 Layers)

|Layer|Name        |Function                       |Protocols/Examples  |
|-----|------------|-------------------------------|--------------------|
|7    |Application |User interfaces & applications |HTTP, FTP, SMTP, DNS|
|6    |Presentation|Data formatting, encryption    |SSL/TLS, JPEG, ASCII|
|5    |Session     |Managing sessions & connections|NetBIOS, RPC        |
|4    |Transport   |End-to-end communication       |TCP, UDP            |
|3    |Network     |Routing & logical addressing   |IP, ICMP, OSPF, BGP |
|2    |Data Link   |Physical addressing (MAC)      |Ethernet, Wi-Fi, ARP|
|1    |Physical    |Physical transmission          |Cables, NICs, hubs  |

**Mnemonic**: “Please Do Not Throw Sausage Pizza Away”
(Physical, Data Link, Network, Transport, Session, Presentation, Application)

#### TCP/IP Model (4 Layers)

|Layer|Name             |OSI Equivalent|Function                     |
|-----|-----------------|--------------|-----------------------------|
|4    |Application      |Layers 5-7    |User applications & protocols|
|3    |Transport        |Layer 4       |End-to-end connections       |
|2    |Internet         |Layer 3       |Routing & IP addressing      |
|1    |Network Interface|Layers 1-2    |Physical transmission        |

#### Key Protocols by Layer

**Application Layer (Layer 7)**:

- **HTTP/HTTPS**: Web traffic
- **DNS**: Name resolution
- **SMTP**: Email sending
- **FTP**: File transfer
- **SSH**: Secure remote access

**Transport Layer (Layer 4)**:

- **TCP**: Connection-oriented, reliable
  - Three-way handshake
  - Error checking
  - Ordered delivery
  - Used for: HTTP, FTP, SSH
- **UDP**: Connectionless, faster
  - No handshake
  - No guaranteed delivery
  - Used for: DNS, streaming, VoIP

**Network Layer (Layer 3)**:

- **IP (Internet Protocol)**: Logical addressing & routing
- **ICMP**: Error messages & diagnostics (ping)
- **OSPF/BGP**: Routing protocols

**Data Link Layer (Layer 2)**:

- **Ethernet**: LAN communication
- **Wi-Fi (802.11)**: Wireless communication
- **ARP**: Maps IP to MAC addresses

### Routing and Protocols

#### What is Routing?

**Routing** is the process of selecting paths in a network to send data packets from source to destination.

#### Routing Table

Every router maintains a **routing table** containing:

- Destination networks
- Next hop (gateway)
- Interface to use
- Metric (cost)

**View routing table**:

```bash
# Linux
ip route show
route -n

# Windows
route print

# macOS
netstat -rn
```

#### Static vs Dynamic Routing

**Static Routing**:

- Manually configured routes
- Best for small, stable networks
- Predictable
- No overhead

**Dynamic Routing**:

- Automatically updated using protocols
- Best for large, complex networks
- Adapts to topology changes
- Examples: OSPF, BGP, EIGRP

#### Common Routing Protocols

**Interior Gateway Protocols (IGP)** - Within an organization:

- **OSPF** (Open Shortest Path First): Link-state, fast convergence
- **RIP** (Routing Information Protocol): Distance-vector, older
- **EIGRP** (Enhanced Interior Gateway Routing Protocol): Cisco proprietary

**Exterior Gateway Protocols (EGP)** - Between organizations:

- **BGP** (Border Gateway Protocol): Internet backbone routing

#### Default Gateway

The **default gateway** is the router that forwards traffic to destinations outside the local network.

**Example**:

```
IP Address:     192.168.1.100
Subnet Mask:    255.255.255.0
Default Gateway: 192.168.1.1
```

When `192.168.1.100` wants to reach `8.8.8.8`:

1. Checks if `8.8.8.8` is in local subnet (192.168.1.0/24)
1. It’s not, so sends to default gateway
1. Gateway routes to internet

#### NAT (Network Address Translation)

**NAT** allows multiple devices on a private network to share a single public IP address.

**Types**:

- **Static NAT**: One-to-one mapping
- **Dynamic NAT**: Pool of public IPs
- **PAT (Port Address Translation)**: Many-to-one using ports

**Example**:

```
Private Network: 192.168.1.0/24
Public IP: 203.0.113.5

Device 192.168.1.10:5000 → NAT → 203.0.113.5:5000
Device 192.168.1.20:5001 → NAT → 203.0.113.5:5001
```

#### DNS (Domain Name System)

**DNS** translates domain names to IP addresses.

**Hierarchy**:

```
Root (.)
  └── Top-Level Domain (.com, .org, .nl)
      └── Second-Level Domain (example.com)
          └── Subdomain (www.example.com)
```

**Record Types**:

- **A**: IPv4 address
- **AAAA**: IPv6 address
- **CNAME**: Canonical name (alias)
- **MX**: Mail server
- **TXT**: Text records
- **NS**: Name server

**DNS Query Process**:

1. Client queries DNS resolver
1. Resolver queries root server
1. Root refers to TLD server
1. TLD refers to authoritative server
1. Authoritative server returns IP
1. Resolver caches and returns to client

#### DHCP (Dynamic Host Configuration Protocol)

**DHCP** automatically assigns IP addresses to devices.

**DHCP Process (DORA)**:

1. **Discover**: Client broadcasts looking for DHCP server
1. **Offer**: Server offers IP configuration
1. **Request**: Client requests offered configuration
1. **Acknowledge**: Server confirms assignment

**DHCP Lease Information**:

- IP address
- Subnet mask
- Default gateway
- DNS servers
- Lease duration

-----

## Part 2: Azure Networking

### Azure Virtual Networks (VNets)

#### What is an Azure VNet?

An **Azure Virtual Network (VNet)** is a logically isolated network in the Azure cloud, similar to a traditional network in an on-premises datacenter.

**Key Characteristics**:

- Scoped to a single Azure region
- Scoped to a single subscription
- Provides isolation and segmentation
- Enables communication between Azure resources
- Can connect to on-premises networks
- Can peer with other VNets

#### VNet Address Space

When creating a VNet, you must define an **address space** using CIDR notation.

**Best Practices**:

- Use private IP ranges (RFC 1918)
- Plan for future growth
- Avoid overlapping with other VNets or on-premises networks
- Don’t create unnecessarily large VNets (avoid /16 if you only need /24)

**Common VNet Sizes**:

```
Small:    10.0.0.0/24    (256 IPs)
Medium:   10.0.0.0/22    (1,024 IPs)
Large:    10.0.0.0/20    (4,096 IPs)
X-Large:  10.0.0.0/16    (65,536 IPs)
```

**Example VNet Planning**:

```
Organization's Azure Footprint:
- Production VNet:    10.0.0.0/16
- Development VNet:   10.1.0.0/16
- Testing VNet:       10.2.0.0/16
- Management VNet:    10.3.0.0/16

On-Premises Network:  192.168.0.0/16
(No overlap!)
```

#### VNet Components

1. **Address Space**: Overall IP range for the VNet
1. **Subnets**: Subdivisions within the VNet
1. **Network Security Groups (NSGs)**: Firewall rules
1. **Route Tables**: Custom routing
1. **Service Endpoints**: Direct access to Azure services
1. **Private Endpoints**: Private IPs for Azure services

### Subnetting in Azure

#### Azure Subnet Basics

**Subnets** in Azure allow you to segment your VNet into logical sections.

**Important Azure Rules**:

- Azure reserves **5 IP addresses** in each subnet:
  - `.0` - Network address
  - `.1` - Default gateway
  - `.2` and `.3` - Azure DNS
  - `.255` (last IP) - Broadcast

**Example for 10.0.1.0/24**:

```
Total IPs:           256
Azure Reserved:      5
Usable for VMs:      251

Reserved IPs:
10.0.1.0    - Network address
10.0.1.1    - Default gateway
10.0.1.2    - Azure DNS
10.0.1.3    - Azure DNS
10.0.1.255  - Broadcast

Available:
10.0.1.4 - 10.0.1.254
```

#### Dedicated Subnets for Azure Services

Some Azure services require **dedicated subnets** with specific names:

|Service            |Subnet Name        |Minimum Size|Recommended Size|
|-------------------|-------------------|------------|----------------|
|Azure Firewall     |AzureFirewallSubnet|/26         |/24             |
|VPN Gateway        |GatewaySubnet      |/29         |/27             |
|Azure Bastion      |AzureBastionSubnet |/27         |/26             |
|Application Gateway|(custom)           |/28         |/24             |

**Example VNet Architecture**:

```
VNet: 10.0.0.0/16

Subnets:
├── GatewaySubnet:         10.0.0.0/27    (VPN Gateway)
├── AzureFirewallSubnet:   10.0.1.0/24    (Azure Firewall)
├── AzureBastionSubnet:    10.0.2.0/27    (Azure Bastion)
├── WebSubnet:             10.0.10.0/24   (Web tier)
├── AppSubnet:             10.0.11.0/24   (App tier)
├── DatabaseSubnet:        10.0.12.0/24   (Database tier)
└── ManagementSubnet:      10.0.255.0/24  (Jump boxes, tools)
```

#### Subnet Delegation

**Subnet delegation** allows Azure services to create service-specific resources in a subnet.

**Services that support delegation**:

- Azure Container Instances
- Azure Kubernetes Service (AKS)
- Azure SQL Managed Instance
- Azure NetApp Files
- Azure App Service

**When to delegate**:

- Service requires network integration
- Service needs to inject resources into your VNet
- Service manages network configuration

### Network Security

#### Network Security Groups (NSGs)

**NSGs** are virtual firewalls that filter network traffic based on rules.

**NSG Rules**:

- **Priority**: 100-4096 (lower = higher priority)
- **Name**: Descriptive rule name
- **Source/Destination**: IP, CIDR, Service Tag, or ASG
- **Protocol**: TCP, UDP, ICMP, Any
- **Port Range**: Single port or range
- **Action**: Allow or Deny

**Default Rules** (cannot be deleted):

```
Inbound:
- AllowVNetInBound      (Priority 65000)
- AllowAzureLoadBalancerInBound (Priority 65001)
- DenyAllInBound        (Priority 65500)

Outbound:
- AllowVNetOutBound     (Priority 65000)
- AllowInternetOutBound (Priority 65001)
- DenyAllOutBound       (Priority 65500)
```

**Example NSG Rules**:

```
Name: Allow-SSH
Priority: 100
Source: 203.0.113.0/24 (Your office)
Destination: *
Port: 22
Protocol: TCP
Action: Allow

Name: Allow-HTTPS
Priority: 110
Source: Internet
Destination: *
Port: 443
Protocol: TCP
Action: Allow

Name: Deny-All-Inbound
Priority: 4096
Source: *
Destination: *
Port: *
Protocol: *
Action: Deny
```

**NSG Best Practices**:

- Apply principle of least privilege
- Use Service Tags when possible
- Document your rules
- Use Application Security Groups for complex scenarios
- Apply NSGs at subnet level for broad protection
- Apply NSGs at NIC level for granular control

#### Application Security Groups (ASGs)

**ASGs** allow you to group VMs and define NSG rules based on groups rather than IP addresses.

**Benefits**:

- Simplify security rules
- Easy to manage as infrastructure grows
- No need to update rules when IPs change

**Example**:

```
ASGs:
├── WebServers
├── AppServers
└── DatabaseServers

NSG Rule:
Allow-Web-to-App
Source: WebServers (ASG)
Destination: AppServers (ASG)
Port: 8080
Protocol: TCP
Action: Allow
```

#### Azure Firewall

**Azure Firewall** is a managed, cloud-based network security service.

**Features**:

- Stateful firewall
- Built-in high availability
- Application and network rules
- Threat intelligence
- FQDN filtering
- SNAT/DNAT support
- Integration with Azure Monitor

**Rule Types**:

1. **Application Rules**: Filter based on FQDN
1. **Network Rules**: Filter based on IP, port, protocol
1. **NAT Rules**: DNAT for inbound connections

**Use Cases**:

- Hub VNet in hub-spoke topology
- Centralized outbound filtering
- Protecting workloads
- Micro-segmentation

#### Azure DDoS Protection

**DDoS Protection** defends against distributed denial-of-service attacks.

**Tiers**:

1. **Basic**: Automatically enabled, free
1. **Standard**: Advanced protection, costs apply

**Standard Features**:

- Always-on monitoring
- Adaptive tuning
- Attack analytics
- Metrics and alerts
- DDoS rapid response support

#### Azure Private Link

**Private Link** provides private connectivity to Azure services over a private endpoint.

**Benefits**:

- Access Azure services over private IP
- No public internet exposure
- Works with on-premises networks
- Data exfiltration protection

**Supported Services**:

- Azure Storage
- Azure SQL Database
- Azure Cosmos DB
- Azure Key Vault
- Many more

**Architecture**:

```
Your VNet
  └── Subnet
      └── Private Endpoint (10.0.1.5)
          └── Private Link
              └── Azure SQL Database
                  (No public IP needed!)
```

### Hybrid Connectivity

#### VPN Gateway

**VPN Gateway** enables encrypted connectivity between Azure and on-premises networks.

**Connection Types**:

1. **Site-to-Site (S2S)**: Connect entire networks
1. **Point-to-Site (P2S)**: Connect individual clients
1. **VNet-to-VNet**: Connect Azure VNets

**Gateway SKUs**:

|SKU   |Bandwidth|Tunnels|P2S Connections|
|------|---------|-------|---------------|
|Basic |100 Mbps |10     |128            |
|VpnGw1|650 Mbps |30     |250            |
|VpnGw2|1 Gbps   |30     |500            |
|VpnGw3|1.25 Gbps|30     |1000           |

**VPN Protocols**:

- **IKEv2**: Modern, secure
- **OpenVPN**: Cross-platform
- **SSTP**: Windows-based

**Site-to-Site VPN Requirements**:

- On-premises VPN device
- Public IPv4 address
- IPsec/IKE support
- Compatible device (check Azure compatibility list)

#### Azure ExpressRoute

**ExpressRoute** provides private, dedicated connections to Azure.

**Benefits**:

- Faster speeds (50 Mbps - 100 Gbps)
- More reliable than internet
- Lower latency
- Private connectivity
- SLA-backed

**Connection Models**:

1. **CloudExchange Co-location**: At provider’s facility
1. **Point-to-Point Ethernet**: Direct connection
1. **Any-to-Any (IPVPN)**: Through MPLS provider
1. **ExpressRoute Direct**: Direct to Microsoft edge

**Peering Types**:

- **Private Peering**: Access VNets
- **Microsoft Peering**: Access Microsoft 365, Azure public services

**Use Cases**:

- Mission-critical workloads
- Large data transfers
- Disaster recovery
- Hybrid cloud scenarios

#### VNet Peering

**VNet Peering** connects two VNets, enabling resources to communicate.

**Types**:

1. **Regional Peering**: VNets in same region
1. **Global Peering**: VNets in different regions

**Characteristics**:

- Low latency (Microsoft backbone)
- No bandwidth constraints
- No downtime
- Non-transitive (A↔B and B↔C doesn’t mean A↔C)

**Use Cases**:

- Hub-spoke topology
- Cross-subscription connectivity
- Multi-region applications
- Service decomposition

**Peering Configuration**:

```
VNet1 (10.0.0.0/16) ←→ VNet2 (10.1.0.0/16)

Requirements:
✓ Non-overlapping address spaces
✓ Peering created in both directions
✓ NSG rules allow traffic
✓ Routes configured if using gateways
```

### Load Balancing and Traffic Management

#### Azure Load Balancer

**Azure Load Balancer** distributes network traffic across multiple VMs.

**SKUs**:

1. **Basic**: Free, limited features
1. **Standard**: Production-ready, SLA-backed

**Types**:

- **Public Load Balancer**: Internet-facing
- **Internal Load Balancer**: Private, within VNet

**Load Balancing Methods**:

- **5-tuple hash**: Source IP, port, destination IP, port, protocol
- **Source IP affinity**: Session persistence

**Components**:

- **Frontend IP**: Load balancer’s IP address
- **Backend Pool**: VMs to distribute traffic to
- **Health Probe**: Checks VM health
- **Load Balancing Rules**: Traffic distribution rules
- **Inbound NAT Rules**: Port forwarding

**Example Configuration**:

```
Public Load Balancer:
Frontend IP: 203.0.113.5
Backend Pool: Web-VMs
Health Probe: HTTP:80/health
Rule: 
  - Frontend 80 → Backend 80
  - Protocol: TCP
  - Session: None
```

#### Azure Application Gateway

**Application Gateway** is a Layer 7 (HTTP/HTTPS) load balancer.

**Features**:

- URL-based routing
- SSL termination
- Web Application Firewall (WAF)
- Autoscaling
- Cookie-based session affinity
- WebSocket support
- HTTP/2 support

**Components**:

- **Frontend IP**: Public or private IP
- **Listeners**: Receive traffic (HTTP/HTTPS)
- **Backend Pools**: Target resources
- **HTTP Settings**: Connection configuration
- **Rules**: Route traffic based on URL

**Routing Types**:

1. **Path-based**: `/images/*` → ImageServers
1. **Multi-site**: `sales.contoso.com` → SalesServers

**Example**:

```
Application Gateway:
Frontend: 203.0.113.10

Listeners:
- HTTP:80  → Redirect to HTTPS
- HTTPS:443 → Backend pool

Rules:
- /api/*     → API servers
- /images/*  → Storage account
- /*         → Web servers
```

#### Azure Front Door

**Azure Front Door** is a global Layer 7 load balancer and CDN.

**Features**:

- Global load balancing
- CDN capabilities
- SSL offload
- URL-based routing
- WAF integration
- Custom domains
- Health probes

**Use Cases**:

- Multi-region applications
- Global web applications
- Microservices architecture
- A/B testing
- Blue-green deployments

**Routing Methods**:

- **Latency**: Route to fastest backend
- **Priority**: Failover routing
- **Weighted**: Traffic distribution
- **Session affinity**: Sticky sessions

#### Azure Traffic Manager

**Traffic Manager** is a DNS-based global load balancer.

**Routing Methods**:

1. **Priority**: Active-passive failover
1. **Weighted**: Distribute traffic by percentage
1. **Performance**: Route to nearest endpoint
1. **Geographic**: Route by user location
1. **Multivalue**: Return multiple healthy endpoints
1. **Subnet**: Route based on source IP

**Use Cases**:

- Disaster recovery
- Multi-region deployments
- Geographic routing
- Migration scenarios

**Example**:

```
Traffic Manager Profile:
Domain: app.trafficmanager.net

Endpoints:
- Priority 1: West Europe (Primary)
- Priority 2: North Europe (Failover)

Routing: Priority
Health Check: HTTPS:443/health
```

-----

## Part 3: Learning Resources

### Official Microsoft Documentation

#### Core Azure Networking Resources

1. **Azure Virtual Network Documentation**
- URL: https://learn.microsoft.com/en-us/azure/virtual-network/
- Topics: VNets, subnets, IP addressing, peering
1. **Azure Networking Fundamentals**
- URL: https://learn.microsoft.com/en-us/azure/networking/fundamentals/
- Topics: Overview of all Azure networking services
1. **Plan for IP Addressing - Cloud Adoption Framework**
- URL: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/plan-for-ip-addressing
- Topics: IP planning, CIDR, subnet design, IPv6
1. **Azure Network Security Best Practices**
- URL: https://learn.microsoft.com/en-us/azure/security/fundamentals/network-best-practices
- Topics: NSGs, segmentation, security architecture
1. **Azure Networking Architecture Documentation**
- URL: https://learn.microsoft.com/en-us/azure/networking/fundamentals/architecture-guides
- Topics: Hub-spoke, network topologies, reference architectures

### Microsoft Learn Training Paths

#### Foundational

1. **Introduction to Azure Networking Fundamentals**
- URL: https://learn.microsoft.com/en-us/training/modules/azure-networking-fundamentals/
- Duration: ~1 hour
- Level: Beginner
1. **Configure Virtual Networks**
- Part of AZ-104 learning path
- Topics: VNet creation, subnetting, IP addressing

#### Advanced

1. **AZ-700: Design and Implement Microsoft Azure Networking Solutions**
- URL: https://learn.microsoft.com/en-us/training/paths/design-implement-microsoft-azure-networking-solutions-az-700/
- Duration: ~20 hours
- Level: Intermediate to Advanced
- Topics:
  - Core networking infrastructure
  - Hybrid networking
  - Application delivery services
  - Private access to Azure services
  - Network security
  - Network monitoring

### Networking Fundamentals Resources

#### Understanding IP Addressing and Subnetting

1. **Understanding IP Addresses, Subnets, and CIDR - DigitalOcean**
- URL: https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking
- Comprehensive guide to IP fundamentals
1. **Introduction to Subnetting - GeeksforGeeks**
- URL: https://www.geeksforgeeks.org/computer-networks/introduction-to-subnetting/
- Clear explanations with examples
1. **CIDR Calculator**
- URL: https://cidr.xyz/
- Visual tool for understanding CIDR notation

#### OSI and TCP/IP Models

1. **Networking Basics: OSI Model and TCP/IP**
- URL: https://scalac.io/blog/networking-basics/
- Beginner-friendly explanation

### Tools and Calculators

1. **Subnet Calculator**
- Various online tools:
  - https://www.subnet-calculator.com/
  - https://www.calculator.net/ip-subnet-calculator.html
1. **IP Address Guide**
- Comprehensive IP reference:
  - https://www.ipaddressguide.com/
1. **Azure Speed Test**
- URL: https://www.azurespeed.com/
- Test Azure region latency
1. **Azure Network Watcher**
- Built into Azure portal
- IP flow verify, NSG diagnostics, packet capture

-----

## Part 4: Practical Exercises

### Exercise 1: IP Address and Subnet Calculations

**Practice Problems**:

1. **Calculate usable IPs**:
- Network: `10.0.0.0/24`
- Question: How many usable IPs?
- Answer: 254 (256 - 2)
1. **Determine subnet mask**:
- Need 50 hosts per subnet
- Question: Minimum subnet mask?
- Answer: /26 (64 IPs, 62 usable)
1. **Split a network**:
- Network: `192.168.1.0/24`
- Requirement: 4 equal subnets
- Answer: Four /26 networks
1. **Azure subnet planning**:
- Network: `10.1.0.0/24`
- Question: Usable IPs in Azure?
- Answer: 251 (256 - 5 Azure reserved)

### Exercise 2: Azure VNet Design

**Scenario**: Design a VNet for a three-tier application

**Requirements**:

- Web tier: 20 VMs
- App tier: 30 VMs
- Database tier: 5 VMs
- VPN Gateway
- Azure Bastion
- Future growth: 50% capacity

**Solution**:

```
VNet: 10.0.0.0/16

Subnets:
├── GatewaySubnet:       10.0.0.0/27    (32 IPs)
├── AzureBastionSubnet:  10.0.1.0/26    (64 IPs)
├── WebSubnet:           10.0.10.0/25   (128 IPs - 30 for growth)
├── AppSubnet:           10.0.11.0/25   (128 IPs - 45 for growth)
└── DatabaseSubnet:      10.0.12.0/27   (32 IPs - 8 for growth)
```

### Exercise 3: NSG Rules Design

**Scenario**: Secure a web application

**Requirements**:

- Allow HTTPS from internet
- Allow SSH only from management subnet
- Allow database access only from app tier
- Deny all other traffic

**NSG Rules**:

```
WebSubnet-NSG:
├── Allow-HTTPS-Inbound (Priority 100)
│   Source: Internet
│   Port: 443
│   Action: Allow
├── Allow-SSH-from-Mgmt (Priority 110)
│   Source: 10.0.255.0/24
│   Port: 22
│   Action: Allow
└── Deny-All-Inbound (Priority 4096)
    Source: *
    Action: Deny

DatabaseSubnet-NSG:
├── Allow-SQL-from-App (Priority 100)
│   Source: 10.0.11.0/25
│   Port: 1433
│   Action: Allow
└── Deny-All-Inbound (Priority 4096)
    Source: *
    Action: Deny
```

### Exercise 4: Hub-Spoke Topology

**Design a hub-spoke network**:

```
Hub VNet (10.0.0.0/16):
├── GatewaySubnet:        10.0.0.0/24
├── AzureFirewallSubnet:  10.0.1.0/24
└── SharedServicesSubnet: 10.0.10.0/24

Spoke VNets (Peered to Hub):
├── Production (10.1.0.0/16)
│   ├── WebSubnet:      10.1.1.0/24
│   ├── AppSubnet:      10.1.2.0/24
│   └── DataSubnet:     10.1.3.0/24
│
└── Development (10.2.0.0/16)
    ├── WebSubnet:      10.2.1.0/24
    ├── AppSubnet:      10.2.2.0/24
    └── DataSubnet:     10.2.3.0/24

Traffic Flow:
1. On-premises → VPN Gateway (Hub)
2. Internet traffic → Azure Firewall (Hub)
3. Spoke-to-Spoke → Through Hub (requires UDR)
```

-----

## Part 5: Certification Paths

### Recommended Certification Journey

#### Level 1: Fundamentals

**AZ-900: Azure Fundamentals**

- **Topics**: Basic cloud concepts, Azure services overview
- **Networking Coverage**: Basic VNet, NSG concepts
- **Duration**: 1-2 weeks study
- **Exam**: $99 USD
- **URL**: https://learn.microsoft.com/en-us/credentials/certifications/azure-fundamentals/

**Prerequisites**: None (entry-level)

#### Level 2: Associate

**AZ-104: Azure Administrator**

- **Topics**: Azure administration, including networking
- **Networking Coverage**:
  - VNets and subnets
  - NSGs
  - VNet peering
  - VPN Gateway basics
  - Load Balancer
  - Azure DNS
- **Duration**: 4-6 weeks study
- **Exam**: $165 USD
- **URL**: https://learn.microsoft.com/en-us/credentials/certifications/azure-administrator/

**Prerequisites**: Recommended 6 months Azure experience

#### Level 3: Specialized

**AZ-700: Azure Network Engineer Associate**

- **Topics**: Advanced Azure networking
- **Networking Coverage**:
  - Design and implement core networking infrastructure
  - Design and implement routing
  - Secure and monitor networks
  - Design and implement Private access to Azure Services
  - Design and implement Azure ExpressRoute
  - Load balancing (all types)
  - Application Gateway and Front Door
  - Azure Firewall
  - Network monitoring and troubleshooting
- **Duration**: 8-12 weeks study
- **Exam**: $165 USD
- **URL**: https://learn.microsoft.com/en-us/credentials/certifications/azure-network-engineer-associate/

**Prerequisites**:

- Understanding of networking fundamentals (TCP/IP, DNS, routing)
- Experience with Azure administration

**Study Resources for AZ-700**:

1. Microsoft Learn training path
1. Hands-on labs in Azure
1. Practice exams
1. Community study groups

### Complementary Certifications

**CompTIA Network+**

- Strong networking fundamentals
- Vendor-neutral
- Good foundation before Azure-specific certs

**Cisco CCNA**

- Deep networking knowledge
- Industry-recognized
- Strong routing/switching foundation

-----

## Quick Reference Guides

### CIDR Quick Reference

```
/32 = 255.255.255.255 = 1 IP
/31 = 255.255.255.254 = 2 IPs
/30 = 255.255.255.252 = 4 IPs
/29 = 255.255.255.248 = 8 IPs
/28 = 255.255.255.240 = 16 IPs
/27 = 255.255.255.224 = 32 IPs
/26 = 255.255.255.192 = 64 IPs
/25 = 255.255.255.128 = 128 IPs
/24 = 255.255.255.0 = 256 IPs
/23 = 255.255.254.0 = 512 IPs
/22 = 255.255.252.0 = 1,024 IPs
/21 = 255.255.248.0 = 2,048 IPs
/20 = 255.255.240.0 = 4,096 IPs
/19 = 255.255.224.0 = 8,192 IPs
/18 = 255.255.192.0 = 16,384 IPs
/17 = 255.255.128.0 = 32,768 IPs
/16 = 255.255.0.0 = 65,536 IPs
```

### Azure Reserved IPs per Subnet

```
Every Azure subnet reserves 5 IPs:
.0   → Network address
.1   → Default gateway
.2   → Azure DNS
.3   → Azure DNS
.255 → Broadcast address

Example: 10.0.1.0/24
Reserved: 10.0.1.0, .1, .2, .3, .255
Available: 10.0.1.4 through 10.0.1.254
Total Available: 251 IPs
```

### Port Numbers Reference

```
Common Well-Known Ports:
20/21   → FTP
22      → SSH
23      → Telnet
25      → SMTP
53      → DNS
80      → HTTP
110     → POP3
143     → IMAP
443     → HTTPS
445     → SMB
1433    → SQL Server
1521    → Oracle
3306    → MySQL
3389    → RDP
5432    → PostgreSQL
```

### Azure Networking Commands

**Azure CLI**:

```bash
# Create VNet
az network vnet create \
  --name MyVNet \
  --resource-group MyRG \
  --address-prefix 10.0.0.0/16 \
  --subnet-name MySubnet \
  --subnet-prefix 10.0.1.0/24

# Create NSG
az network nsg create \
  --name MyNSG \
  --resource-group MyRG

# Add NSG rule
az network nsg rule create \
  --nsg-name MyNSG \
  --resource-group MyRG \
  --name Allow-SSH \
  --priority 100 \
  --source-address-prefixes '*' \
  --destination-port-ranges 22 \
  --access Allow \
  --protocol Tcp
```

**PowerShell**:

```powershell
# Create VNet
$vnet = New-AzVirtualNetwork `
  -Name MyVNet `
  -ResourceGroupName MyRG `
  -Location westeurope `
  -AddressPrefix 10.0.0.0/16

# Create subnet
Add-AzVirtualNetworkSubnetConfig `
  -Name MySubnet `
  -AddressPrefix 10.0.1.0/24 `
  -VirtualNetwork $vnet

$vnet | Set-AzVirtualNetwork
```

-----

## Study Plan Recommendation

### Week 1-2: Networking Fundamentals

- IP addressing and binary
- Subnetting calculations
- CIDR notation
- OSI and TCP/IP models
- Basic routing concepts

### Week 3-4: Azure Networking Basics

- Azure VNets and subnets
- IP address planning in Azure
- NSGs and security
- Azure networking services overview

### Week 5-6: Advanced Azure Networking

- VNet peering
- VPN Gateway and ExpressRoute
- Load balancing options
- Azure Firewall
- Private Link and endpoints

### Week 7-8: Practice and Hands-On

- Build lab environments
- Practice subnet calculations
- Design network architectures
- Troubleshooting scenarios
- Practice exams (if pursuing certification)

-----

## Additional Resources

### Books

- “TCP/IP Illustrated, Volume 1” by W. Richard Stevens
- “Computer Networking: A Top-Down Approach” by Kurose and Ross
- “Exam Ref AZ-700 Designing and Implementing Microsoft Azure Networking Solutions” by Microsoft Press

### Video Courses

- Pluralsight: Azure Networking courses
- LinkedIn Learning: Azure Network Engineer path
- YouTube: John Savill’s Azure networking videos
- Microsoft Learn: Free online training

### Community Resources

- r/Azure subreddit
- Microsoft Tech Community
- Azure networking blog
- Stack Overflow

### Practice Tools

- Azure Free Account (12 months free services)
- Azure Sandbox environments
- Microsoft Learn hands-on labs
- Subnet calculators

-----

## Conclusion

Mastering Azure networking requires a solid foundation in networking fundamentals combined with deep knowledge of Azure-specific implementations. This guide provides the roadmap, but hands-on practice is essential.

**Key Takeaways**:

1. Understand IP addressing and CIDR notation thoroughly
1. Practice subnet calculations regularly
1. Know the OSI and TCP/IP models
1. Plan Azure networks carefully (avoid overlapping address spaces)
1. Remember Azure reserves 5 IPs per subnet
1. Use NSGs and ASGs for security
1. Choose the right load balancing solution for your scenario
1. Practice with real Azure environments

**Next Steps**:

1. Start with fundamental networking concepts
1. Practice subnetting calculations
1. Create a free Azure account
1. Build sample network architectures
1. Consider pursuing AZ-700 certification
1. Join Azure networking communities
