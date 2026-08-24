# Static Routing with Failover – Multi-Router Topology

## 📌 Project Overview
This lab demonstrates **static routing configuration** across a 4-router topology (R1, R2, R3, R4) with a switch and end device (PC1).  
The goal is to ensure **redundant connectivity**: when the primary path goes down, traffic automatically shifts to an alternate path using administrative distance (AD) and route tracking.

---

## 🖥️ Topology
- **Routers:** R1, R2, R3, R4  
- **Switch:** Switch1  
- **PC:** PC1  
- **Subnets:**
  - R1 ↔ R2 → `192.168.40.0/30`
  - R1 ↔ R3 → `192.168.40.4/30`
  - R3 ↔ R4 → `192.168.40.8/30`
  - R2 ↔ R4 → `192.168.40.12/30`
  - R4 ↔ Switch1 ↔ PC1 → `192.168.1.0/24`

---

## ⚙️ Configuration Highlights
- **Static Routes:**  
  - Primary path configured with **lower AD (10)**.  
  - Backup path configured with **higher AD (20)**.  
- **Failover Behavior:**  
  - If the primary interface or next-hop fails, traffic is rerouted via the alternate path.  
  - This ensures continuous connectivity between PC1 and R1/R2/R3/R4.

---

## 🔄 Failover Demonstration
1. **Normal Operation:**  
   - PC1 pings R1 via the primary path (through R3).  
   - R1 reaches PC1 via primary path (through R2).  

2. **Failure Simulation:**  
   - When the primary interface (e.g., `f0/0`) is shut down, traffic drops initially.  
   - Router detects the failure and installs the **alternate static route**.  
   - Connectivity is restored via the backup path.

---

## 🧩 Key Learning Points
- Static routing with AD provides **basic redundancy**.  
- Without dynamic protocols (OSPF/EIGRP), failover depends on **interface state**.  
- For advanced failover (detecting downstream failures), use **IP SLA + Track**.  

---

## 📂 Repository Contents  
- `captures/` → Wireshark packet captures showing DHCP DORA and ARP checks.  
- `topology.png` → Network diagram of the setup.  
- `README.md` → Documentation (this file).

---

## 🚀 Future Enhancements
- Implement **IP SLA tracking** for smarter failover.  
- Compare static routing failover with **OSPF/EIGRP dynamic routing**.  
- Automate configuration deployment using **Ansible/Netmiko**.

---

## ✍️ Author
**ANUGRAHA** – Final-year Engineering Student, passionate about Networking, Security, and Digital Forensics.  

