# 🗂️ How to Mount and Edit Android Image Files (`system.img`, `vendor.img`, etc.)

When porting ROMs, fixing GSIs, or debugging recoveries, you’ll often need to extract or mount:

- `system.img`
- `vendor.img`
- `product.img`
- `odm.img`

These files may be in **sparse format**, and you must convert or mount them on Linux to access contents.

---

## 🧪 Types of Android Images

| Format          | What it Means                   | How to Mount           |
|------------------|----------------------------------|-------------------------|
| Sparse Image     | Compressed format (`simg`)       | Use `simg2img` first    |
| Raw EXT4 Image   | Regular file system image        | Mount directly via loop |
| EROFS/SquashFS    | Read-only compressed system      | Use `mount -t erofs`    |
| `.new.dat.br`    | Android OTA update format        | Use `sdat2img.py`       |

---

## ✅ Step 1: Convert Sparse Image to Raw

```bash
simg2img system.img system.raw.img

You’ll now have a system.raw.img which can be mounted.

Install if missing:

sudo apt install android-sdk-libsparse-utils


---

✅ Step 2: Mount the Raw Image

Create mount point:

mkdir /mnt/system
sudo mount -o loop system.raw.img /mnt/system

✅ Now you can browse, copy, or patch files.

To unmount:

sudo umount /mnt/system


---

✅ Step 3: Edit Files and Repack (Optional)

If you want to modify and repackage:

1. Mount → Copy files to working folder


2. Modify what you need


3. Create new image:



make_ext4fs -s -l 2097152000 -a system new_system.img system_folder/

-s = sparse output

-l = size (adjust to your needs)

-a = mount point name



---

✅ Alternative: Use Loop-Mount Tools (Easy GUI)

On Linux:

Use gnome-disk-utility

Or Archivemount

Or scripts like loopmount.sh


Great for beginners who don’t want to use CLI.


---

🧪 Mount EROFS or SquashFS (Advanced)

Some Android 11+ ROMs use read-only filesystems like EROFS.

Mounting EROFS:

sudo mount -t erofs -o loop system.erofs.img /mnt/system

Install support if needed:

sudo apt install erofs-utils


---

✅ Tools You’ll Need

Tool	Purpose

simg2img	Sparse → raw image
make_ext4fs	Build new ext4 image
mount	Mount loop device
erofs-utils	Handle Android 11+ system.img
img2simg	Raw → sparse (optional)



---

✅ Summary

Task	Command / Tool

Convert .img to mountable	simg2img
Mount on Linux	sudo mount -o loop
Unmount	sudo umount /mnt/folder
Repack modified system	make_ext4fs
Handle new EROFS formats	erofs-utils, mount -t erofs



---

> 🗂️ Knowing how to mount and manipulate .img files lets you patch anything — no need to reflash whole ROMs just to tweak one lib or config!



---
