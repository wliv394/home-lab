# Planned build — funded by the Meter Networking Grant

This is the next phase of the lab, and the line-item budget I proposed to the
Meter Network Engineering Grant Program.

## The upgrade path

| Layer | Today | Next phase |
|---|---|---|
| NAS | Compact two-bay NAS | Four-bay Pro unit with 10GbE networking |
| Memory | Stock RAM | Doubled DDR5 RAM for Docker workloads and VMs |
| Disk | Existing array | Enterprise HDD pair + NVMe cache pool |
| Network | Single flat LAN | Segmented LAN, 10GbE backbone |

## Line-item budget

- UGREEN NASync four-bay Pro NAS server (home-lab core) — $799.99
- Sixteen-gigabyte DDR5 SODIMM RAM upgrade — $128.99
- Two eighteen-terabyte enterprise HDDs, recertified WD Ultrastar — $559.98
- Two two-terabyte NVMe SSDs, Crucial P3 Plus, for cache and Docker — $393.98
- Patch cables, labels, rack accessories — $40.00

**Total: $1,922.95**

## What this unlocks

- A faster CPU and more RAM: more Docker containers, and a path to virtualization
- NVMe pool: container/cache storage off the HDD array
- 10GbE: the NAS becomes a real network node, not just an appliance
- The next study targets (Network+ and CCNA) get a physical network to practice on

This document doubles as the grant budget — every item above is the actual
purchase plan, prices verified in October of this year.
