# 💾 Porting Custom Recovery (TWRP / OrangeFox)

Porting a custom recovery (like TWRP or OrangeFox) is essential for installing custom ROMs, formatting partitions, and debugging bootloops.

This guide covers how to port a recovery from a similar device and make it boot on yours.

---

## 🧰 What You Need

- **Stock recovery.img** of your device
- **Recovery.img** from a similar device (same SoC, resolution, Android version)
- **AIK (Android Image Kitchen)** – to unpack/repack images
- **Hex editor (HxD)** – optional for advanced work
- **TWRP builder kitchen** – optional

---

## 📦 Step 1: Unpack Both Recoveries

Use AIK to unpack both:
```bash
./unpackimg.sh recovery.img

Compare:

ramdisk contents (init.rc, sbin, default.prop, etc.)

Kernel and DTB/DTBO if needed



---

🔧 Step 2: Replace Ramdisk (If Needed)

You can try:

Using stock kernel + TWRP ramdisk

OR using TWRP kernel + stock ramdisk (rare)


Most stable method:

Use your stock kernel with ported recovery’s ramdisk



---

📋 Step 3: Patch default.prop

Inside the ramdisk, check default.prop:

ro.debuggable=1
ro.secure=0

Change values to match your base system if needed.


---

⚙️ Step 4: Fix fstab and Partition Paths

Edit:

/ramdisk/etc/recovery.fstab

Make sure partition names match your device (e.g., system, vendor, product, userdata).

Use your stock fstab as a reference — it's usually found in:

vendor/etc/fstab.*


---

🧪 Step 5: Test Boot

Repack recovery using AIK:

./repackimg.sh

Flash with:

fastboot flash recovery recovery.img
fastboot boot recovery.img

OR use adb sideload or Odin if using Samsung devices.


---

🛠 Common Issues & Fixes

Issue	Fix

Bootloop	Wrong kernel or broken ramdisk
Touch not working	Kernel DTB mismatch or missing drivers
Internal storage missing	Wrong fstab or selinux labels
Red error logs	Check recovery.log in /tmp/ or via ADB



---

📺 Recommended Videos

▶️ Port TWRP for any Android device
▶️ Advanced Recovery Porting


---

✅ Summary

Use stock kernel + donor ramdisk for best chance of success

Always match partition paths in fstab

Compare and debug with adb logcat or recovery.log



---

> 🔐 A good recovery is your fail-safe. Always test thoroughly before sharing publicly.



---
