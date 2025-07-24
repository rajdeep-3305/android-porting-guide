# ⚙️ Rooting Your Ported ROM (Magisk, Kernel Patching)

After successfully booting a custom ROM or GSI, you may want to **root** the system for additional control, debugging, and customizations.

This guide covers the most stable and universal method: **Magisk** root.

---

## 🔧 What You’ll Need

- `boot.img` from your ROM (stock or ported)
- Magisk app (latest)
- A phone with working **adb/fastboot**
- A PC or phone with patching capability (can be done without PC too)

---

## ✅ Method 1: Patch boot.img with Magisk

---

### Step-by-step:

1. Install **Magisk APK** on your Android device:  
   📥 [https://github.com/topjohnwu/Magisk](https://github.com/topjohnwu/Magisk)

2. Extract your `boot.img` (from payload.bin or firmware)

3. Copy `boot.img` to your phone

4. Open Magisk → Install → Select **"Select and Patch a File"**

5. Choose `boot.img`

6. It will generate a file like:

magisk_patched-XXXX.img

7. Copy the patched image back to PC (or use adb)

---

### Flash it via Fastboot:

```bash
fastboot flash boot magisk_patched.img

Or for A/B devices:

fastboot flash boot_a magisk_patched.img
fastboot flash boot_b magisk_patched.img

✅ Done! Your ROM is now rooted.


---

💡 What If You Don’t Have boot.img?

Extract it from:

payload.bin (use payload-dumper-go)

update.zip

Or your stock ROM zip


> Tools like Payload Dumper, MTK Extractor, or IMGExtractor can help.




---

🛑 Avoid Pre-rooted ROMs

Pre-rooted zips are often outdated and less secure

Magisk provides systemless rooting, making OTA and mods safer



---

🔁 Unroot or Remove Magisk

To unroot:

1. Open Magisk app → Uninstall Magisk


2. OR flash stock boot.img via fastboot




---

🧠 Advanced Tips

Task	Tip

Root GSIs	Patch stock boot.img from base firmware
Add modules	Place in /data/adb/modules/ or use Magisk app
Hide root (banking apps)	Use MagiskHide or Zygisk with DenyList
OTA compatibility	Use retail ROM boot.img when patching



---

🛠️ Optional: Use KernelSU (Advanced)

KernelSU is an alternative root system built directly into the kernel.
Requires compiling or patching kernel source.
Used on advanced custom ROM builds.

🔗 https://github.com/tiann/KernelSU


---

> ✅ Magisk is the safest and most versatile method for rooting Android 6.0 and up.



---
