# Optimized Network Project

This repository contains the configuration for an optimized network setup using Cisco Packet Tracer.

## Network Configuration

The network is configured with the following components:

- **Access Switches (1-4)**: Configured with trunk mode for interfaces F0/1-2, access mode for interfaces F0/3-20 (VLAN 10, Voice VLAN 30) and F0/21-24 (VLAN 20). Spanning-tree portfast and bpduguard are enabled for these interfaces.

- **Distribution Switches (DSW-1 and DSW-2)**: Interface F0/7 is configured with trunk encapsulation dot1q and trunk mode.

- **Wireless LAN Controller (WLC) and Control PC**: Interface F0/9 on WLC and F0/10 on Control PC are configured with access mode and assigned to VLAN 20 and VLAN 10 respectively. Voice VLAN 30 is also configured on the Control PC. Spanning-tree portfast is enabled on these interfaces.

- **Core Router and ISP Router**: Configured with specific IP addresses on interfaces F0/1, F0/0, and F1/0 for the Core Router and g0/0/0, g0/0/1 for the ISP Router.

- **OSPF Configuration**: OSPF is configured on the Distribution switches, Core Router, ISP Core, and IBM Cloud Instance with specific router IDs and network areas.

- **HSRP & Inter-VLAN Routing**: Configured on VLANs 10, 20, and 30 with specific IP addresses, helper addresses, and standby priorities and IPs.

- **Voice VLAN**: Configured on interface fa1/1.30 with specific IP address and DHCP pool settings. Telephony service is also configured with maximum directory numbers (DNs) and IP phones, auto assignment, and specific source address.

Please refer to the configuration files for more details.

## Usage

To use this configuration, load it into your Cisco Packet Tracer and start the simulation.

## Contributing

Contributions are welcome. Please open an issue to discuss your ideas or submit a pull request with your changes.

## License

This project is free to use for conventional practices.

## Disclaimer

This project is for educational purposes only. Please use caution when implementing these configurations in a production environment.
