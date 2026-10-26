# Design Decisions

- **VLAN segmentation:** IT, Finance, Data Servers, DMZ, and Management use separate VLANs/subnets.
- **Layer 2 / Layer 3 boundary:** SW-A/SW-B are L3 gateways. DC-SW-A/DC-SW-B are L2 switches; their core uplinks should be trunks, not routed /30 links.
- **VRRP:** provides gateway redundancy, not WAN/VPN failover.
- **ACL placement:** ACL rules only apply to traffic crossing the interface/direction where attached. First matching rule wins; place deny rules before broad permits.
- **IPsec:** tunnel establishment alone does not guarantee reachability. Protected subnets/traffic selectors, forward routes, and return routes must match.
- **Management:** restrict SSH/SNMP to authorized administrators and Zabbix sources.
- **Limitations:** this is a learning lab, not a production-ready design. Consider firewalls, AAA, secure credential storage, backups, NTP, logging, and regular failover testing for production.


## VRRP redundancy and traffic distribution
VRRP provides gateway redundancy. You can distribute normal traffic across SW-A and SW-B by making SW-A the preferred master for some VLANs and SW-B the preferred master for others. This is per-VLAN distribution, not per-flow load balancing within one VLAN. Verify the master/backup state for every VRRP group.
