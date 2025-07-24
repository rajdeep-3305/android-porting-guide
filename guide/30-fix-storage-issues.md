# 💾 Fixing Storage Issues in GSIs and Custom ROMs

GSIs or ported ROMs sometimes boot, but users face weird internal storage bugs like:

- **Internal storage = 0MB**
- **“Can’t mount /data”**
- **No access to storage in file manager**
- **File system errors after reboot**

This guide walks you through identifying and fixing storage problems.

---

## 🧪 Common Storage Symptoms

| Symptom                     | Likely Cause                         |
|-----------------------------|--------------------------------------|
| `/data` won't mount         | Wrong `fstab`, encrypted volume      |
| Internal storage = 0MB      | Encrypted `/data` + no decryption    |
| Apps can't access storage   | Wrong mount contexts or SELinux      |
| Reboots break storage       | Missing `vold` or bad partitions     |

---

## ✅ Step 1: Format `/data` Properly

In custom recovery (TWRP / OFOX):

1. Tap **Wipe** → **Format Data**
2. Type `yes` to confirm
3. Then reboot recovery **before system**

> ⚠️ Skipping this reboot can cause encryption fallback!

---

## ✅ Step 2: Patch `fstab` for Decryption

Edit `/vendor/etc/fstab.qcom` (or whatever matches your SoC).

Change this:

/data ext4 ... forceencrypt

To:

/data ext4 ... encryptable=footer

You may also add:

formattable length=-16384

Then repack and flash the image containing fstab (usually `vendor.img` or `boot.img`).

---

## ✅ Step 3: Disable Encryption (if needed)

Use a **DFE (Disable Force Encryption)** zip:
- Flash DFE after formatting `/data`
- Then flash Magisk if using root

---

## ✅ Step 4: Fix Permissions and Ownership

Boot into shell:

```bash
su
chown system:system /data
chmod 0771 /data

chown media_rw:media_rw /data/media/0
chmod 0770 /data/media/0

Run:

restorecon -v /data


---

✅ Step 5: Fix Mount Scripts

Some ported ROMs have broken /init.rc, /fstab, or /vold.rc.

Check:

Does /data have proper secontext? (ls -Z /)

Does vold start at boot? (ps | grep vold)

Is /storage/emulated mounted?



---

🧪 Optional: Patch Boot Image Props

Inside default.prop or build.prop, add:

persist.sys.usb.config=mtp,adb
persist.sys.storage.umd.enabled=true

This helps trigger MTP access via USB and internal media scanner.


---

✅ Summary

Problem	Fix

/data fails to mount	Format properly + patch fstab
0MB internal storage	Patch encryption or use DFE
Apps can’t access files	Run restorecon, fix /data perms
No MTP on PC	Patch build.prop USB config



---

> 💾 Storage bugs are often caused by bad mounts or encryption leftovers — fix them early so you can avoid re-flashing later!



---
