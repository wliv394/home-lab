# SMB shares and permissions

## The service

- SMB enabled in Control Panel > File Services, standard Windows workgroup,
  LAN access with local NAS accounts.
- Clients: Windows machines on the LAN map the share directly; media servers
  (Jellyfin, Audiobookshelf, Navidrome) read from the same storage.

## Share layout

One main media share organized as a media library:

- Multimedia/ — audiobooks, books, concerts, hip-hop videos, movies, music,
  music videos, photos, TV shows, general video
- plus a private personal folder (redacted by design — a public repo should
  never leak personal context)

## Access model

- One NAS admin account: full read-write on all shares, used for management,
  Docker, and the media services.
- Media apps run against the library through the NAS, each serving its own
  user accounts at the application layer:
  - Jellyfin — family profiles (one per household member)
  - Audiobookshelf — shared listening for me and my partner
  - Navidrome — music streaming, clients connect through it
  - a TV-streaming app — separate viewer accounts for family members
- The pattern: storage-level access stays with the admin account, while
  per-person access control happens at the application layer. One write
  path, many read paths, no per-user NAS accounts to maintain.

## What I learned about permissions

- Keeping write access to a single account simplifies everything: no ACL
  surprises between users, no accidental deletes by viewers, and the media
  apps only ever read.
- Application-layer users (Jellyfin profiles, etc.) can be granted/revoked
  instantly without touching storage permissions.
