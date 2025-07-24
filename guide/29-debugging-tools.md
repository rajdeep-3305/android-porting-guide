# 🧰 Best Debugging Tools for Android ROM & GSI Porting

Fixing broken Wi-Fi or bootloops is one thing — knowing *how* to debug it properly is what separates beginners from pros.  
Here’s a curated list of **essential tools and commands** every Android ROM/GSI porter should master.

---

## 🧪 🖥️ PC Tools

| Tool                   | Purpose                              |
|------------------------|---------------------------------------|
| **ADB + Fastboot**     | Core communication tools             |
| **logcat**             | Real-time logs from device           |
| **dmesg**              | Kernel-level hardware logs           |
| **AIK** (Image Kitchen)| Extract/repack boot and recovery     |
| **Payload Dumper**     | Extract `payload.bin` from stock zips|
| **simg2img / img2simg**| Convert sparse ↔ raw image formats   |
| **MagiskBoot**         | Advanced unpack/patching of boot.img |
| **Heimdall / Odin**    | Flashing Samsung firmware (tar.md5)  |
| **libncurses / hexedit**| Low-level blob or DTB editing       |

> Always keep these in a portable folder like `Android-Tools/`

---

## 📱 On-Device Debugging (ADB Shell)

### 🔍 Check Hardware Info
```bash
getprop | grep -iE 'hardware|board|soc|device'

🧱 Mount Partitions

ls -l /dev/block/bootdevice/by-name
mount /vendor

🔥 Monitor Logs

logcat -d > log.txt
dmesg > dmesg.txt

🧪 Check Boot Reason

cat /proc/last_kmsg


---

🔧 Boot Image Debugging

Extract Boot Image

unpackimg.sh boot.img
# OR use AIK or MagiskBoot

Check:

default.prop

fstab.*

init.rc


Modify & reflash with:

mkbootimg --kernel zImage --ramdisk ramdisk.cpio.gz ...
fastboot flash boot new_boot.img


---

🔐 SELinux & Permissions

Check SELinux State

getenforce

View File Contexts

ls -Z /vendor/lib64/

Temporarily Disable SELinux

setenforce 0


---

📁 Logcat Filters for Specific Bugs

Log Filter	What It Shows

`logcat	grep -i audio`
`logcat	grep -i ril`
`logcat	grep -i hal`
`logcat	grep -i binder`
`logcat	grep -i denied`



---

🧠 GSI-Specific Tools

Tool / App	Use Case

Treble Info (Play Store)	Show A/B slot, VNDK, Treble status
phh Treble Settings	Built-in settings panel in phh GSIs
DSU Loader (root)	Test GSIs without flashing



---

📂 Helpful Paths to Check

Path	What’s Inside

/vendor/etc/audio/	Mixer paths, audio configs
/system/lib*/hw/	HAL libraries
/vendor/lib*/hw/	Vendor HALs (Wi-Fi, BT, RIL, etc.)
/proc/last_kmsg	Previous boot crash logs
/data/tombstones/	App crashes & native segfaults



---

✅ Summary

Task	Tool

View logs	logcat, dmesg
Boot.img analysis	AIK, MagiskBoot
Extract stock partitions	payload-dumper, dd, 7zip
Debug Wi-Fi or HALs	ADB shell + `logcat
Patch file-level perms	chown, chmod, restorecon



---

> 🧠 Tools don’t fix things — you do. But using the right tool at the right time can save hours of guessing and help you pinpoint even the nastiest GSI or recovery bugs.



---
