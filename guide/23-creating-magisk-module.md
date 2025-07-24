# 🧩 Creating Your Own Magisk Module (Fixes, Tweaks, Add-ons)

Magisk modules let you inject files, patch props, or fix broken ROM/GSI behavior without modifying the actual system.  
This guide walks you through creating a **simple, clean, and systemless** Magisk module from scratch.

---

## 🧠 What Can a Magisk Module Do?

| Task                          | Possible via Module? |
|-------------------------------|-----------------------|
| Add missing `.so` libraries   | ✅ Yes                |
| Patch `build.prop` values     | ✅ Yes                |
| Fix Wi-Fi/camera              | ✅ If libs/configs needed |
| Load kernel `.ko` modules     | ✅ Yes (via scripts)  |
| Replace ringtones/fonts/icons | ✅ Yes                |

---

## 📁 Module Structure

MyModule/ ├── module.prop ├── config.sh (optional) ├── post-fs-data.sh (optional) ├── service.sh (optional) └── system/ └── lib64/ └── etc/ └── product/

All files inside `system/` are **mirrored into the actual system** during boot (systemless).

---

## ✍️ 1. `module.prop` Template

```text
id=wifi-fix-module
name=Wi-Fi HAL Patch for GSIs
version=1.0
versionCode=1
author=yourname
description=Adds missing Wi-Fi HAL files to vendor/lib

> 🔒 id must be unique (no spaces).




---

⚙️ 2. Optional Scripts

post-fs-data.sh

Runs after data is mounted — useful for prop changes.

#!/system/bin/sh
resetprop ro.product.model PixelPort

service.sh

Runs in background during boot. Use for mods that start services or daemon patches.

#!/system/bin/sh
sleep 10
setenforce 0

> Add chmod +x to both scripts if needed.




---

🔧 3. Add Fix Files

Let’s say you want to add Wi-Fi HAL:

MyModule/
└── system/
    └── vendor/
        └── lib64/
            └── libwifi-hal.so

✅ Place exactly as it should appear in real /system.


---

🗜️ 4. Zip the Module

Compress the full folder as .zip. Example:

wifi-fix-module.zip

Don’t zip from inside — zip the full folder with root files.


---

📦 5. Install via Magisk App

1. Open Magisk → Modules


2. Tap Install from storage


3. Choose your .zip


4. Reboot



✅ Done! Your fix is applied systemlessly.


---

🧪 Debugging Tips

Symptom	Fix

Module doesn't apply	Check file paths/case sensitive
Libs not loaded	Use `logcat
Props not changing	Ensure resetprop used properly
Services don't run	Debug service.sh permissions



---

✅ Summary

File	Purpose

module.prop	Module metadata (required)
system/	Injects files into system
post-fs-data.sh	Run script after early boot
service.sh	Background tasks (SELinux, etc.)
Zip → flash in Magisk	Deploys module systemlessly



---

> 🧠 Magisk modules are the cleanest way to patch GSIs, ROMs, or recoveries — no need to repack anything or touch /system.



---
