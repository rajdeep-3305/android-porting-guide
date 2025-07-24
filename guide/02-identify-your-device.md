# 🔍 Identify Your Device

Before you begin porting or flashing, you must understand the layout and internals of your device.

---

## 📱 Key Information to Identify

- **Architecture**:  
  - `ARM32` or `ARM64`  
  - Extract `boot.img`, then check for `CONFIG_ARM64=y` inside kernel config

- **Partition Type**:  
  - A-only or A/B  
  - Check for `boot`, `boot_a`, `boot_b` using fastboot or partition manager

- **File System**:  
  - EXT4, F2FS, or EROFS  
  - Open `vendor/etc/fstab*` and check mount types

---

## 📂 Common Android Partitions

| Partition   | Purpose                        |
|-------------|--------------------------------|
| `system`    | Android OS                     |
| `vendor`    | HALs, proprietary libraries    |
| `product`   | OEM config and apps            |
| `odm`       | Device-specific drivers        |
| `super`     | A dynamic partition that holds the rest |

---

## 🎯 How to Check File System

Open `fstab` from `vendor/etc/` and look for something like:

/dev/block/by-name/system  /system  ext4  ro,barrier=1

Possible types:
- `ext4` – fully supported
- `f2fs` – mostly readonly
- `erofs` – used by Huawei, some Xiaomi/Samsung

---

## 📊 GSI Compatibility by Vendor Version

| Vendor Version | GSI Minimum Version |
|----------------|---------------------|
| 33             | Android 13+         |
| 32             | Android 12.1+       |
| 31             | Android 12+         |
| 30             | Android 11+         |
| 29             | Android 10+         |

---

## ✅ Example

Samsung Galaxy M01:
- A-only
- ARM64
- Uses `super` partition
- File system: F2FS

Use this info to pick the right GSI/vendor/system images for porting.


---
