# Lessons learned

Format: what broke, what I found, what I fixed. The honest version.

## Incident 1 — Jellyfin library paths and deleted files

### What broke
Jellyfin's library drifted from reality: entries pointed at files that no
longer existed after I reorganized folders on the NAS, and other media
services picked up the same mess — wrong paths, dead entries, playback
errors for the family.

### Symptom
Media missing from libraries, items that wouldn't play, duplicate or stale
entries after moving files around the Multimedia share.

### What I checked first
The library folders in Jellyfin — comparing what the scanner saw against
what was actually on disk.

### Root cause
The library path structure and the on-disk folder structure had diverged:
I had moved/renamed/deleted files on the NAS without Jellyfin's library
layout being reorganized to match. The scanner was holding on to old paths
and catching half of the changes.

### Fix
Re-aligned the library paths with the real folder structure on the NAS,
cleaned out the dead entries, and let the scanner rebuild against the
correct structure. Then established the rule: media folder structure changes
happen once, deliberately, followed by a full re-scan — not piecemeal.

### What I'd do differently
Design the folder layout once, up front, before pointing any media service
at it — reorganizing after three different apps have indexed it costs three
times the cleanup.

## Incident 2 — Remote access from another house

### What broke
Accessing the NAS and media services remotely from my partner's house
didn't work — the services were reachable on the home LAN but not from
another network.

### Symptom
Connections failed or hung from the remote location; everything worked
fine at home.

### What I checked first
Whether the router was exposing anything — and deliberately did NOT go the
port-forwarding route. Exposing NAS services to the internet is how these
boxes get owned; I wanted remote access without opening inbound ports.

### Root cause
The devices at the remote location weren't on the mesh network, and the
connection path between the two networks wasn't established — the NAS was
only reachable from inside its own LAN.

### Fix
Installed the mesh-VPN client (Tailscale) on the NAS and on the devices at
the remote location, connecting both networks to the same tailnet. With the
NAS as a node (and subnet routing available), the media services became
reachable from the remote location over encrypted WireGuard tunnels —
zero inbound ports opened on the router, nothing exposed to the internet.

### What I'd do differently
Set up the mesh VPN from day one, before any service existed — retrofitting
remote access after the stack is running means re-testing every service
through the new path.
