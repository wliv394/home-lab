# Jellyfin notes

- Runs in Docker on the NAS so the media server stays isolated from the
  storage layer — a bad update can be rolled back by rebuilding the
  container, never by touching the array.
- The library reads the Multimedia share read-only, so nothing a viewer
  does in Jellyfin can write to the storage pool.
- Transcoding: hardware-accelerated via the N100's integrated graphics
  (Intel Quick Sync), mapped into the container through /dev/dri — no
  discrete GPU needed, and transcodes run cool.
- Config lives in a mapped folder on the NAS, so container rebuilds keep
  libraries and watch history.
