## 🔐 Policy-Based Site-to-Site IPsec VPN

### 📌 Project Overview

Configured a **policy-based Site-to-Site IPsec VPN** between **Site-1 and Site-2** through an ISP router.

The VPN uses **IKEv1** for Phase 1 negotiation and **IPsec/ESP** for encrypted data traffic.

### 🏗️ Network Topology

![VPN Topology]([VPN/SITE-TO-SITE-WITHOUT-NAT/vpn-topology.png](https://github.com/Ayush52-s/EVE-NG-ALL-PROJECT/blob/main/VPN/SITE-TO-SITE-WITHOUT-NAT/vpn-topology.png))

### 🌐 IP Addressing

| Device | Interface | IP Address |
|---|---|---|
| Site-1 | Gi0/0 | 11.1.1.1 |
| ISP | Gi0/0 | 11.1.1.10 |
| ISP | Gi0/1 | 12.1.1.10 |
| Site-2 | Gi0/1 | 12.1.1.2 |
| Site-1 LAN | — | 10.1.1.0/24 |
| Site-2 LAN | — | 10.2.2.0/24 |

### 🔑 IKEv1 Phase 1

Configured IKEv1/ISAKMP for secure peer authentication and negotiation.

- IKE Version: IKEv1
- Exchange Mode: Main Mode
- Authentication: Pre-Shared Key
- ISAKMP Policy: Configured
- Encryption: Configured
- Hash: Configured
- Diffie-Hellman Group: Configured
- Lifetime: Configured

### 🔒 IPsec Phase 2

Configured IPsec to encrypt traffic between the Site-1 and Site-2 LAN networks.

- IPsec
- ESP
- Transform Set
- Crypto ACL
- Crypto Map
- Peer Address
- Encryption
- Authentication

### 🛡️ Interesting Traffic

Extended ACL is used to identify the traffic that should be encrypted by the VPN.

```text
Site-1 LAN  →  Site-2 LAN
10.1.1.0/24 → 10.2.2.0/24
