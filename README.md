<p align="center">
  <img src="Androids.jpeg" width="100%">
</p>

# 🔧 Android ROM / Recovery Porting Toolkit

</div>

<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/platform-Android-3ddc84?logo=android&logoColor=white" alt="Android"></a>
  <a href="#"><img src="https://img.shields.io/badge/type-GSI%20Porting-blueviolet" alt="GSI"></a>
  <a href="#"><img src="https://img.shields.io/badge/license-MIT-lightgrey" alt="License"></a>
  <a href="#"><img src="https://img.shields.io/badge/status-actively--maintained-brightgreen" alt="Maintained"></a>
</p>

---

## 🧠 What This Is

A full collection of **real-world Android ROM & recovery porting guides**, based on experience across dozens of devices and countless reboots, bugs, logcats, and bricked boots.

This isn't copy-paste stuff — it's from actually fixing things:
- GSIs that won't boot
- Recoveries that crash
- Boot loops with no logs
- Audio, camera, or Wi-Fi that's just dead after a flash

---

## 📖 Quick Access

- [ROM Porting Basics](guide/02-rom-porting-basic.md)
- [Advanced ROM Porting](guide/03-rom-porting-advance.md)
- [GSI Boot Fixing](guide/06-gsi-boot-fix.md)
- [Recovery Porting](guide/09-recovery-port.md)
- [Magisk Module Creation](guide/23-creating-magisk-module.md)
- [SELinux / Permissions Fix](guide/26-permission-sepolicy-fix.md)
- [Audio / Mic Fixes](guide/27-fix-audio-gsi.md)
- [Mount/Edit .img Files](guide/31-mount-edit-img.md)

---

## 📚 All Available Guides

| # | Guide Title | Link |
|--:|-------------|------|
| 1 | What You Need (Tools & Setup) | [Guide 1](guide/01-what-you-need.md) |
| 2 | ROM Porting Basics | [Guide 2](guide/02-rom-porting-basic.md) |
| 3 | Advanced ROM Porting | [Guide 3](guide/03-rom-porting-advance.md) |
| 4 | GSI Porting Essentials | [Guide 4](guide/04-gsi-porting.md) |
| 5 | Dumping Vendor / Boot | [Guide 5](guide/05-how-to-dump.md) |
| 6 | GSI Boot Fixing | [Guide 6](guide/06-gsi-boot-fix.md) |
| 7 | GSI Bug Fixing | [Guide 7](guide/07-gsi-bug-fix.md) |
| 8 | Fix Touchscreen / Rotation | [Guide 8](guide/08-rotation-touch.md) |
| 9 | Recovery Porting (Manual) | [Guide 9](guide/09-recovery-port.md) |
| 10 | Device Tree Recovery Porting | [Guide 10](guide/10-recovery-treble.md) |
| 11 | Bootloop Fixing | [Guide 11](guide/11-bootloop-fix.md) |
| 12 | Magisk Boot Patching | [Guide 12](guide/12-magisk-boot.md) |
| 13 | Fixing Boot.img Manually | [Guide 13](guide/13-bootimg-manual.md) |
| 14 | DTBO & vbmeta Patching | [Guide 14](guide/14-dtbo-vbmeta.md) |
| 15 | Build Boot.img from Scratch | [Guide 15](guide/15-build-boot.md) |
| 16 | Use MagiskBoot / AIK | [Guide 16](guide/16-magiskboot.md) |
| 17 | build.prop / system.prop Edits | [Guide 17](guide/17-buildprop.md) |
| 18 | init.rc & Service.rc Editing | [Guide 18](guide/18-initrc.md) |
| 19 | Debug Boot / Init Failures | [Guide 19](guide/19-debug-init.md) |
| 20 | Use PHH Patches on GSI | [Guide 20](guide/20-phh-patch.md) |
| 21 | Partition Flashing (Properly) | [Guide 21](guide/21-partition-flash.md) |
| 22 | A/B + Dynamic Partitions | [Guide 22](guide/22-ab-dynamic.md) |
| 23 | Create Magisk Modules | [Guide 23](guide/23-creating-magisk-module.md) |
| 24 | Fix Camera/WiFi GSI Bugs | [Guide 24](guide/24-fix-camera-wifi-gsi.md) |
| 25 | Fix Boot Loop on Reboot | [Guide 25](guide/25-reboot-issues.md) |
| 26 | SELinux & Permission Fixing | [Guide 26](guide/26-permission-sepolicy-fix.md) |
| 27 | Fix Audio / Mic / Calls | [Guide 27](guide/27-fix-audio-gsi.md) |
| 28 | Optimize Boot / Battery / Thermals | [Guide 28](guide/28-optimize-performance.md) |
| 29 | Best Debugging Tools | [Guide 29](guide/29-debugging-tools.md) |
| 30 | Fix Storage / Internal = 0MB | [Guide 30](guide/30-fix-storage-issues.md) |
| 31 | Mount & Edit `.img` Partitions | [Guide 31](guide/31-mount-edit-img.md) |

---

## 🧰 tools/ (Coming Soon)

This will include:
- ✅ Magisk modules (permissive, sepolicy patchers, DFE, etc.)
- ✅ HAL patch ZIPs (for Wi-Fi, Audio, RIL)
- ✅ Unpack/repack tools, fix scripts, common debug binaries

---

## 📎 Notes

- Tested on real devices — not just in VMs/emulators
- SoC coverage: Unisoc
- Android 10 to 16, Treble + non-Treble
- Most guides are systemless-friendly via Magisk

---

## 🙌 Credits

Big shoutout to:
- XDA devs and testers
- phhusson’s GSI base
- TWRP/OFRP maintainers
- Everyone who’s shared logs, zips, and broken boots

---

## ✉️ Contribute / Contact

Found a bug? Got a fix or better method?  
➡️ Open an issue or send a PR — happy to merge helpful content.  
Let’s keep building for newer devices together.
