# 📐 Understanding Dynamic Partitions

Starting with Android 10, many devices switched to **dynamic partitioning**, which merges system-related partitions like `system`, `vendor`, `product`, `odm`, and `system_ext` into a single **super partition**.

This guide explains how to manage, unpack, repack, and flash dynamic partitions.

---

## 🧩 What Are Dynamic Partitions?

Instead of static partitions, Android now uses **logical partitions** stored inside a **dynamic `super.img`**.

| Logical Partition | Purpose                        |
|-------------------|--------------------------------|
| `system`          | Core Android OS                |
| `vendor`          | Hardware blobs and configs     |
| `product`         | OEM configurations and apps    |
| `odm`             | Device-specific drivers        |
| `system_ext`      | Additional AOSP or OEM content |

All these are packed together inside `super.img`.

---

## 🔍 How to Check If Your Device Uses Dynamic Partitions

Use `adb shell` or recovery terminal:
```bash
ls -l /dev/block/by-name/

If you don’t see partitions like system, vendor, product, etc., but see super, your device uses dynamic partitions.


---

📦 Extracting Super.img

Step-by-step:

1. Convert sparse image to raw:

simg2img super.img super.raw


2. Use 7Zip ZS, CRB Kitchen, or lpunpack to extract:

lpunpack super.img out_dir/



You’ll get:

system.img

vendor.img

product.img

etc.



---

🛠 Repacking Dynamic Partitions

Use LPTools, DSU Builder, or CRB Kitchen to:

Repack system.img, vendor.img, etc.

Recreate super.img for flashing


Example tool: lpmake

lpmake --metadata-size 65536 \
  --super-name super \
  --device super:3221225472 \
  --group main:3221225472 \
  --partition system:readonly:1073741824:main \
  --image system=system.img \
  ...

> Advanced use only — requires exact partition layout and size math




---

🧨 Flashing System/Vendor on Dynamic Devices

Use fastbootd:

fastboot reboot fastboot
fastboot flash system system.img
fastboot flash vendor vendor.img

> Only fastbootd can resize partitions before flashing.
TWRP cannot do this for dynamic partitions.




---

🔄 Convert Static ROM to Dynamic

If you have a legacy A-only ROM (non-dynamic) and want to port it to dynamic devices:

Use CRB Kitchen to repack images

Rebuild super.img

Replace the vendor partition as explained in Guide 6



---

⚠️ Warnings

Sizes must be exact when rebuilding super.img

Wrong size or layout = fastboot flash error or brick

Always test on a secondary device or use emulated GSI testbed



---

✅ Summary

Task	Tool

Extract super.img	simg2img, lpunpack, 7Zip
Rebuild super.img	lpmake, CRB, DSU Builder
Flash dynamic partitions	fastbootd
Convert static to dynamic	CRB Kitchen, manual split



---

> 🧠 Mastering dynamic partitions is key for Android 10+ ROMs. Always triple-check your sizes and layout!



---
