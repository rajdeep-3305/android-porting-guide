# 💥 Flashing Methods for ROMs, GSIs, and Recoveries

Flashing a custom ROM or recovery can vary depending on device type, partition setup (A-only, A/B), and whether the phone uses dynamic partitions.  
This guide summarizes **all safe flashing methods** across devices — including fastboot, recovery, fastbootd, and SP Flash Tool.

---

## 📲 Types of Partitions

| Type     | Devices (Examples)             |
|----------|--------------------------------|
| A-only   | Older Samsung, MTK, early SD   |
| A/B      | Most Android 10+ devices       |
| Dynamic  | Dynamic super.img (Android 10+)|

Check using:
```bash
adb shell getprop ro.boot.slot_suffix

If output is _a or _b, your device uses A/B slots.



---

🔧 1. Flash via Fastboot

⚙️ Bootloader must be unlocked

fastboot flash boot boot.img
fastboot flash recovery recovery.img
fastboot flash system system.img

For A/B devices:

fastboot flash boot_a boot.img
fastboot flash boot_b boot.img

Use:

fastboot getvar all

To verify partition names.


---

🔧 2. Flash via fastbootd (for Dynamic Devices)

For flashing logical partitions like system, vendor, product on dynamic partition devices:

fastboot reboot fastboot

Then:

fastboot flash system system.img
fastboot flash vendor vendor.img

> ✅ Use this when fastboot flash gives size errors.




---

🔧 3. Flash via Custom Recovery (TWRP, OrangeFox)

Best for installing .zip files like:

Custom ROMs

Magisk

DFE

GApps

Kernel zips


TWRP Install:

1. Wipe → Advanced Wipe → Dalvik + Cache + Data + System
2. Flash ROM.zip
3. (Optional) Flash GApps + Magisk + DFE
4. Reboot

> ⚠️ Make sure TWRP supports your device & encryption.




---

🔧 4. Flash via SP Flash Tool (for MTK Devices)

For MTK-based phones (Infinix, Tecno, older Xiaomi/Realme):

1. Use MTK Auth Bypass (if needed)


2. Load scatter.txt


3. Select boot, recovery, system, etc.


4. Flash selected partitions



> SPFT is powerful — always double-check scatter file paths.




---

🧠 Tips for Safe Flashing

Tip	Why It's Important

Backup boot.img, vbmeta.img	For recovery if anything fails
Flash vbmeta.img with --disable-verity	To prevent boot verification
Use exact partition names	Mismatch = no boot or brick
Always reboot to recovery after format	Prevents encryption relock



---

📄 Example: Flash GSI on A/B Dynamic Device

fastboot reboot fastboot
fastboot flash system system.img
fastboot --disable-verity --disable-verification flash vbmeta vbmeta.img
fastboot reboot


---

📄 Example: Flash ROM via TWRP

1. Format Data
2. Flash ROM.zip
3. Flash Magisk.zip (optional)
4. Flash DFE.zip (if encrypted)
5. Reboot → System


---

✅ Summary

Method	Use Case

fastboot	Boot, recovery, A-only system flashes
fastbootd	Dynamic partitions (system, vendor)
TWRP/OrangeFox	ROM zip, GApps, modules
SP Flash Tool	Full MTK firmware flash



---

> 🧪 Flashing is risky — read partition names, sizes, and logs carefully. Always backup your boot, vbmeta, and dtbo before testing ROMs.



---
