# 🧷 Patching vbmeta & dtbo.img for Custom ROMs and GSIs

On modern Android devices, **vbmeta.img** (Verified Boot Metadata) and **dtbo.img** (Device Tree Blob Overlay) are critical for successful booting.  
They enforce **dm-verity**, **AVB (Android Verified Boot)**, and **device tree correctness**.

This guide explains how to disable verification and patch `vbmeta` / `dtbo` properly.

---

## 📦 What is vbmeta.img?

- Stores verified boot metadata (AVB v2.0)
- Verifies system, boot, vendor partitions at boot time
- Often prevents modified images from booting

---

## 📦 What is dtbo.img?

- Device Tree Blob Overlay
- Extends the base kernel DTB
- Often used to enable display, touch, sensors, etc.

---

## 🔧 Why Patch vbmeta?

| Situation                         | Why Patch?                      |
|----------------------------------|---------------------------------|
| Bootloop after flashing GSI/ROM  | Prevent AVB verification failure |
| TWRP says “no valid slot”        | Corrupted or unpatched vbmeta   |
| `dm-verity` error on boot        | vbmeta verifies `/system` hash  |

---

## ✅ Disable Verity & Verification

If you have stock `vbmeta.img`, use this command:
```bash
fastboot --disable-verity --disable-verification flash vbmeta vbmeta.img

Or flash empty vbmeta (dangerous on some devices):

fastboot flash vbmeta empty_vbmeta.img

> ⚠️ Some devices (like Samsung, Huawei) need valid signed vbmeta.




---

🧪 How to Get Stock vbmeta.img

From firmware zip (often in images/ or firmware-update/)

From device dump:


adb shell
su
dd if=/dev/block/by-name/vbmeta of=/sdcard/vbmeta.img


---

🔧 Patching dtbo.img

1. Extract from firmware or use:



adb shell su
dd if=/dev/block/by-name/dtbo of=/sdcard/dtbo.img

2. Patch via:



MagiskBoot (command line)

AIK or CRB Kitchen (built-in support)


3. Repack and flash:



fastboot flash dtbo dtbo.img


---

💡 When to Replace or Patch dtbo

Issue	Fix (dtbo related?)

No display in recovery	✅ Replace with stock DTBO
Touch not working	✅ Often DTBO or DTB issue
Boot stuck at logo	✅ Kernel + DTBO mismatch
GSI fails after flash	✅ Patch DTBO or replace



---

🛠 Tools You Can Use

Tool	Purpose

MagiskBoot	Patch/inspect vbmeta, dtbo
AIK	Extract/patch boot+dtbo
CRB Kitchen	Full boot image processing
lpmake	dtbo inside dynamic images



---

✅ Summary

Task	Tool / Command

Patch vbmeta	fastboot --disable-verity --disable-verification
Dump vbmeta/dtbo	dd from /dev/block/by-name/
Patch dtbo	AIK, MagiskBoot, CRB Kitchen
Flash patched vbmeta	fastboot flash vbmeta vbmeta.img
Flash patched dtbo	fastboot flash dtbo dtbo.img



---

> 🔐 Patch vbmeta and dtbo responsibly — one wrong image can soft-brick your phone. Always keep backups of stock images before testing custom ROMs.



---
