# PC Café Baseline Security Assessment

## Purpose
This assessment documents the current PC Café network before security controls are implemented.

## Network Segments
- Guest Network
- Reception VLAN 10
- Sales VLAN 20
- Back Office Network

## Baseline Connectivity Tests

| Source | Destination | Result |
|---|---|---|
| Guest PC 192.168.0.2 | Guest Gateway 192.168.0.1 | PASS |
| Guest PC 192.168.0.2 | Reception PC 192.168.0.34 | PASS |
| Guest PC 192.168.0.2 | Sales PC 192.168.0.66 | PASS |
| Guest PC 192.168.0.2 | Back Office PC 192.168.0.97 | PASS |
| Reception PC 192.168.0.34 | Sales PC 192.168.0.66 | PASS |
| Reception PC 192.168.0.34 | Back Office PC 192.168.0.97 | PASS |
| Sales PC 192.168.0.66 | Back Office PC 192.168.0.97 | PASS |
| Reception PC | Reception Printer 192.168.0.35 | PASS |
| Internal PC | Back Office Printer 192.168.0.98 | PASS |

## Security Weaknesses Identified
1. Guest devices can communicate with internal business networks.
2. Guest devices can reach the Back Office network.
3. Reception and Sales can communicate without restrictions.
4. Sales can communicate with the Back Office network.
5. Internal printers can be reached from other network segments.
6. Network segmentation exists, but traffic between segments is not sufficiently restricted.

## Recommended Improvements
- Implement ACLs between network segments.
- Restrict Guest access to internal networks.
- Protect the Back Office network from unnecessary access.
- Configure secure management using SSH.
- Implement switch port security.
- Disable unused switch ports where appropriate.
- Test the network again after security controls are implemented.

## Baseline Conclusion
The network is operational and all tested devices can communicate. However, the current configuration allows more communication between network segments than is necessary. Security controls should be added to restrict unauthorized access while keeping required network services available.