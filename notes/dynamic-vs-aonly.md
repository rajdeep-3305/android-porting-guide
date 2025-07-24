# 📦 A/B vs A-only Differences

- A/B (dynamic partitions):
  - boot, dtbo, vbmeta are critical
  - most have recovery inside boot.img

- A-only:
  - /recovery is separate
  - easier to flash but harder to patch sepolicy

Always check `getprop ro.boot.slot_suffix` and `ls /dev/block/by-name/`
