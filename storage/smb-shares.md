# SMB shares and permissions

## The service

- SMB is enabled in Control Panel > File Services, standard Windows
  workgroup, LAN access with local NAS accounts.
- Clients: Windows machines on the LAN map the share directly; media
  clients (Jellyfin) read from the same storage through the container.

## Share layout

One main share, organized as a media library:

- Multimedia/ — audiobooks, books, concerts, hip-hop videos, movies,
  music, music videos, photos, TV shows, general video
- plus a private personal folder (redacted here by design — shares
  should never leak personal context into a public repo)

## Access model

<FILL IN — answer these and I'll finish this section:>
- How many NAS accounts, and what roles? (e.g. one admin account for
  management, separate daily-use account for media)
- Who can write vs. read? (e.g. admin read-write everywhere, media
  account read-only on Multimedia, write access only to its own folder)
- Does the media server account have its own restricted credentials?

## What I learned about permissions

<FILL IN — any surprise? e.g. "a user could see a share they weren't
given write access to", "permissions only took effect after re-mounting",
"hidden share vs. permission difference">
