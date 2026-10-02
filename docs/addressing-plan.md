# Addressing Plan

Assigned block: **10.14.0.0/16**

## VLANs

| VLAN | Name | Subnet | Gateway (HSRP) | SW-CORE-01 | SW-CORE-02 |
|---|---|---|---|---|---|
| 10 | DEPT-A | 10.14.10.0/24 | 10.14.10.1 | .2 | .3 |
| 20 | DEPT-B | 10.14.20.0/24 | 10.14.20.1 | .2 | .3 |
| 30 | PRINTER-ZONE | 10.14.30.0/24 | 10.14.30.1 | .2 | .3 |
| 99 | MANAGEMENT | 10.14.99.0/24 | 10.14.99.1 | .10 | .11 |

## Point-to-point links

| Link | Subnet | Addresses |
|---|---|---|
| R1 Gi0/1 to SW-CORE-01 Fa0/4 | 10.14.0.0/30 | R1 .1, SW-CORE-01 .2 |
| R1 Gi0/0 to SW-CORE-02 Fa0/1 | 10.14.0.4/30 | R1 .5, SW-CORE-02 .6 |

## Hosts and management

| Device | Address | Gateway |
|---|---|---|
| PC-A-01 to PC-A-04 | 10.14.10.10 to .13 /24 | 10.14.10.1 |
| PC-B-01 to PC-B-04 | 10.14.20.10 to .13 /24 | 10.14.20.1 |
| Printer0 | 10.14.30.10 /24 | 10.14.30.1 |
| Printer1 | 10.14.30.11 /24 | 10.14.30.1 |
| SW-CORE-01 / SW-CORE-02 | 10.14.99.10 / .11 | 10.14.99.1 |
| SW-ACC-A / SW-ACC-B / SW-PRN | 10.14.99.12 / .13 / .14 | 10.14.99.1 |

## Physical connections

| From | To | Type |
|---|---|---|
| R1 Gi0/1 | SW-CORE-01 Fa0/4 | Routed |
| R1 Gi0/0 | SW-CORE-02 Fa0/1 | Routed |
| SW-CORE-01 Fa0/5 | SW-CORE-02 Fa0/2 | Trunk |
| SW-CORE-01 Fa0/1 | SW-ACC-A Fa0/7 | Trunk |
| SW-CORE-02 Fa0/3 | SW-ACC-A Fa0/6 | Trunk |
| SW-CORE-01 Fa0/3 | SW-ACC-B Fa0/1 | Trunk |
| SW-CORE-02 Fa0/5 | SW-ACC-B Fa0/6 | Trunk |
| SW-CORE-01 Fa0/2 | SW-PRN Fa0/1 | Trunk |
| SW-CORE-02 Fa0/4 | SW-PRN Fa0/3 | Trunk |

## Future branch office (18-month constraint)

| Item | Range |
|---|---|
| Reserved branch block | 10.14.128.0/17 |
| Branch VLAN 10 / 20 / 30 | 10.14.138.0/24, 10.14.148.0/24, 10.14.158.0/24 |
| Branch VLAN 99 | 10.14.227.0/24 |
| HQ to branch link | 10.14.0.8/30 |

The current site stays in 10.14.0.0/17, so each site can be summarised as one route.
