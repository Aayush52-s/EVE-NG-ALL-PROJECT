🔐 Site-to-Site IPsec VPN — Without NAT-T

A policy-based Site-to-Site IPsec VPN lab built using Cisco IOS and EVE-NG, demonstrating secure communication between two remote LANs through an ISP network without NAT-T.

---

📌 Project Overview

This project demonstrates the complete configuration, operation, and verification of a Site-to-Site IPsec VPN between two remote sites.

The VPN uses IKEv1, ISAKMP, pre-shared key authentication, IPsec, ESP, Extended ACLs, and Crypto Maps to securely transport traffic between private networks.

"VPN Topology" (images/vpn-topology.png)

---

🎯 Project Objectives

- Configure Site-to-Site IPsec VPN
- Configure IKEv1 Phase 1
- Configure ISAKMP policy
- Configure pre-shared key authentication
- Configure IPsec Phase 2
- Configure ESP encryption
- Configure Extended ACL for interesting traffic
- Configure Crypto Map
- Apply Crypto Map to the WAN interface
- Establish secure communication between two sites
- Verify IKE and IPsec Security Associations
- Analyze encrypted traffic using Wireshark
- Demonstrate IPsec VPN without NAT-T

---

🏗️ Network Topology

The topology consists of two remote sites connected through an ISP network.

"Network Topology" (images/vpn-topology.png)

Topology Components

Component| Role
🏢 Site-1 Router| VPN Endpoint
🏢 Site-2 Router| VPN Endpoint
🌐 ISP Router| WAN Connectivity
💻 Site-1 LAN| Private Network
💻 Site-2 LAN| Private Network

Traffic Flow

Site-1 LAN
     │
     ▼
Site-1 Router
     │
     │  🔐 IPsec VPN
     ▼
ISP Network
     │
     │  🔐 IPsec VPN
     ▼
Site-2 Router
     │
     ▼
Site-2 LAN

---

🛠️ Technologies Used

