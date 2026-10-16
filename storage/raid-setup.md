# RAID setup notes

- Drives: 2x 8TB HDD (~7.2TB usable each)
- Array: RAID 1 (mirror)
- Why RAID 1: with two bays, mirroring is the right trade-off — any single
  drive failure costs zero data and zero downtime. Redundancy matters more
  than raw capacity for a homelab that other people's data lives on too.
- Build: array created in the NAS storage manager; both drives assigned to
  one storage pool.
- How I validated it:
  - Storage manager shows both drives status Normal
  - Drive temps 47-48°C at idle/load — within normal range
  - SMART test plans configured on both drives:
    - Rapid SMART test: once a week
    - Full SMART test: once a month
- Monitoring: scheduled SMART tests run automatically; next check alert
  is on my list to confirm notifications are enabled.

## Screenshots
- Storage pool view
- Array health / SMART test plans
(sanitized before upload — no serials)
