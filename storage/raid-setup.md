# RAID setup notes

- Drives: 2x 8TB HDD
- Array: RAID 1 (mirror)
- Why RAID 1: with two bays, mirroring is the right trade-off — any single
  drive failure costs zero data and zero downtime. Capacity is 8TB usable,
  which is plenty for media and documents, and the redundancy matters more
  than raw space.
- Build/scrub time observed: <FILL IN if you remember — e.g. "took a few hours">
- How I validated it: <FILL IN — e.g. "storage pool shows healthy, SMART
  checks pass on both drives, scrub/rebuild completed">
- Monitoring: <FILL IN — does the NAS email/notify you on drive issues?
  If you haven't set alerts yet, say "next up: SMART alerting" — honest plans
  read better than claimed habits>

## Screenshots
- Storage pool view
- Array health / SMART details
(sanitized before upload — no serials)
