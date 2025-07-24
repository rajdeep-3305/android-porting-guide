# 🔍 Identify Your Device

Before porting anything, you need to know the device’s structure and software stack.

---

## 📱 Key Things to Identify

- **Architecture**:  
  - `ARM32` vs `ARM64`  
  - Check with boot.img kernel config: look for `CONFIG_ARM64=y` and `CONFIG_64BIT=y`

- **Partitioning**:  
  - A-only or A/B (check for `boot_a`, `boot_b`)

- **File System**:
  - EXT4, F2FS, or EROFS  
  - Check `vendor/etc/fstab*` and partition images

---

## 📂 Common Partition Types

| Partition   | Purpose                 |
|-------------|--------------------------|
| `system`    | Main OS files            |
| `vendor`    | Hardware blobs & config  |
| `product`   | OEM-specific config      |
| `odm`       | Device-specific blobs    |
| `super`     | Merged dynamic partitions (system, vendor, etc.) |

---

## 🎯 How to Check File System Type

Open `fstab` in `vendor/etc/` and look for lines like:
