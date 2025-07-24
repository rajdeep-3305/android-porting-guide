# 🧩 Using Magisk Modules to Fix & Tweak ROMs

Magisk modules are systemless modifications that extend functionality, fix bugs, and enable features — all without modifying the system partition.

This guide covers how to use, install, and build simple Magisk modules for ROM/GSI compatibility.

---

## 🧰 What Are Magisk Modules?

Magisk modules are `.zip` files that install via Magisk and:
- Add missing libs or binaries
- Patch `build.prop`
- Load `.ko` kernel modules
- Inject files into system/vendor/product

---

## 📦 How to Install a Magisk Module

### ✅ From Magisk App:
1. Open Magisk → Modules
2. Tap **Install from storage**
3. Select `.zip` module
4. Reboot

### ✅ From Recovery (TWRP):
- Flash `.zip` like a normal mod
- Only works if Magisk is installed

---

## 🔧 Useful Modules for ROM Fixing

| Module Name            | Use Case                                    |
|------------------------|---------------------------------------------|
| **WifiLibsFix**        | Fix Wi-Fi drivers or HAL for GSIs           |
| **Camera2API Enabler** | Force-enable Camera2 on devices              |
| **GAppsFix**           | Fix Play Store/Google services on GSIs      |
| **Binder64 Fix**       | Enable 64-bit binder for some devices       |
| **SafetyNetFix**       | Pass SafetyNet & CTS checks                  |
| **OneUI Port Helper**  | Required for Samsung ROM ports              |
| **KernelMods Loader**  | Load .ko drivers into live kernel           |

> 🔗 You can find many on [https://github.com/Magisk-Modules-Repo](https://github.com/Magisk-Modules-Repo)

---

## 🧪 Build a Simple Magisk Module

### Folder structure:

YourModule/ ├── module.prop ├── system/ │   └── etc/ │       └── yourfile.conf

### `module.prop` example:

id=example-module name=Example Config Tweaks version=1.0 versionCode=1 author=yourname description=Adds missing config for audio and display

Put your modified files inside `system/`, `vendor/`, or `product/` folders (mirroring Android structure).

Compress the folder as `.zip` → install via Magisk.

---

## 🧠 Tips for Porters

- You can use modules to:
  - Inject missing blobs into GSIs
  - Patch `build.prop` dynamically
  - Overlay fonts, ringtones, or icons
  - Load patched `lib*.so` into system/vendor

- For debugging, use:

adb shell su -c "magisk --help"

- Temporary module changes are reversible — great for testing!

---

## 🔄 Remove a Module

- From Magisk app → tap trash icon next to module  
- OR manually delete folder in `/data/adb/modules/`  
- Then reboot

---

## ✅ Summary

| Action                     | Tool / Method                          |
|----------------------------|----------------------------------------|
| Install module             | Magisk app or recovery                 |
| Create new module          | Zip `module.prop` + file structure     |
| Use module for port fixes  | Add `.so`, `.ko`, or conf files        |
| Debug module effects       | `logcat`, `adb shell`, `/magisk/` paths |

---

> 🔧 Magisk modules let you fix port bugs without touching the base ROM. Modular, safe, and powerful!


---
