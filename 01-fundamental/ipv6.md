## IPv6 Basics

### Overview

IPv6 (Internet Protocol version 6) is the successor to IPv4, designed to address the exhaustion of the 32-bit IPv4 address space. IPv6 uses 128-bit addresses, providing approximately 3.4 × 10³⁸ unique addresses.

### IPv6 Address Format

An IPv6 address consists of **eight groups of four hexadecimal digits**, separated by colons.

```
Full form:    2001:0DB8:0000:0000:0000:FF00:0042:8329
Compressed:   2001:DB8::FF00:42:8329
```

#### Compression Rules

1. **Leading zeros** within any group may be omitted.  
   `0042` → `42`

2. **Consecutive groups of all zeros** may be replaced by `::` — but only **once** per address.  
   `0000:0000:0000` → `::`

### IPv6 Address Types

| Type        | Prefix       | Description                                      |
|-------------|--------------|--------------------------------------------------|
| Global Unicast | `2000::/3` | Routable on the public internet (equivalent to public IPv4) |
| Link-Local  | `FE80::/10`  | Valid only within a single network link; automatically assigned |
| Loopback    | `::1/128`    | Equivalent to IPv4 `127.0.0.1`                  |
| Multicast   | `FF00::/8`   | Replaces IPv4 broadcast                          |
| Unique Local | `FC00::/7`  | Equivalent to IPv4 private address ranges        |

### Configuring IPv6 on a Cisco Router

```
! Enable IPv6 routing globally
Router(config)# ipv6 unicast-routing

! Configure an interface with a global unicast address
Router(config)# interface FastEthernet0/0
Router(config-if)# ipv6 address 2001:DB8:1::1/64
Router(config-if)# no shutdown
Router(config-if)# exit

! Configure an interface using EUI-64 (auto-generates host portion from MAC address)
Router(config)# interface FastEthernet1/0
Router(config-if)# ipv6 address 2001:DB8:2::/64 eui-64
Router(config-if)# no shutdown
Router(config-if)# exit
```

### Verification Commands

```
! Display all IPv6 interfaces
Router# show ipv6 interface brief

! Display the IPv6 routing table
Router# show ipv6 route

! Test IPv6 connectivity
Router# ping ipv6 2001:DB8:1::2

! Display neighbor discovery cache (equivalent to IPv4 ARP)
Router# show ipv6 neighbors
```

### IPv4 vs IPv6 Comparison

| Feature          | IPv4                  | IPv6                         |
|------------------|-----------------------|------------------------------|
| Address Length   | 32 bits               | 128 bits                     |
| Address Format   | Decimal (dotted)      | Hexadecimal (colon-separated) |
| Total Addresses  | ~4.3 billion          | ~3.4 × 10³⁸                  |
| Broadcast        | Supported             | Replaced by multicast        |
| ARP              | Used for MAC lookup   | Replaced by Neighbor Discovery Protocol (NDP) |
| Header Size      | 20–60 bytes (variable) | 40 bytes (fixed)            |
| Configuration    | Manual or DHCP        | Manual, DHCPv6, or SLAAC    |
| IPsec            | Optional              | Built-in support             |

### EUI-64 Address Generation

When using the `eui-64` flag, the router automatically generates the 64-bit interface identifier from its MAC address by:

1. Splitting the 48-bit MAC address in half
2. Inserting `FF:FE` in the middle
3. Flipping the 7th bit of the first byte (Universal/Local bit)

```
MAC Address:   00:1A:2B:3C:4D:5E
Split:         00:1A:2B | 3C:4D:5E
Insert FF:FE:  00:1A:2B:FF:FE:3C:4D:5E
Flip 7th bit:  02:1A:2B:FF:FE:3C:4D:5E
IPv6 IID:      021A:2BFF:FE3C:4D5E
```

---

## Files in This Module

| File                          | Description                                      |
|-------------------------------|--------------------------------------------------|
| `basic-router-config.pkt`     | Three-network topology with inter-LAN routing    |
| `basic-switch-config.pkt`     | Switch initial configuration and management IP   |
| `network-topologies.pkt`      | Comparison of bus, star, ring, and mesh topologies |
| `cabling-types.pkt`           | Straight-through, crossover, serial, and console demo |
| `subnetting-exercise.pkt`     | VLSM allocation practice across multiple subnets |
| `ipv6-basics.pkt`             | Global unicast and link-local IPv6 configuration |
| `verify-commands-cheatsheet.md` | Quick reference for all `show` and `ping` commands |
