# Lessons learned

Format: what broke, what I found, what I fixed. The honest version.

## FILL IN — template (copy for each incident)

### <What broke>
- **Symptom:**
- **What I checked first:**
- **Root cause:**
- **Fix:**
- **What I'd do differently:**

## Good candidates from this build
- The first RAID build and validation (scrub/verify before trusting it)
- Getting Jellyfin's container to see the storage and the network correctly
- The Tailscale subnet-router setup and NAS firewall rules per source subnet
- SMB permission errors between users, and how permissions actually resolve
