# 🔐 Site-to-Site IPsec VPN — Without NAT-T

## 📌 Project Overview

This project demonstrates the configuration and verification of a
policy-based Site-to-Site IPsec VPN between two remote sites through
an ISP network.

The VPN provides secure communication between the private networks
of Site-1 and Site-2 using IKEv1, IPsec, ESP, Extended ACLs and
Crypto Maps.

---

## 🎯 Project Objectives

- Configure Site-to-Site IPsec VPN
- Configure IKEv1 Phase 1
- Configure ISAKMP
- Configure pre-shared key authentication
- Configure IPsec Phase 2
- Configure ESP encryption
- Configure Extended ACL for interesting traffic
- Configure Crypto Map
- Establish VPN communication between two sites
- Verify encrypted traffic using Wireshark
- Demonstrate Site-to-Site VPN without NAT-T

---

# 🏗️ 1. Network Topology

The following topology represents the complete Site-to-Site VPN
environment.

Site-1 and Site-2 communicate through an ISP network.

![VPN Topology](01-vpn-topology.png)

### Topology Components

| Component | Function |
|---|---|
| Site-1 Router | VPN Endpoint |
| Site-2 Router | VPN Endpoint |
| ISP Router | WAN Connectivity |
| Site-1 LAN | Private Network |
| Site-2 LAN | Private Network |

### Traffic Flow

```text
Site-1 LAN
    ↓
Site-1 Router
    ↓
IPsec VPN
    ↓
ISP Network
    ↓
IPsec VPN
    ↓
Site-2 Router
    ↓
Site-2 LAN
