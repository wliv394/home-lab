# Pi-hole notes

- Runs in Docker on the NAS in **host network mode**. DNS has to answer on
  port 53 of the host's LAN address; host mode keeps that simple and keeps
  real client IPs visible in the query log (bridge mode with port mapping
  hides them behind the Docker gateway).
- **Port 53 conflict, solved first.** UGOS Pro ships its own dnsmasq already
  listening on 53. Pi-hole cannot bind while it runs, so I stopped and
  disabled the NAS's dnsmasq, freed the port, then started Pi-hole. This is
  the classic "why won't Pi-hole start" problem on a NAS — the fix is to
  find the existing resolver, not to change Pi-hole's port.
- **Upstream: Quad9 (9.9.9.9 / 149.112.112.112).** Malware-blocking,
  privacy-respecting, no logging tie to an ad company.
- **Blocking used for telemetry, not just ads.** Six domains are set as
  regex deny rules: the NAS vendor's phone-home and cloud-relay domains plus
  a third-party crash reporter. Enforcing at DNS means the whole house is
  covered from one place — no per-device configuration, no host-file edits,
  and nothing to re-apply after an app update.
- **The NAS itself resolves through Pi-hole.** Its `/etc/resolv.conf` and the
  UGOS `dnsmasq-resolv.conf` were both pointed at Pi-hole, so the NAS's own
  outbound lookups are filtered the same as every other device.
- **Verification method:** `nslookup` the blocked domains — they return
  `0.0.0.0`, meaning the query is answered locally and never leaves the
  network. Then `nslookup` a normal domain (e.g. `docker.io`) to confirm real
  resolution still works. One command proves the block, the other proves you
  didn't break DNS.
- **Bind-mount ownership gotcha.** Gravity (the blocklist database) failed to
  write on first run because the mapped folders were root-owned. Fixed by
  `chown`-ing `/etc/pihole` and `/etc/dnsmasq.d` to the container's user.
- **Failure mode is designed for.** The router hands out the NAS as DNS, so
  if Pi-hole is down the house loses DNS with it. Documented recovery: set
  the router's DNS back to "get automatically from ISP" — one setting, sixty
  seconds, internet back. Worth knowing before you need it.
- **Firmware updates can revert this.** A UGOS update may rewrite
  `resolv.conf`, quietly sending NAS lookups back to the vendor. Re-check
  after every OS update — the block is only as good as the resolver config.

