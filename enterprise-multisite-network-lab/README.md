# Multi-Site Enterprise Network Lab (GNS3)

A GNS3 learning project covering VLAN segmentation, inter-VLAN routing, VRRP gateway redundancy, extended ACLs, site-to-site IPsec VPNs, and centralized Zabbix monitoring.

## Topology
- **HQ / Site A:** VLAN 10 (IT), VLAN 20 (Finance); SW-A and SW-B provide Layer 3 routing and VRRP.
- **Data Center / Site B:** VLAN 70 (Data Servers), VLAN 80 (DMZ/Application), VLAN 90 (Management/Zabbix). DC-SW-A and DC-SW-B are Layer 2 switches; VLAN gateways remain on SW-A/SW-B.
- **Branch A:** VLAN 10 IT (`10.1.10.0/26`), VLAN 20 Finance (`10.1.20.0/26`).
- **Branch B:** VLAN 10 IT (`10.2.10.0/26`), VLAN 20 Finance (`10.2.20.0/26`).
- IPsec VPN tunnels provide encrypted inter-site connectivity. Dual-path failover must be verified separately.

## HQ / Data Center addressing (confirm against final configs)
| VLAN | Purpose | Subnet | Gateway |
|---:|---|---|---|
| 10 | IT | `192.168.10.0/26` | `192.168.10.1` |
| 20 | Finance | `192.168.20.0/26` | `192.168.20.1` |
| 70 | Data Servers | `192.168.70.0/26` | `192.168.70.1` |
| 80 | DMZ/Application | `192.168.80.0/26` | `192.168.80.1` |
| 90 | Management/Zabbix | `192.168.90.0/26` | `192.168.90.1` |

## Design logic
1. VLANs separate user, server, DMZ, and management traffic.
2. SW-A/SW-B route between VLANs; DC switches use Layer 2 trunks/access ports.
3. VRRP provides a virtual default gateway and gateway failover. Different preferred masters across VLANs can distribute traffic across SW-A/SW-B; this is per-VLAN traffic distribution, not per-flow load balancing within one VLAN.
4. ACLs enforce least privilege. The implemented policy includes blocking Finance access to VLAN 70 and VLAN 90, plus restrictions between user VLANs and the DMZ.
5. IPsec encrypts inter-site traffic; routes and security ACLs are still required.
6. Zabbix provides centralized device/service monitoring.

## Security policy goals
- Finance (VLAN 20) → Data Servers (VLAN 70): deny.
- Finance (VLAN 20) → Management/Zabbix (VLAN 90): deny.
- IT → central servers/applications: permit only required services.
- DMZ → internal networks: deny by default, with documented exceptions.
- SSH to network devices: allow only from authorized management hosts.

ACLs are stateless. For production-like segmentation, use explicit service permits and consider a stateful firewall at the DMZ boundary.

## Verification commands
```text
show ip interface brief
show vlan brief
show interfaces trunk
show spanning-tree
show vrrp brief
show access-lists
show ip route
show crypto isakmp sa
show crypto ikev2 sa
show crypto ipsec sa
```
Use the VPN command matching the configured IKE version and platform.

## Validation checklist
- [ ] VLANs, SVI addresses, and masks match the addressing plan.
- [ ] VRRP master/backup states are correct.
- [ ] DC trunks carry only required VLANs.
- [ ] Finance cannot reach VLAN 70 or VLAN 90.
- [ ] Approved branch-to-application traffic works over IPsec.
- [ ] Unauthorized SSH is blocked.
- [ ] IPsec counters increase during test traffic.
- [ ] Primary-path failure moves traffic to backup, if configured.
- [ ] Zabbix monitors HQ, DC, and branch devices.
- [ ] GNS3 project saves and reopens correctly.

## Before publishing
Replace example values with verified values from your final configuration. Remove passwords, pre-shared keys, real credentials, and personal information. Do not upload vendor appliance images unless redistribution is permitted.

The actual GNS3 project file is not included in this documentation package. Add your saved `.gns3` project and required project files after verifying that it opens correctly.
