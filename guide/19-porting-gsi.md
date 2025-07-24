# 🌐 Porting and Fixing Generic System Images (GSI)

GSIs (Generic System Images) are AOSP-based system images designed to boot on any Project Treble-compliant Android device.  
While they work out-of-the-box on some phones, others need **fixes, patches, or hacks** to make them usable.

This guide shows how to patch, flash, and fix GSIs for real-world use.

---

## 🧩 What is a GSI?

- A **system.img** that follows AOSP layout
- Universal for ARM64, ARM32-binder64, or x86
- Built by Google (phhusson), or custom (Pixel+, Lineage, etc.)

---

## 📥 Downloading GSIs

### Official:
- [Google GSI images](https://source.android.com/docs/core/ota/gsi)
- [phhusson's GSI (GitHub)](https://github.com/phhusson/treble_experimentations)

### Community:
- Pixel Dust, Cherish, Project Elixir, RisingOS, etc.

Make sure to match:
- `arm64-ab`, `arm64-aonly`, etc.
- Android version supported by your device’s firmware

---

## 🔧 Preparing for GSI Flash

1. **Unlock bootloader**
2. **Extract or flash stock vendor, vbmeta, dtbo**
3. Format `/data` from recovery
4. Use `fastbootd` if using dynamic partitions

---

## 📦 Flashing GSI

```bash
fastboot reboot fastboot
fastboot erase system
fastboot flash system system.img
fastboot --disable-verity --disable-verification flash vbmeta vbmeta.img
fastboot reboot

> Replace vbmeta.img with one from your device’s stock firmware.




---

🛠 Common Fixes After Flashing

Issue	Fix

Bootloop	Use correct vbmeta, check dtbo
No SIM / RIL	Patch GSI with stock lib64/lib*ril.so
No Wi-Fi / BT	Use GSI Fix Magisk module
Camera crashes	Add camera blobs from stock
GApps issues	Use GSI with GApps or flash separately
System not writable	Use phh-su + adb remount
Encryption errors	Use decrypted userdata (Guide 10)



---

🧪 Debugging

adb logcat > log.txt
adb shell dmesg > dmesg.txt
adb shell getprop ro.treble.enabled

Check:

Is ro.treble.enabled= true?

Are HALs missing? (Wi-Fi, camera, etc.)

Do init.rc logs show denied mounts?



---

🔧 Patch GSI with GSI Kitchen (Optional)

Use GSI Kitchen to:

Add or remove GApps

Add custom boot animations, props

Patch VNDK/lib compatibility

Mount /product, /odm dynamically


🔗 https://github.com/eremitein/gsi-kitchen


---

💡 Tips for Successful Boot

Match system image type (a-only, ab)

Flash proper vbmeta.img

Disable encryption (forceencrypt, verity)

Patch with Magisk modules if needed

Avoid kernel mismatches



---

✅ Summary

Step	Tool / Fix

Flash GSI	fastbootd or recovery
Fix no SIM	RIL libs from stock
Fix Wi-Fi/Bluetooth	GSI Fix module or vendor blobs
Decryption error	Format /data + use DFE
GSI modding	GSI Kitchen, Magisk modules



---

> 🚀 GSIs are a powerful way to try AOSP/Pixel-based ROMs without building from source — just patch smartly and test often!



---
