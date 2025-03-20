Some tricks here.

1. Create A-S group.
2. create VS, create http profile with preserv client ip.
3. have the SE, vs and pool memebers on the same T1.
4. disable urpf mode on the data-segment.
5. create a pool with a securitygroup where the webserver is in.


*TODO automation*
show nsxt segment se-datasegment
+--------------------+--------------------------------------+
| Field              | Value                                |
+--------------------+--------------------------------------+
| uuid               | segmentruntime-8475e13f7a40          |
| segment_id         | /infra/segments/se-datasegment       |
| name               | se-datasegment                       |
| subnet             | 192.168.34.0/24                      |
| dhcp_enabled       | True                                 |
| nw_ref             | se-datasegment                       |
| nw_name            | se-datasegment                       |
| vrf_context_ref    | sfo-w01-mgmt                         |
| tier1_id           | /infra/tier-1s/sfo-w01-mgmt          |
| opaque_network_id  | 47124de0-2488-4a13-b91d-de2bbde63cf2 |
| segment_gw         | 192.168.34.1/24                      |
| dhcp_ranges[1]     | 192.168.34.10-192.168.34.100         |
| segname            | se-datasegment                       |
| tenant_ref         | admin                                |
| cloud_ref          | sfo-w01-nsx01                        |
| security_only_nsxt | False                                |
+--------------------+--------------------------------------+

show networkservice preserve-ip
+--------------------------------+-----------------------------------------------------+
| Field                          | Value                                               |
+--------------------------------+-----------------------------------------------------+
| uuid                           | networkservice-43918503-89a1-4e7b-a24b-0eec6cf4aa45 |
| name                           | preserve-ip                                         |
| se_group_ref                   | active-standby                                      |
| vrf_ref                        | sfo-w01-mgmt                                        |
| service_type                   | ROUTING_SERVICE                                     |
| routing_service                |                                                     |
|   enable_routing               | False                                               |
|   routing_by_linux_ipstack     | False                                               |
|   floating_intf_ip[1]          | 192.168.34.101                                      |
|   enable_vmac                  | False                                               |
|   enable_vip_on_all_interfaces | True                                                |
|   advertise_backend_networks   | False                                               |
|   graceful_restart             | False                                               |
|   enable_auto_gateway          | False                                               |
| tenant_ref                     | admin                                               |
| cloud_ref                      | sfo-w01-nsx01                                       |
+--------------------------------+-----------------------------------------------------+