"Cisco" (https://img.shields.io/badge/Cisco-IOS-blue)
"EVE-NG" (https://img.shields.io/badge/EVE--NG-Lab-red)
"IPsec" (https://img.shields.io/badge/IPsec-VPN-green)
"IKEv1" (https://img.shields.io/badge/IKEv1-ISAKMP-orange)
"Wireshark" (https://img.shields.io/badge/Wireshark-Analysis-blue)
"ESP" (https://img.shields.io/badge/ESP-Encryption-purple)

Technologies & Concepts

- Cisco IOS
- EVE-NG
- IKEv1
- ISAKMP
- IPsec
- ESP
- AES Encryption
- SHA Integrity
- Diffie-Hellman
- Pre-Shared Key
- Extended ACL
- Crypto Map
- Security Associations
- Wireshark
- Site-to-Site VPN
- NAT-T vs Non-NAT-T

---

🔑 IKEv1 Phase 1

IKE Phase 1 establishes a secure management channel between the two VPN peers.

IKE Parameters

Parameter| Configuration
Encryption| AES
Hash| SHA
Authentication| Pre-Shared Key
Diffie-Hellman| Group 14
Lifetime| 86400 seconds

Configuration

crypto isakmp policy 10
 encryption aes
 hash sha
 authentication pre-share
 group 14
 lifetime 86400

Pre-Shared Key

crypto isakmp key VPN-KEY address <REMOTE-VPN-PEER-IP>

---

🤝 IKE Negotiation

The following screenshot shows the IKE negotiation and Phase 1 establishment.

"IKE Negotiation" (images/ike-negotiation.png)

Verification Command

show crypto isakmp sa

Expected state:

QM_IDLE

"QM_IDLE" indicates that the IKEv1 Security Association has been successfully established.

---

🔐 IPsec Phase 2

IPsec Phase 2 establishes the Security Associations used to protect actual user traffic.

Transform Set

crypto ipsec transform-set VPN-TRANSFORM esp-aes esp-sha-hmac
 mode tunnel

IPsec Provides

- 🔒 Confidentiality
- 🛡️ Integrity
- 🔑 Authentication
- 🔐 Secure communication

---

🎯 Interesting Traffic

An Extended ACL identifies the traffic that should be protected by IPsec.

Example

ip access-list extended VPN-TRAFFIC
 permit ip 10.1.1.0 0.0.0.255 10.2.2.0 0.0.0.255

Traffic Definition

Source Network      : 10.1.1.0/24
Destination Network : 10.2.2.0/24

Only traffic matching this ACL is considered interesting traffic for the VPN.

---

🗺️ Crypto Map

The Crypto Map connects the VPN peer, transform set, and interesting traffic ACL.

Interesting Traffic
        │
        ├── Remote VPN Peer
        │
        ├── IPsec Transform Set
        │
        ▼
    Crypto Map

Configuration

crypto map SITE-TO-SITE 10 ipsec-isakmp
 set peer <REMOTE-VPN-PEER-IP>
 set transform-set VPN-TRANSFORM
 match address VPN-TRAFFIC

Apply Crypto Map

interface GigabitEthernet0/0
 crypto map SITE-TO-SITE

---

🔒 ESP Encryption

ESP protects the actual user data traveling through the VPN tunnel.

"ESP Encryption" (images/esp-encryption.png)

Packet Flow

Original IP Packet
        │
        ▼
   ESP Header
        │
        ▼
Encrypted Payload
        │
        ▼
ESP Integrity Data

The ISP can forward the encrypted packet but cannot read the protected payload.

---

🔄 VPN Packet Flow

When a host from Site-1 communicates with a host at Site-2:

1. Site-1 Host
       ↓
2. Site-1 Router
       ↓
3. Interesting Traffic ACL
       ↓
4. IKE Phase 1
       ↓
5. IPsec Phase 2
       ↓
6. ESP Encryption
       ↓
7. ISP Network
       ↓
8. Site-2 Router
       ↓
9. ESP Decryption
       ↓
10. Site-2 Host

---

🚫 IPsec Without NAT-T

🔐 Site-to-Site IPsec VPN — Without NAT-T

A policy-based Site-to-Site IPsec VPN lab built using Cisco IOS and EVE-NG, demonstrating secure communication between two remote LANs through an ISP network without NAT-T.

---

📌 Project Overview

This project demonstrates the complete configuration, operation, and verification of a Site-to-Site IPsec VPN between two remote sites.

The VPN uses IKEv1, ISAKMP, pre-shared key authentication, IPsec, ESP, Extended ACLs, and Crypto Maps to securely transport traffic between private networks.

"VPN Topology" (images/vpn-topology.png)

---

🎯 Project Objectives

- Configure Site-to-Site IPsec VPN
- Configure IKEv1 Phase 1
- Configure ISAKMP policy
- Configure pre-shared key authentication
- Configure IPsec Phase 2
- Configure ESP encryption
- Configure Extended ACL for interesting traffic
- Configure Crypto Map
- Apply Crypto Map to the WAN interface
- Establish secure communication between two sites
- Verify IKE and IPsec Security Associations
- Analyze encrypted traffic using Wireshark
- Demonstrate IPsec VPN without NAT-T

---

🏗️ Network Topology

The topology consists of two remote sites connected through an ISP network.

"Network Topology" (images/vpn-topology.png)

Topology Components

Component| Role
🏢 Site-1 Router| VPN Endpoint
🏢 Site-2 Router| VPN Endpoint
🌐 ISP Router| WAN Connectivity
💻 Site-1 LAN| Private Network
💻 Site-2 LAN| Private Network

Traffic Flow

Site-1 LAN
     │
     ▼
Site-1 Router
     │
     │  🔐 IPsec VPN
     ▼
ISP Network
     │
     │  🔐 IPsec VPN
     ▼
Site-2 Router
     │
     ▼
Site-2 LAN

---

🛠️ Technologies Used

"Cisco" (https://img.shields.io/badge/Cisco-IOS-blue)
"EVE-NG" (https://img.shields.io/badge/EVE--NG-Lab-red)
"IPsec" (https://img.shields.io/badge/IPsec-VPN-green)
"IKEv1" (https://img.shields.io/badge/IKEv1-ISAKMP-orange)
"Wireshark" (https://img.shields.io/badge/Wireshark-Analysis-blue)
"ESP" (https://img.shields.io/badge/ESP-Encryption-purple)

Technologies & Concepts

- Cisco IOS
- EVE-NG
- IKEv1
- ISAKMP
- IPsec
- ESP
- AES Encryption
- SHA Integrity
- Diffie-Hellman
- Pre-Shared Key
- Extended ACL
- Crypto Map
- Security Associations
- Wireshark
- Site-to-Site VPN
- NAT-T vs Non-NAT-T

---

🔑 IKEv1 Phase 1

IKE Phase 1 establishes a secure management channel between the two VPN peers.

IKE Parameters

Parameter| Configuration
Encryption| AES
Hash| SHA
Authentication| Pre-Shared Key
Diffie-Hellman| Group 14
Lifetime| 86400 seconds

Configuration

crypto isakmp policy 10
 encryption aes
 hash sha
 authentication pre-share
 group 14
 lifetime 86400

Pre-Shared Key

crypto isakmp key VPN-KEY address <REMOTE-VPN-PEER-IP>

---

🤝 IKE Negotiation

The following screenshot shows the IKE negotiation and Phase 1 establishment.

"IKE Negotiation" (images/ike-negotiation.png)

Verification Command

show crypto isakmp sa

Expected state:

QM_IDLE

"QM_IDLE" indicates that the IKEv1 Security Association has been successfully established.

---

🔐 IPsec Phase 2

IPsec Phase 2 establishes the Security Associations used to protect actual user traffic.

Transform Set

crypto ipsec transform-set VPN-TRANSFORM esp-aes esp-sha-hmac
 mode tunnel

IPsec Provides

- 🔒 Confidentiality
- 🛡️ Integrity
- 🔑 Authentication
- 🔐 Secure communication

---

🎯 Interesting Traffic

An Extended ACL identifies the traffic that should be protected by IPsec.

Example

ip access-list extended VPN-TRAFFIC
 permit ip 10.1.1.0 0.0.0.255 10.2.2.0 0.0.0.255

Traffic Definition

Source Network      : 10.1.1.0/24
Destination Network : 10.2.2.0/24

Only traffic matching this ACL is considered interesting traffic for the VPN.

---

🗺️ Crypto Map

The Crypto Map connects the VPN peer, transform set, and interesting traffic ACL.

Interesting Traffic
        │
        ├── Remote VPN Peer
        │
        ├── IPsec Transform Set
        │
        ▼
    Crypto Map

Configuration

crypto map SITE-TO-SITE 10 ipsec-isakmp
 set peer <REMOTE-VPN-PEER-IP>
 set transform-set VPN-TRANSFORM
 match address VPN-TRAFFIC

Apply Crypto Map

interface GigabitEthernet0/0
 crypto map SITE-TO-SITE

---

🔒 ESP Encryption

ESP protects the actual user data traveling through the VPN tunnel.

"ESP Encryption" (images/esp-encryption.png)

Packet Flow

Original IP Packet
        │
        ▼
   ESP Header
        │
        ▼
Encrypted Payload
        │
        ▼
ESP Integrity Data

The ISP can forward the encrypted packet but cannot read the protected payload.

---

🔄 VPN Packet Flow

When a host from Site-1 communicates with a host at Site-2:

1. Site-1 Host
       ↓
2. Site-1 Router
       ↓
3. Interesting Traffic ACL
       ↓
4. IKE Phase 1
       ↓
5. IPsec Phase 2
       ↓
6. ESP Encryption
       ↓
7. ISP Network
       ↓
8. Site-2 Router
       ↓
9. ESP Decryption
       ↓
10. Site-2 Host

---

🚫 IPsec Without NAT-T

This project demonstrates Site-to-Site IPsec without NAT-T.

There is no NAT device between the two VPN endpoints.

Site-1 Router
      │
      │ No NAT
      ▼
 ISP Network
      │
      │ No NAT
      ▼
Site-2 Router

Native IPsec

IP
 │
 ▼
ESP
 │
 ▼
IP

When NAT exists between VPN peers, NAT-T can encapsulate ESP inside UDP/4500.

IP
 │
 ▼
UDP/4500
 │
 ▼
ESP
 │
 ▼
IP

---

🦈 Wireshark Verification

Wireshark is used to verify that traffic is being encrypted using ESP.

"VPN Verification" (images/vpn-verification.png)

Wireshark Filter

esp

You can also filter by the VPN peer:

ip.addr == <VPN-PEER-IP>

Expected Result

ESP packets should be visible between the two VPN endpoints.

The original application payload should not be visible to the ISP.

---

🧪 VPN Verification

Verify IKE Phase 1

show crypto isakmp sa

Verify IPsec Phase 2

show crypto ipsec sa

Check these counters:

#pkts encaps
#pkts encrypt
#pkts decaps
#pkts decrypt

The counters should increase when traffic passes through the VPN.

Verify Crypto Map

show crypto map

Verify Interesting Traffic ACL

show access-lists VPN-TRAFFIC

Verify Routing

show ip route

Verify Interfaces

show ip interface brief

---

📊 Verification Results

Verification| Expected Result
Site-1 → Site-2 Ping| ✅ Successful
IKEv1 Phase 1| ✅ Established
IPsec Phase 2| ✅ Established
ESP Packets| ✅ Visible
Encryption Counters| ✅ Increasing
Decryption Counters| ✅ Increasing
NAT-T| ❌ Not Required
VPN Communication| ✅ Operational

---

🛠️ Troubleshooting

If the VPN does not establish, verify the following:

Basic Connectivity

ping <REMOTE-VPN-PEER-IP>

IKE

show crypto isakmp sa

IPsec

show crypto ipsec sa

Crypto Map

show crypto map

ACL

show access-lists VPN-TRAFFIC

Routing

show ip route

Common Issues

- Incorrect VPN peer IP
- Incorrect pre-shared key
- IKE Phase 1 mismatch
- IPsec transform-set mismatch
- Incorrect interesting traffic ACL
- Crypto Map not applied to WAN interface
- Missing route
- Incorrect LAN/WAN addressing
- Unwanted NAT configuration

---

📸 Project Evidence

Network Topology

"VPN Topology" (images/vpn-topology.png)

IKE Negotiation

"IKE Negotiation" (images/ike-negotiation.png)

ESP Encryption

"ESP Encryption" (images/esp-encryption.png)

VPN Verification

"VPN Verification" (images/vpn-verification.png)

---

📁 Project Structure

SITE-TO-SITE-WITHOUT-NAT-T/
│
├── README.md
├── s2s-without-NAT-config.txt
│
└── images/
    ├── vpn-topology.png
    ├── ike-negotiation.png
    ├── esp-encryption.png
    └── vpn-verification.png

---

🧠 Key Concepts Demonstrated

Cisco IOS
EVE-NG
Site-to-Site VPN
IKEv1
ISAKMP
IPsec
ESP
AES Encryption
SHA Integrity
Diffie-Hellman
Pre-Shared Key
Extended ACL
Interesting Traffic
Crypto Map
Security Associations
Wireshark
NAT-T

---

🏁 Conclusion

This project demonstrates the configuration and verification of a policy-based Site-to-Site IPsec VPN without NAT-T.

The implementation covers the complete VPN process:

IKEv1 Phase 1
      ↓
ISAKMP
      ↓
Pre-Shared Key Authentication
      ↓
IPsec Phase 2
      ↓
ESP Encryption
      ↓
Interesting Traffic ACL
      ↓
Crypto Map
      ↓
Secure Site-to-Site Communication

The VPN was verified using Cisco IOS commands and Wireshark packet analysis.

---

👨‍💻 Author

Aayush Sojitra

Network Engineer | Network Security Engineer

Core Skills:
"Networking" • "Cisco IOS" • "IPsec VPN" • "IKEv1" • "ESP" • "ACL" • "Wireshark" • "EVE-NG"This project demonstrates Site-to-Site IPsec without NAT-T.

There is no NAT device between the two VPN endpoints.

Site-1 Router
      │
      │ No NAT
      ▼
 ISP Network
      │
      │ No NAT
      ▼
Site-2 Router

Native IPsec

IP
 │
 ▼
ESP
 │
 ▼
IP

When NAT exists between VPN peers, NAT-T can encapsulate ESP inside UDP/4500.

IP
 │
 ▼
UDP/4500
 │
 ▼
ESP
 │
 ▼
IP

---

🦈 Wireshark Verification

Wireshark is used to verify that traffic is being encrypted using ESP.

"VPN Verification" (images/vpn-verification.png)

Wireshark Filter

esp

You can also filter by the VPN peer:

ip.addr == <VPN-PEER-IP>

Expected Result

ESP packets should be visible between the two VPN endpoints.

The original application payload should not be visible to the ISP.

---

🧪 VPN Verification

Verify IKE Phase 1

show crypto isakmp sa

Verify IPsec Phase 2

show crypto ipsec sa

Check these counters:

#pkts encaps
#pkts encrypt
#pkts decaps
#pkts decrypt

The counters should increase when traffic passes through the VPN.

Verify Crypto Map

show crypto map

Verify Interesting Traffic ACL

show access-lists VPN-TRAFFIC

Verify Routing

show ip route

Verify Interfaces

show ip interface brief

---

📊 Verification Results

Verification| Expected Result
Site-1 → Site-2 Ping| ✅ Successful
IKEv1 Phase 1| ✅ Established
IPsec Phase 2| ✅ Established
ESP Packets| ✅ Visible
Encryption Counters| ✅ Increasing
Decryption Counters| ✅ Increasing
NAT-T| ❌ Not Required
VPN Communication| ✅ Operational

---

🛠️ Troubleshooting

If the VPN does not establish, verify the following:

Basic Connectivity

ping <REMOTE-VPN-PEER-IP>

IKE

show crypto isakmp sa

IPsec

show crypto ipsec sa

Crypto Map

show crypto map

ACL

Aayush Sojitra

Network Engineer | Network Security Engineer

Core Skills:
"Networking" • "Cisco IOS" • "IPsec VPN" • "IKEv1" • "ESP" • "ACL" • "Wireshark" • "EVE-NG"
