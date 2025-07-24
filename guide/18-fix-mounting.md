# 🗂️ Fix /vendor, /product, /data Not Mounting in ROM or Recovery

Missing or broken mounts like `/vendor`, `/system`, `/product`, or `/data` can cause:
- Bootloops
- Broken Wi-Fi, RIL, or camera
- Recovery not detecting internal storage
- Failed flashing in TWRP

This guide helps you diagnose and fix these issues in custom ROMs, GSIs, and recoveries.

---

## 🧪 How to Know It’s a Mounting Issue

| Symptom                                 | Likely Cause             |
|-----------------------------------------|--------------------------|
| Recovery says `/vendor` not found       | Wrong `fstab` or missing partition |
| `/data` shows 0MB in TWRP               | Encrypted or broken format |
| ROM bootloop with `/system not found`   | Wrong mount flags or dynamic super |
| Apps crash due to missing libraries     | `/vendor` or `/product` not mounted |

---

## 🔧 Fixes Based on Partition Type

---

### ✅ A. `/vendor`, `/system`, `/product` Not Mounting

#### 1. Check `fstab` Entries

Found in:

/vendor/etc/fstab.*

Ensure entries look like this:

/vendor ext4 /dev/block/by-name/vendor ... /system ext4 /dev/block/by-name/system ... /product ext4 /dev/block/by-name/product ...

✅ Match partition names with actual device blocks:
```bash
ls -l /dev/block/by-name/

> If names mismatch, fix your fstab or rename mountpoints in init*.rc




---

2. Patch init*.rc

In boot/recovery ramdisk (init.rc, init.target.rc), fix lines like:

mount ext4 /dev/block/bootdevice/by-name/vendor /vendor

Make sure the device path is valid on your device.


---

✅ B. /data Not Mounting or Internal Storage Missing

1. Format Data Properly

In TWRP:

Use “Format Data” (not wipe)

Reboot recovery after formatting


2. FBE Encryption Fix

Check fstab flags:

/data ext4 /dev/block/... flags=encryptable=footer

Remove forceencrypt

Add encryptable=footer


3. Disable Quota (Optional)

Add in fstab:

/data ext4 ... noatime,nosuid,nodev,noexec,nodiratime,errors=panic


---

✅ C. System-as-root Fix (SAR)

On Android 10+ SAR devices, system is root-mounted:

Check /init.rc or fstab does not mount /system directly.
Let Android handle rootfs.


---

🧠 Dynamic Partition Handling

If your ROM uses dynamic partitions:

Mounts should point to logical partitions, not physical ones

Use fastbootd or lpunpack to inspect the actual layout



---

🧪 Debug Mount Failures

Use:

adb shell mount
adb shell ls /vendor
adb shell ls /data

Also use logcat:

adb logcat | grep -i mount


---

✅ Summary Fix Table

Issue	Fix

/vendor not found	Fix fstab or mount path
Internal storage 0MB	Format /data + DFE
Product libs not loading	Check /product mount path
TWRP can't mount system	Use SAR-compatible recovery
Dynamic system flash fails	Use fastbootd for partition resize



---

> 🧠 Always match fstab, DTB, and init.rc files to your exact partition layout — most mounting issues are just misnamed blocks!



---
