# CMPG325-2026-008 – Kopano Community Bank (Mahikeng)

## Milestone 1 – Client Design Review

**Module:** CMPG 325 – Computer Networks
**Project ID:** CMPG325-2026-008
**Client ID:** CLI-008
**Student:** CHABA, T
**Student Number:** 35808438
**Organisation:** Kopano Community Bank (Mahikeng)
**Industry:** Banking & Finance
**Milestone:** 1 – Client Design Review
**Milestone Date:** 28 August 2026

---

## 1. Project Overview

This project involves the design and simulation of a computer network for **Kopano Community Bank (Mahikeng)**.

The network will be developed and simulated using **Cisco Packet Tracer**. The design is based on the requirements provided in the CMPG 325 project brief.

The assigned IPv4 addressing block is:

**10.14.0.0/16**

The main networking challenge assigned to this project is:

**STP – Loop Prevention & Root Design**

The client also has a change request:

**CR8 – A shared printer zone must serve two departments that currently cannot print.**

The project must provide appropriate connectivity, support the required services, demonstrate STP, and allow for possible future network expansion.

---

## 2. Milestone 1 Objectives

The main objectives of Milestone 1 are to establish the initial network design before the detailed Packet Tracer implementation.

The Milestone 1 design focuses on:

* Documenting the client requirements.
* Designing the proposed physical topology.
* Designing the proposed logical topology.
* Developing an IP addressing plan using `10.14.0.0/16`.
* Planning VLAN segmentation.
* Designing the STP root-bridge approach.
* Including the CR8 shared printer zone.
* Considering future branch-office growth.
* Preparing the GitHub portfolio structure.

---

## 3. Client Requirements

The network design must satisfy the following requirements:

1. Provide appropriate connectivity and network services for the client.
2. Use the assigned `10.14.0.0/16` addressing block.
3. Produce a working and testable Cisco Packet Tracer implementation.
4. Configure the required routers, switches, end devices and other necessary nodes.
5. Demonstrate successful connectivity and testing.
6. Configure, verify and demonstrate STP for loop prevention and root design.
7. Allow the addressing plan to accommodate a possible branch office within 18 months.
8. Implement CR8 by providing a shared printer zone for two departments.
9. Capture evidence of successful configuration and operation.
10. Document important troubleshooting.
11. Maintain a professional GitHub portfolio with meaningful commits and project evidence.

---

## 4. Proposed Physical Topology

The proposed physical topology contains an edge router, two core/distribution switches, departmental access switches and a dedicated printer-zone switch.

### Proposed Devices

| Device     | Role                               | Purpose                                                |
| ---------- | ---------------------------------- | ------------------------------------------------------ |
| R1         | Edge Router                        | Connects the internal network to the external/WAN side |
| SW-CORE-01 | Primary Core/Distribution Switch   | Main core connectivity and preferred STP root          |
| SW-CORE-02 | Secondary Core/Distribution Switch | Provides a redundant core path                         |
| SW-ACC-A   | Department A Access Switch         | Connects Department A endpoints                        |
| SW-ACC-B   | Department B Access Switch         | Connects Department B endpoints                        |
| SW-PRN     | Printer-Zone Access Switch         | Connects the shared printer                            |
| PCs        | End Devices                        | Provide user access                                    |
| Printer    | Shared Resource                    | Provides printing services to both departments         |

### Proposed Physical Arrangement

```text
                         INTERNET / WAN
                              |
                              |
                             R1
                              |
                    ---------------------
                    |                   |
              SW-CORE-01 ========== SW-CORE-02
                    | \               / |
                    |  \             /  |
                    |   \           /   |
                 SW-ACC-A   SW-ACC-B   SW-PRN
                    |          |          |
                  PCs        PCs       Printer
```

The redundant switch paths are included specifically to support the STP challenge.

The final physical cabling and port assignments will be verified and updated during the Packet Tracer implementation.

---

## 5. STP Design

STP is the assigned networking challenge for this project.

The proposed design uses:

* **SW-CORE-01** as the primary STP root bridge.
* **SW-CORE-02** as the secondary/redundant core switch.
* Redundant physical links between switching devices.

