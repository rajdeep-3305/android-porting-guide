# 🧰 Tools, Fixes, and Flashables (Placeholder)

This folder contains helpful resources for Android ROM/recovery/GSI porting, organized into categories.

> ⚠️ These are currently **placeholder files**. Real tested tools will be added soon.

---

## 📦 magisk_modules/

Systemless flashable zips for patching on-the-fly.

| File               | Purpose                                |
|--------------------|-----------------------------------------|
| `permissive.zip`   | Sets SELinux to permissive              |
| `dfe.zip`          | Disables forced encryption              |
| `sepolicy-fix.zip` | Injects custom sepolicy rules           |

---

## 🛠️ system_fix/

Fix zips for common GSI bugs.

| File               | Fixes                                  |
|--------------------|-----------------------------------------|
| `camera_fix.zip`   | Missing camera blobs or configs         |
| `wifi_fix.zip`     | Broken Wi-Fi due to HAL mismatch        |
| `audio_fix.zip`    | No sound / mic / headphone jack issues  |

---

## 🔄 recovery/

Prebuilt recovery images for testing and flashing.

| File          | Description             |
|---------------|--------------------------|
| `twrp.img`    | TWRP recovery image      |
| `ofrp.img`    | OFRP/Fastboot recovery   |

---

## 🧪 scripts/

Handy tools for unpacking, patching, and debugging.

| Script               | Purpose                                      |
|----------------------|----------------------------------------------|
| `payload-dumper.py`  | Extract files from `payload.bin`             |
| `img-extract.sh`     | Mount or unpack `.img` files                 |
| `gsi-resign.sh`      | Re-sign GSI system images                    |

---

## 🚧 Notes

- All files here are safe placeholders (`# Placeholder file`) — ready to be replaced
- When uploading actual zips or scripts, make sure to describe them properly and update this table

> Want to contribute a tool or fix ZIP? Open a PR or drop it in Issues — credit will be given!
