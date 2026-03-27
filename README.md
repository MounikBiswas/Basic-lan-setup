# Basic LAN Setup using Cisco Packet Tracer

## Objective

This project demonstrates the configuration of a basic Local Area Network (LAN) using Cisco Packet Tracer. The setup includes connecting multiple end devices (PCs) across two different subnets and routing traffic between them using a Cisco router.

---

## Network Topology

> 📸 *(Insert a screenshot of your Cisco Packet Tracer topology here)*

**Devices Used:**

- 1x Cisco Router (2911)
- 2x Cisco Switches (2960)
- 4x PCs (PC0, PC1, PC2, PC3)

**Topology Type:** Star topology per subnet, connected via a central router (Inter-VLAN style routing)

---

## IP Addressing Table

The network is divided into two distinct subnets. Below is the static IP configuration applied to all devices:

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **Router** | GigabitEthernet0/0 | 192.168.1.1 | 255.255.255.0 | N/A |
| **Router** | GigabitEthernet0/1 | 192.168.2.1 | 255.255.255.0 | N/A |
| **PC0** | FastEthernet0 | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| **PC1** | FastEthernet0 | 192.168.1.11 | 255.255.255.0 | 192.168.1.1 |
| **PC2** | FastEthernet0 | 192.168.2.10 | 255.255.255.0 | 192.168.2.1 |
| **PC3** | FastEthernet0 | 192.168.2.11 | 255.255.255.0 | 192.168.2.1 |

---

## Router Configuration

Below is the Cisco IOS CLI configuration used to assign IP addresses and bring router interfaces online:

```text
! Enter Privileged EXEC mode
Router> enable

! Enter Global Configuration mode
Router# configure terminal

! Configure the first interface (Gateway for PC0 and PC1 - Subnet 1)
Router(config)# interface g0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

! Configure the second interface (Gateway for PC2 and PC3 - Subnet 2)
Router(config)# interface g0/1
Router(config-if)# ip address 192.168.2.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

! Save configuration
Router# write memory
```

---

## Switch Configuration

No advanced configuration is required on the switches for this basic setup. Both switches operate at **Layer 2** using default settings, forwarding frames based on MAC addresses within their respective subnets.

- **Switch 1** connects PC0 and PC1 → Router interface G0/0
- **Switch 2** connects PC2 and PC3 → Router interface G0/1

---

## Verification & Testing

After completing the configuration, the following `ping` tests were performed to verify connectivity:

| Test | Source | Destination | Result |
| :--- | :--- | :--- | :--- |
| Same subnet | PC0 (192.168.1.10) | PC1 (192.168.1.11) | ✅ Success |
| Same subnet | PC2 (192.168.2.10) | PC3 (192.168.2.11) | ✅ Success |
| Inter-subnet | PC0 (192.168.1.10) | PC2 (192.168.2.10) | ✅ Success |
| Inter-subnet | PC1 (192.168.1.11) | PC3 (192.168.2.11) | ✅ Success |

> All pings returned **0% packet loss**, confirming that the router is correctly routing traffic between the two subnets.

---

## How to Run / Reproduce

1. Download and install **Cisco Packet Tracer** (free via [Cisco NetAcad](https://www.netacad.com/))
2. Open the `.pkt` file included in this repository
3. Click on each device to verify IP configurations
4. Use **PC Command Prompt** → type `ping <destination IP>` to test connectivity
5. Optionally, switch to **Simulation Mode** to observe ICMP packet flow step-by-step

---

## Conclusion

This project successfully demonstrated the setup of a basic LAN with two subnets using Cisco Packet Tracer. Key concepts applied include:

- **Static IP addressing** across two /24 subnets
- **Default gateway** configuration on end devices
- **Router interface configuration** using Cisco IOS CLI (`ip address`, `no shutdown`)
- **Inter-subnet routing** — the router acts as the bridge between 192.168.1.0/24 and 192.168.2.0/24
- **Layer 2 switching** — switches forward frames within the same subnet without any manual configuration

This forms the foundational understanding required for more advanced topics like VLANs, dynamic routing (RIP/OSPF), and DHCP configuration.

---

## References

- Cisco Networking Academy – *Introduction to Networks (ITN)* — [netacad.com](https://www.netacad.com)
- Cisco IOS Command Reference — [cisco.com](https://www.cisco.com/c/en/us/support/ios-nx-os-software/ios-15-4m-t/products-command-reference-list.html)
- GeeksforGeeks – *Computer Networks* — [geeksforgeeks.org](https://www.geeksforgeeks.org/computer-network-tutorials/)
