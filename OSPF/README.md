# OSPF Router ID Selection and Neighbor Formation

## 📘 Project Overview
This lab demonstrates how **OSPF (Open Shortest Path First)** routers select their **Router ID** and form neighbor adjacencies across multiple areas.  
The focus is on understanding how OSPF chooses the Router ID based on **loopback or interface IPs**, and how this choice affects **neighbor relationships, LSDB exchanges, and routing table updates**.

---

## 🖥️ Topology
- **Routers:** R1, R2, R3, R4  
- **Areas:**
  - **Area 0 (Backbone):** R1, R2, R4  
  - **Area 1:** R2, R3  
- **Networks:**
  - 192.168.12.0/24  
  - 192.168.14.0/24  
  - 192.168.23.0/24  
  - 192.168.42.0/24  

---

## ⚙️ Configuration Highlights
- Each router is configured with **loopback interfaces** to represent stable Router IDs.
- OSPF automatically selects the **highest loopback IP** as the Router ID.
- If no loopback exists, OSPF uses the **highest active physical interface IP**.
- Once Router IDs are established, routers exchange **Hello packets** to form adjacencies.
- After adjacency, routers share **Link State Advertisements (LSAs)** to build the **Link State Database (LSDB)**.
- The LSDB is used to compute the **shortest path tree**, populating the routing table dynamically.

---

## 🔄 Process Flow
1. **Router ID Selection** → Highest loopback or interface IP chosen.  
2. **OSPF Hello Exchange** → Routers introduce themselves using Router IDs.  
3. **LSDB Synchronization** → Neighbors share link states and topology info.  
4. **Routing Table Update** → Optimal paths calculated and installed.

---

## 🧩 Key Learning Points
- Loopback interfaces ensure **stable Router IDs** even if physical links fail.  
- Consistent Router IDs simplify **troubleshooting and topology mapping**.  
- OSPF dynamically adapts to network changes through **LSA flooding** and **SPF recalculation**.  
- Understanding Router ID logic is crucial for **multi-area OSPF design** and **inter-area route propagation**.

---

## 📂 Repository Contents
- `configs/` → Router configuration files (R1–R4).  
- `captures/` → Wireshark packet captures showing OSPF Hello and LSDB exchanges.  
- `topology.png` → Network diagram of the OSPF setup.  
- `ospf_routerid_diagram.png` → Visual flow of Router ID selection and neighbor formation.  
- `README.md` → Documentation (this file).

---

## 🚀 Future Enhancements
- Implement **OSPF authentication** for secure neighbor formation.  
- Compare **Router ID behavior** in OSPF vs EIGRP.  
- Automate OSPF configuration using **Ansible or Python scripts**.

---

## ✍️ Author
**ANUGRAHA** – Final-year Engineering Student | Networking & Security Enthusiast | Aspiring Digital Forensics Analyst  

