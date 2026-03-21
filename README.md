# DMZ-ACL_Network-Implementation

## Description
  This project demonstrates a small network simulated in Cisco Packet Tracer. It shows how to implement a DMZ and ACLs to protect both the internal LAN and DMZ servers. The lab also configures NAT and PAT so all internal hosts
and servers share a single public IP.

## Network Diagram
![Network Diagram](Diagram.png)

## Network Componets
| Component Type | Model                                      | Quantity |
|----------------|--------------------------------------------|----------|
| Switch         | Cisco 2960                                 | 3        |
| Router         | Cisco PT-Empty(1CGE/PT-ROUTER-NM-1S_ports) | 2        |
| PC             | Generic PC                                 | 5        |
| Server         | Cisco Server                               | 7        |

## IP Addressing Scheme
| Device            | Interface     | IP Address   | Subnet Mask       | Default Gateway | DNS          | NAT     |
|-------------------|---------------|--------------|-------------------|-----------------|--------------|---------|
| SW0               |               |              |                   |                 |              |         |
|   PC1-1           | F0/1          | DHCP         | 255.255.255.0     | 192.168.1.1     | 192.168.1.3  |         |
|   PC1-2           | F0/2          | DHCP         | 255.255.255.0     | 192.168.1.1     | 192.168.1.3  |         |
|   PC1-3           | F0/3          | DHCP         | 255.255.255.0     | 192.168.1.1     | 192.168.1.3  |         |
|   DHCP-Server     | F0/23         | 192.168.1.2  | 255.255.255.0     | 192.168.1.1     | 192.168.1.3  |         |
|   Private-DNS     | F0/24         | 192.168.1.3  | 255.255.255.0     | 192.168.1.1     |              |         |
| SW0               |               |              |                   |                 |              |         |
|   Public-DNS      | F0/1          | 192.168.2.10 | 255.255.255.0     | 192.168.2.1     |              |         |
|   Company-mail    | F0/2          | 192.168.2.20 | 255.255.255.0     | 192.168.2.1     | 192.168.2.10 |         |
|   Company-web     | F0/3          | 192.168.2.30 | 255.255.255.0     | 192.168.2.1     | 192.168.2.10 |         |
| SW0               |               |              |                   |                 |              |         |
|   PC2-1           | F0/1          | DHCP         | 255.255.255.0     | 10.10.10.1      | 192.168.2.10 |         |
|   PC2-2           | F0/2          | DHCP         | 255.255.255.0     | 10.10.10.1      | 192.168.2.10 |         |
|   DHCP_LAN-2      | F0/23         | 10.10.10.2   | 255.255.255.0     | 10.10.10.1      | 192.168.2.10 |         |
|   Web_LAN-2       | F0/24         | 10.10.10.3   | 255.255.255.0     | 10.10.10.1      | 192.168.2.10 |         |
| DMZ_Router        | G0/0          | 192.168.1.1  | 255.255.255.0     |                 |              | Inside  |
| DMZ_Router        | G1/0          | 192.168.2.1  | 255.255.255.0     |                 |              | Inside  |
| DMZ_Router        | S9/0          | 10.20.30.252 | 255.255.255.0     |                 |              | Outside |
| LAN-2_Router      | S9/0          | 10.20.30.94  | 255.255.255.0     |                 |              |         |
| LAN-2_Router      | G0/0          | 10.10.10.1   | 255.255.255.0     |                 |              |         |
