---
created:
  "{ date }":
ip:
vlan:
type:
url:
notes:
cpu:
memory:
tags:
  - infra
---

# {{title}}

## Purpose


## Hardware

| | |
|---|---|
| CPU | |
| Memory | |

## IPAM

| IP | VLAN | Type | URL |
|---|---|---|---|
| `= this.ip` | `= this.vlan` | `= this.type` | `= this.url` |

See [[04. IPAM]] for the full registry.

For most infra, `ip` is a single value (one management IP) even if `vlan` lists several trunked VLANs. If a device holds a separate address in every VLAN (e.g. the router acting as gateway), make `ip` a list matching `vlan` position-for-position — e.g. `vlan: [LAN, Servers]` + `ip: [192.168.1.1, 10.30.0.1]`.

## Services



## Configuration notes


## Changelog

### DD-MM-YYYY
-
