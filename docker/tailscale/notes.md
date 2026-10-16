# Tailscale mesh VPN notes

- The NAS and my daily devices are nodes on the same tailnet; the NAS also
  advertises subnet routes so the whole home LAN is reachable from remote.
- Remote access (e.g. from my partner's house) rides the mesh — no inbound
  ports opened on the router, nothing exposed to the internet.
- NAS firewall rules: management ports allowed only from the LAN and
  Tailscale subnets; everything else dropped.
- Why this beats port-forwarding: no public attack surface, and the
  connection is encrypted end-to-end by WireGuard regardless of network.
