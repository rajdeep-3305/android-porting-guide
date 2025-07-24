# ⚠️ GSI Quirks & Gotchas

- Some GSIs don’t mount `/odm` or `/vendor` on certain dynamic devices
- PHH GSI bootloops with AOSP init if AVB/dynamic mismatch
- `overlay.d` may be skipped entirely if fstab doesn't mount `/vendor` properly
- `ro.hardware.*` changes not reflected in `getprop` unless in early init
