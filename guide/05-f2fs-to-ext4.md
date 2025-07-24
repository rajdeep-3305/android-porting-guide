# 🔄 Convert F2FS to EXT4

Some modern Android devices use the **F2FS (Flash-Friendly File System)**, which is often **read-only** when extracted.  
To make modifications, you need to convert it to **EXT4** — a fully writable format.

---

## 💡 When Do You Need This?

- You extracted a `system.img`, `vendor.img`, `product.img`, etc., and it’s **F2FS**
- You want to modify files inside but can’t mount or edit them
- You plan to repack the image after editing

---

## 🛠 Tools Required

- A **Linux system** (Fedora, Arch, Ubuntu, etc.)  
  OR use **WSL2 on Windows**
- `f2fs-tools` package
- `dd`, `mount`, `mkfs.ext4`, `tune2fs`, `cp` commands

---

## 🔧 Step-by-Step: Convert F2FS to EXT4

### 1. Install f2fs-tools

On Ubuntu/Debian:
```bash
sudo apt install f2fs-tools


---

2. Create folders and mount original F2FS image

mkdir system
sudo mount -o ro -t auto raw_f2fs_system.img system

> 📁 This mounts your F2FS image as read-only




---

3. Create a new blank EXT4 image

sudo dd if=/dev/zero of=system_new.img bs=6k count=1048576
sudo mkfs.ext4 system_new.img
sudo tune2fs -c0 -i0 system_new.img

> 🔢 This creates a 6GB system_new.img. Change bs and count as needed.




---

4. Mount EXT4 image and copy contents

mkdir new
sudo mount -o rw,sync,loop system_new.img new
sudo cp -fva system/* new/

✅ This copies everything from the original read-only mount into the new EXT4 image.


---

📦 You Now Have:

system_new.img → fully editable EXT4 version of your original F2FS image


You can now:

Modify files inside

Repack for flashing

Include in custom builds



---