The purpose of STP is to prevent Layer 2 switching loops while retaining physical redundancy.

The final Packet Tracer implementation must verify:

* The selected STP root bridge.
* STP port roles and states.
* Forwarding and blocking/discarding behaviour where applicable.
* That redundant paths do not create a Layer 2 loop.

---

## 6. Proposed Logical Topology

The network is logically divided into four VLANs.

| VLAN | Name                | Purpose                   | Subnet          | Gateway      |
| ---: | ------------------- | ------------------------- | --------------- | ------------ |
|   10 | Department A        | Department A users        | `10.14.10.0/24` | `10.14.10.1` |
|   20 | Department B        | Department B users        | `10.14.20.0/24` | `10.14.20.1` |
|   30 | Shared Printer Zone | Shared network printer    | `10.14.30.0/24` | `10.14.30.1` |
|   99 | Management          | Network-device management | `10.14.99.0/24` | `10.14.99.1` |

### VLAN 10 – Department A

Department A users will be placed into VLAN 10.

**Subnet:** `10.14.10.0/24`
**Gateway:** `10.14.10.1`

This provides a separate logical network for Department A endpoints.

### VLAN 20 – Department B

Department B users will be placed into VLAN 20.

**Subnet:** `10.14.20.0/24`
**Gateway:** `10.14.20.1`

This separates Department B from Department A at Layer 2.

### VLAN 30 – Shared Printer Zone

VLAN 30 is dedicated to the shared printer.

**Subnet:** `10.14.30.0/24`
**Gateway:** `10.14.30.1`

Both Department A and Department B should be able to reach the printer through the routed network.

This VLAN directly addresses **CR8**.

### VLAN 99 – Management

VLAN 99 is reserved for network-device management.

**Subnet:** `10.14.99.0/24`
**Gateway:** `10.14.99.1`

Management addresses can be assigned to the switches within this subnet.

---

## 7. IP Addressing Plan

The assigned address block is:

```text
10.14.0.0/16
```

For Milestone 1, selected `/24` networks are proposed for the current LAN.

### Current Allocation

| Network         | Purpose             | Gateway      |
| --------------- | ------------------- | ------------ |
| `10.14.10.0/24` | Department A        | `10.14.10.1` |
| `10.14.20.0/24` | Department B        | `10.14.20.1` |
| `10.14.30.0/24` | Shared Printer Zone | `10.14.30.1` |
| `10.14.99.0/24` | Management          | `10.14.99.1` |

### Example Host Addresses

| Device         | IP Address    | Subnet Mask     | Gateway      |
| -------------- | ------------- | --------------- | ------------ |
| PC-A1          | `10.14.10.10` | `255.255.255.0` | `10.14.10.1` |
| PC-A2          | `10.14.10.11` | `255.255.255.0` | `10.14.10.1` |
| PC-B1          | `10.14.20.10` | `255.255.255.0` | `10.14.20.1` |
| PC-B2          | `10.14.20.11` | `255.255.255.0` | `10.14.20.1` |
| Shared Printer | `10.14.30.10` | `255.255.255.0` | `10.14.30.1` |
| SW-CORE-01     | `10.14.99.10` | `255.255.255.0` | `10.14.99.1` |
| SW-CORE-02     | `10.14.99.11` | `255.255.255.0` | `10.14.99.1` |
| SW-ACC-A       | `10.14.99.12` | `255.255.255.0` | `10.14.99.1` |
| SW-ACC-B       | `10.14.99.13` | `255.255.255.0` | `10.14.99.1` |
| SW-PRN         | `10.14.99.14` | `255.255.255.0` | `10.14.99.1` |

**Note:** These host addresses are proposed examples for Milestone 1. They must be checked against the final Cisco Packet Tracer configuration.

---

## 8. CR8 – Shared Printer Zone

The client change request requires a shared printer zone that serves two departments that currently cannot print.

The proposed solution places the printer in:

```text
VLAN 30
10.14.30.0/24
```

The logical communication path is:

