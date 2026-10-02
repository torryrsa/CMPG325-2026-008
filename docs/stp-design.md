# STP Design (Loop Prevention and Root Design)

## Why STP is needed

Every access switch has an uplink to both core switches, and the cores are linked to each other. This gives redundancy but also creates Layer 2 loops that would cause broadcast storms. STP builds a loop-free logical topology while keeping the redundant links available.

## Design

| Item | Choice |
|---|---|
| Protocol | Rapid-PVST+ (`spanning-tree mode rapid-pvst`) |
| Primary root | SW-CORE-01, priority 4096 for VLANs 10, 20, 30, 99 |
| Secondary root | SW-CORE-02, priority 8192 |
| Access switches | Default priority 32768 (never root) |
| Host ports | PortFast and BPDU Guard |
| Trunks | Native VLAN 99, allowed VLANs 10, 20, 30, 99 |

## Expected result

| Switch | VLAN | Forwarding uplink | Blocked uplink |
|---|---|---|---|
| SW-ACC-A | 10 | Fa0/7 to SW-CORE-01 | Fa0/6 to SW-CORE-02 |
| SW-ACC-B | 20 | Fa0/1 to SW-CORE-01 | Fa0/6 to SW-CORE-02 |
| SW-PRN | 30 | Fa0/1 to SW-CORE-01 | Fa0/3 to SW-CORE-02 |

## Verification commands

```
show spanning-tree vlan 10
show spanning-tree summary
show interfaces trunk
```

## Failover test

1. Run `ping -t 10.14.30.10` from a Department A PC.
2. On SW-CORE-01: `interface fastEthernet0/1`, `shutdown`.
3. On SW-ACC-A: `show spanning-tree vlan 10` shows Fa0/6 take over as the root port.
4. On SW-CORE-01: `no shutdown` and confirm STP returns to the original state.

Screenshots are in the `screenshots/` folder.
