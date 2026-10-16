# Home Lab — NAS + Docker Media Server + Mesh VPN

A self-hosted home lab built and administered end-to-end by me: NAS storage,
Docker services, media server, remote access over a mesh VPN, and network
segmentation with firewall rules.

This repo is my build log — it documents what I built, how it's configured,
and what I learned, as I work toward CompTIA Network+ and Cisco CCNA.

![Network topology](docs/topology.png)

## The stack at a glance

| Layer | What runs there |
|---|---|
| Storage | UGREEN NASync NAS, RAID array on enterprise-grade HDDs, SMB shares with per-user permissions |
| Services | Docker containers: Jellyfin (media server), live-TV streaming stack |
| Networking | LAN + Tailscale subnet interfaces, firewall rules restricting management ports by source subnet |
| Remote access | Tailscale mesh VPN — services reachable remotely without opening inbound ports |

## Why I built it this way

**RAID for resilience.** Two large enterprise drives in a mirrored array —
any single drive failure costs zero data and zero downtime. [FILL IN: your
actual RAID level and why you chose it — e.g. RAID 1 for a two-bay setup.]

**Docker for isolation.** Every service runs in its own container with pinned
versions. I can rebuild a container from scratch in minutes without touching
the host or the storage layer.

**Tailscale for access.** Instead of exposing NAS services to the internet
(port-forwarding is how NAS boxes get owned), every connection rides an
encrypted WireGuard mesh. My NAS firewall rules only allow management ports
from the LAN and Tailscale subnets — everything else gets dropped.

**SMB with least-privilege shares.** [FILL IN: how you split user accounts and
permissions — e.g. separate admin/user accounts, media read-only vs. docs
read-write.]

## What I learned building this

- Storage RAID rebuilds and the trade-offs between RAID levels
- Docker networking: container ports vs. host ports, and why a container
  listening on 0.0.0.0 is visible to every subnet unless firewalled
- Firewall rules per interface/source-subnet on the NAS itself
- WireGuard fundamentals: how a mesh VPN differs from a traditional
  site-to-site VPN, and why no open inbound ports beats port-forwarding
- [FILL IN: one or two specific problems you hit and fixed — the best part
  of a portfolio. Example: "Jellyfin container couldn't reach the tuner on
  the LAN — the Docker bridge was isolating it; fixed by X."]

## Where this is going

I'm studying for **CompTIA Network+**, then **Cisco CCNA**, and expanding the
lab toward: VLAN segmentation, a dedicated router/firewall, 10GbE backbone,
and hands-on Cisco switch/router configuration. This grant-funded next build
is detailed in [docs/next-steps.md](docs/next-steps.md).

## Repo contents

- `docs/` — topology diagram, lessons learned, planned upgrades
- `docker/` — compose files and notes for each container
- `storage/` — RAID setup and SMB share configuration notes