```text
Department A
10.14.10.0/24
       |
       v
   Layer 3 Gateway
       |
       v
Printer Zone
10.14.30.0/24
       ^
       |
   Layer 3 Gateway
       ^
       |
Department B
10.14.20.0/24
```

This design allows the printer to remain in a dedicated logical network while being accessible to both departments through inter-VLAN routing.

The final Packet Tracer implementation will be used to test this connectivity.

---

## 9. Future Branch-Office Planning

The client may open a branch office within 18 months.

Therefore, the entire `10.14.0.0/16` address block will not be consumed by the current LAN.

The current design uses only selected subnets, leaving additional address space available for:

* Future departments.
* Additional network devices.
* Additional services.
* Expansion of existing VLANs.
* A future branch office.

The topology documentation may illustrate `10.15.0.0/16` as a possible future branch network. This is only an illustrative planning choice and is **not an address assigned by the project brief**.

---

## 10. Milestone 1 Testing Plan

The detailed testing will take place during the Packet Tracer implementation.

The planned tests include:

* Testing connectivity from Department A to its gateway.
* Testing connectivity from Department B to its gateway.
* Testing Department A access to the shared printer.
* Testing Department B access to the shared printer.
* Testing management connectivity.
* Verifying VLAN configuration.
* Verifying IP addressing.
* Verifying inter-VLAN routing.
* Verifying the STP root bridge.
* Checking STP port states.
* Confirming that redundant paths do not create Layer 2 loops.

Screenshots and command output will be captured as evidence.

---

## 11. Proposed Repository Structure

```text
CMPG325-2026-008/
│
├── README.md
│
├── 01-Client-Requirements/
│
├── 02-Physical-Topology/
│
├── 03-Logical-Topology/
│
├── 04-IP-Addressing/
│
├── 05-Packet-Tracer/
│
├── 06-Configuration/
│
├── 07-Testing/
│
├── 08-Evidence/
│
└── 09-Troubleshooting/
```

For Milestone 1, the main focus is on:

```text
01-Client-Requirements/
02-Physical-Topology/
03-Logical-Topology/
04-IP-Addressing/
```

The remaining folders will contain evidence as the project progresses.

---

## 12. Milestone 1 Deliverables

The Milestone 1 design includes:

* Client requirements analysis.
* Proposed physical topology.
* Proposed logical topology.
* VLAN design.
* Initial IP addressing plan.
* STP root-design approach.
* CR8 shared printer-zone design.
* Future branch-office addressing consideration.
* Initial GitHub repository structure.

---

## 13. Milestone 1 Status

| Requirement                  | Status          |
| ---------------------------- | --------------- |
| Client requirements          | Completed       |
| Physical topology            | Proposed        |
| Logical topology             | Proposed        |
| IP addressing plan           | Proposed        |
| VLAN design                  | Proposed        |
| STP root design              | Proposed        |
| CR8 printer zone             | Included        |
| Future branch planning       | Included        |
| Packet Tracer implementation | To be completed |
| Connectivity testing         | To be completed |
| STP verification             | To be completed |
| Final evidence               | To be completed |

---

## 14. Conclusion

Milestone 1 establishes the proposed network design for Kopano Community Bank (Mahikeng).

The design uses the assigned `10.14.0.0/16` addressing block and separates the network into Department A, Department B, the shared printer zone and management VLANs.

Two core switches provide redundancy and allow the assigned STP challenge to be demonstrated. SW-CORE-01 is proposed as the primary STP root, while SW-CORE-02 provides a redundant path.

The dedicated VLAN 30 printer zone addresses CR8 by providing a shared network printer that can be reached by both departments through the routed network.

The addressing plan also preserves unused address space for future growth and a possible branch office within the required 18-month period.

The next stages of the project will involve implementing this design in Cisco Packet Tracer, configuring the network, testing connectivity, verifying STP behaviour and collecting evidence for the GitHub portfolio.

---

## 15. Academic and Scope Note

This README represents the **Milestone 1 design stage**. Detailed device configurations, exact Packet Tracer port assignments, final host addresses and testing results should only be recorded after they have been implemented and verified.

The student remains responsible for checking, understanding and verifying all submitted work in accordance with the CMPG 325 project requirements.
