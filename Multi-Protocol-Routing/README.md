# Multi‑Protocol Routing Lab: OSPF, EIGRP, and BGP Integration

## 📌 Overview
This repository documents the configuration and verification of a complex network topology integrating **OSPF**, **EIGRP**, and **BGP** routing domains. The project demonstrates how Autonomous System Boundary Routers (ASBRs) can be used to redistribute routes across heterogeneous protocols, ensuring end‑to‑end connectivity.

## 🔹 Topology Summary
- **EIGRP AS 100** → Routers R3, R5, R7
- **OSPF ASN 100 (PID 10)** → Routers R1, R2, R4, R6
- **OSPF ASN 200 (PID 20)** → Routers R8, R9
- **BGP AS 200** → Peering between R1 and R8

### ASBR Roles
- **R3** → Redistributes between OSPF and EIGRP
- **R1** → Redistributes between OSPF and BGP

## 🔹 Key Configurations
- **OSPF ↔ EIGRP Redistribution (R3)**
  ```bash
  router ospf 10
   redistribute eigrp 100 subnets

  router eigrp 100
   redistribute ospf 10 metric 10000 10 255 1 1500

  **OSPF ↔ BGP Redistribution (R1)**
  router bgp 200
 neighbor 192.168.18.8 remote-as 200
 redistribute ospf 10 match internal external 1 external 2

 Default Route Injection (R1)
 ip route 0.0.0.0 0.0.0.0 <next-hop>
router ospf 10
 default-information originate


🔹 Verification
Routing Tables

show ip route → Confirm EIGRP routes appear as OSPF E2 in ASN 200
show ip bgp → Confirm OSPF external routes are redistributed into BGP

Connectivity Tests
ping and traceroute from R7 → R9 successful via R1 → R8
End‑to‑end reachability established across all domains


🔹 Learning Outcomes
Importance of Administrative Distance (AD) in route selection:

EIGRP internal = 90
OSPF (internal/external) = 110
EIGRP external = 170

Careful redistribution design is critical to avoid routing loops and ensure stability.
Route‑maps and prefix‑lists provide granular control over which prefixes are exchanged.

🚀 Conclusion
This lab demonstrates advanced redistribution strategies across EIGRP, OSPF, and BGP, highlighting how ASBRs enable interoperability between different routing domains. It serves as a practical reference for network engineers preparing for CCNP/CCIE or working on multi‑protocol enterprise networks.
