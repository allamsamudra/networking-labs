## Subnetting Exercise

### Overview

Subnetting is the process of dividing a larger IP network into smaller, more manageable subnetworks. It improves security, reduces broadcast traffic, and enables efficient IP address utilization.

### Key Terms

| Term            | Description |
|-----------------|-------------|
| Network Address | First address in a subnet — identifies the subnet itself |
| Broadcast Address | Last address in a subnet — used to address all hosts in the subnet |
| Usable Host Range | All addresses between network and broadcast address |
| Subnet Mask     | 32-bit value that distinguishes the network portion from the host portion |
| CIDR Notation   | Shorthand notation (e.g., /24) representing the number of network bits |

### CIDR Quick Reference

| CIDR | Subnet Mask       | Usable Hosts |
|------|-------------------|--------------|
| /24  | 255.255.255.0     | 254          |
| /25  | 255.255.255.128   | 126          |
| /26  | 255.255.255.192   | 62           |
| /27  | 255.255.255.224   | 30           |
| /28  | 255.255.255.240   | 14           |
| /29  | 255.255.255.248   | 6            |
| /30  | 255.255.255.252   | 2            |

### Exercise — Based on Lab Topology

The network used in this lab (`192.168.1.0/24`, `192.168.2.0/24`, `192.168.3.0/24`) uses classful /24 subnets. Below is the subnet breakdown for each:

#### Network 1 — 192.168.1.0/24

| Property          | Value               |
|-------------------|---------------------|
| Network Address   | 192.168.1.0         |
| Subnet Mask       | 255.255.255.0       |
| First Usable Host | 192.168.1.1 (Router Fa0/0) |
| Last Usable Host  | 192.168.1.254       |
| Broadcast Address | 192.168.1.255       |
| Total Usable Hosts | 254                |

#### Network 2 — 192.168.2.0/24

| Property          | Value               |
|-------------------|---------------------|
| Network Address   | 192.168.2.0         |
| Subnet Mask       | 255.255.255.0       |
| First Usable Host | 192.168.2.1 (Router Fa1/0) |
| Last Usable Host  | 192.168.2.254       |
| Broadcast Address | 192.168.2.255       |
| Total Usable Hosts | 254                |

#### Network 3 — 192.168.3.0/24

| Property          | Value               |
|-------------------|---------------------|
| Network Address   | 192.168.3.0         |
| Subnet Mask       | 255.255.255.0       |
| First Usable Host | 192.168.3.1 (Router Fa2/0) |
| Last Usable Host  | 192.168.3.254       |
| Broadcast Address | 192.168.3.255       |
| Total Usable Hosts | 254                |

### Advanced Exercise — VLSM (Variable Length Subnet Masking)

Suppose you are given the block `192.168.10.0/24` and need to allocate subnets for the following departments:

| Department | Required Hosts |
|------------|----------------|
| Engineering | 50            |
| Marketing   | 25            |
| Management  | 10            |
| WAN Link    | 2             |

VLSM allocation (largest subnet first):

| Subnet | Network Address     | Mask | Usable Hosts | Assigned To  |
|--------|---------------------|------|--------------|--------------|
| 1      | 192.168.10.0/26     | /26  | 62           | Engineering  |
| 2      | 192.168.10.64/27    | /27  | 30           | Marketing    |
| 3      | 192.168.10.96/28    | /28  | 14           | Management   |
| 4      | 192.168.10.112/30   | /30  | 2            | WAN Link     |

### Subnetting Formula

```
Number of subnets  = 2^n  (n = number of borrowed bits)
Usable hosts       = 2^h - 2  (h = number of remaining host bits)
Subnet increment   = 256 - (last octet of subnet mask)
```
