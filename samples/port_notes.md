# 🛠️ Port Notes – Redmi Note 8 Pro

- Used TD-S AOSP 15 GSI (bvN)
- Booted after patching boot.img for permissive & dm-verity
- Patched `/system/etc/audio_policy.conf` to fix audio routing
- `camera.mtk.so` missing — likely ABI mismatch
- IMS registration skipped — workaround using persist props
