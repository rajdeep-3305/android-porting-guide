# 📦 Extracting Stock ROM Files for Porting and Patching

Whether you're porting a custom ROM, patching a GSI, or fixing a broken feature — having access to your **stock ROM files** is critical.  
This guide shows how to **extract and use boot.img, vbmeta, dtbo, system, vendor, firmware** and more from stock packages.

---

## 🧩 Why Extract Stock ROM Files?

| File           | Use Case                                 |
|----------------|-------------------------------------------|
| `boot.img`     | For Magisk patch, recovery compatibility  |
| `vbmeta.img`   | To disable AVB, patch GSI boot            |
| `dtbo.img`     | For fixing display/touch in custom recovery |
| `system.img`   | Compare to GSI, extract libs              |
| `vendor.img`   | Needed for ROM porting and compatibility  |
| `firmware/`    | Baseband, DSP, modem, etc.                |

---

## 📥 Stock ROM Formats

| Format         | Devices (Examples)              | Extract Tool            |
|----------------|----------------------------------|--------------------------|
| `.zip`         | Xiaomi, Pixel, Realme (some)     | 7-Zip, Payload Dumper    |
| `.tar.md5`     | Samsung                          | Odin / Heimdall          |
| `.ofp`         | Realme, Oppo                     | OZIPTool, mtkpayload     |
| `.nb0`         | Nokia (rare)                     | Hex editing (advanced)   |
| `.img`         | MTK dumps, backups               | None — already usable    |

---

## 🔧 Extraction Methods

---

### ✅ 1. Extract `.zip` or `.tar.md5`

Use **7-Zip** or **WinRAR** to get:
- `boot.img`
- `vbmeta.img`
- `dtbo.img`
- `system.img`
- `vendor.img`

For `.tar.md5`, remove `.md5` extension first.

---

### ✅ 2. Extract `payload.bin` (used by Pixel & MIUI)

Found inside some `.zip` ROMs.

Use [Payload Dumper Go](https://github.com/vm03/payload-dumper-go):

```bash
payload-dumper-go payload.bin

This gives:

boot.img

system.img

vendor.img

product.img
(Depending on ROM version)



---

✅ 3. Extract .ofp (Realme, Oppo, OnePlus)

Use:

OFPExtractor

Or mtk_extractor.py


Example:

python ofp_extractor.py ROM.ofp


---

✅ 4. Extract from MTK Scatter Firmware

Look for:

boot.img

recovery.img

system.img

vbmeta.img

dtbo.img

preloader.bin


✅ Already raw — no need to extract further.


---

🧠 Best Practices

Task	Tip

Fixing ROM compatibility	Always use matching vbmeta and dtbo
Porting recovery	Extract stock boot.img or recovery.img
GSI won’t boot	Replace kernel or patch DTBO
System/lib fix	Extract from system.img → mount or use simg2img
Vendor mismatch	Use your own stock vendor.img



---

💻 Mount System or Vendor Images

Convert sparse image to raw:

simg2img system.img system.raw.img

Mount:

sudo mount -o loop system.raw.img /mnt/system

Extract files you need: lib, lib64, etc, etc.


---

✅ Summary

Action	Tool

Extract .zip/.tar.md5	7-Zip, WinRAR
Dump payload.bin	Payload Dumper Go
Extract .ofp	OFPExtractor
Mount image files	simg2img + mount
Get stock partitions	Flash tool folder / by-name dump



---

> 🧪 Having clean stock ROM files makes debugging, porting, and recovering from bricks 10× easier — always keep your base firmware archived!



---
