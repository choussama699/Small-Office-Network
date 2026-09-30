# Small-Office-Network

A secured small-office network built in Cisco Packet Tracer. It combines VLANs, inter-VLAN routing, static routing, DHCP, a wireless guest network, EtherChannel, port security, SSH, and ACL-based guest isolation.


Features
VLAN segmentation for Administration, IT, Sales and Guest users
Inter-VLAN routing on Router0
Static routing with a default route toward the DSL modem (internet)
DHCP server on the router for all VLANs
Guest Wi-Fi through an access point in VLAN 40
EtherChannel (3 physical links) between SW1 and Switch1 on Fa0/6-8
Port security on Fa0/1-3 of both switches
SSH for secure remote management of SW1
ACL that blocks the Guest VLAN from all internal VLANs while still allowing internet access


Network Design
VLAN	Name	        Subnet        	Gateway	      Devices	Switch
10	Administration	192.168.10.0/24	192.168.10.1	PC0	SW1
20	IT	            192.168.20.0/24	192.168.20.1	PC1	SW1
30	Sales	          192.168.30.0/24	192.168.30.1	Laptop1	SW1
40	Guest         	192.168.40.0/24	192.168.40.1	Laptop0, Laptop2 (via Guest Wi-Fi AP)	Switch1


LAN 1: VLANs 10, 20, 30 on SW1
LAN 2: VLAN 40 on Switch1




Security Policy
Source	          Destination        	Result
VLAN 10 / 20 / 30	Each other	        Allowed
VLAN 10 / 20 / 30	Internet  	        Allowed
VLAN 40 (Guest)	  VLAN 10 / 20 / 30	  Blocked (ACL)
VLAN 40 (Guest)	  Internet	          Allowed


Verification : 



show vlan brief
show interfaces trunk
show etherchannel summary
show port-security
show ip dhcp binding              ! on Router0
show ip route                     ! on Router0
show access-lists                 ! on Router0
