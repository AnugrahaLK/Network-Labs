# Test Plan

| ID | Test | Expected result | Evidence |
|---|---|---|---|
| T01 | IT and Finance IP/gateway | Correct address and gateway | TODO |
| T02 | `show vrrp brief` on SW-A/SW-B | Expected master/backup per VLAN | TODO |
| T03 | DC trunk validation | Required VLANs allowed and active | TODO |
| T04 | Finance to VLAN 70 | Blocked | TODO |
| T05 | Finance to VLAN 90/Zabbix | Blocked | TODO |
| T06 | IT to approved application | Allowed on required ports only | TODO |
| T07 | Branch to approved central application | Works over IPsec | TODO |
| T08 | IPsec counters | Encapsulation/decapsulation increase | TODO |
| T09 | Unauthorized SSH | Blocked | TODO |
| T10 | VPN primary-path failure | Backup takes over if configured | TODO |
| T11 | Zabbix monitoring | Devices report availability/metrics | TODO |
| T12 | Save and reopen GNS3 project | No missing-node issues | TODO |

Capture topology, `show vrrp brief`, `show interfaces trunk`, `show access-lists`, `show crypto ipsec sa`, and Zabbix status as evidence.
