## Cabling Types

### Overview

Selecting the correct cable type is critical in physical network design. In Cisco Packet Tracer, cable selection determines whether a connection is established successfully between devices.

### Cable Types

#### Straight-Through Cable

Used to connect **devices of different types** (e.g., PC to switch, router to switch).

| From Device | To Device |
|-------------|-----------|
| PC          | Switch    |
| Router      | Switch    |
| Router      | Hub       |

```
Wiring standard:
  Pin 1 (TX+) ──────── Pin 1 (RX+)
  Pin 2 (TX-) ──────── Pin 2 (RX-)
  Pin 3 (RX+) ──────── Pin 3 (TX+)
  Pin 6 (RX-) ──────── Pin 6 (TX-)
```

#### Crossover Cable

Used to connect **devices of the same type** (e.g., PC to PC, switch to switch, router to router).

| From Device | To Device |
|-------------|-----------|
| PC          | PC        |
| Switch      | Switch    |
| Router      | Router    |
| Hub         | Hub       |

```
Wiring standard:
  Pin 1 (TX+) ──────── Pin 3 (RX+)
  Pin 2 (TX-) ──────── Pin 6 (RX-)
  Pin 3 (RX+) ──────── Pin 1 (TX+)
  Pin 6 (RX-) ──────── Pin 2 (TX-)
```

#### Serial/DCE Cable

Used for **WAN connections** between routers. The DCE (Data Communications Equipment) side must be configured with a clock rate.

```
Router-A (DCE) ──────────── Router-B (DTE)
  Serial0/0/0                 Serial0/0/0
  clock rate 64000
```

Configuration on the DCE side:
```
Router(config)# interface Serial0/0/0
Router(config-if)# clock rate 64000
Router(config-if)# ip address 10.0.0.1 255.255.255.252
Router(config-if)# no shutdown
```

#### Rollover (Console) Cable

Used to access a device's **CLI through the console port**. Connects a PC's RS-232 port to the router/switch console port. In Packet Tracer, this is represented as a light blue cable.

### Quick Reference Table

| Cable Type     | Color in PT | Use Case                              |
|----------------|-------------|---------------------------------------|
| Straight-Through | Black      | PC ↔ Switch, Router ↔ Switch          |
| Crossover       | Black       | PC ↔ PC, Switch ↔ Switch              |
| Serial (DCE)    | Red         | Router ↔ Router (WAN)                 |
| Rollover        | Light Blue  | PC ↔ Router/Switch (Console Access)   |

> **Note:** Modern switches and NICs support **Auto-MDIX**, which automatically detects and corrects cable type mismatches. However, in Cisco Packet Tracer simulations, cable selection must still be accurate for connections to function correctly.
