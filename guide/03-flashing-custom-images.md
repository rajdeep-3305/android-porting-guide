# 📤 Flashing Custom Images

Flashing custom ROM components like `system.img`, `vendor.img`, and `super.img` requires some setup to bypass Android Verified Boot (AVB) and ensure compatibility with your device’s partition layout.

---

## 🔐 Disable AVB with Empty VBMETA

Most devices require an **empty vbmeta** to flash GSIs, recoveries, or other unsigned images.

### ✅ Files to flash:
- `vbmeta.img`
- `vbmeta_system.img`
- `vbmeta_vendor.img`

You can patch these using:
- **CRB Kitchen**
- **Magisk patched boot image**
- **vbmeta stub from forums**

### 💡 Flash using Fastboot:
```bash
fastboot flash vbmeta vbmeta.img
fastboot flash vbmeta_system vbmeta_system.img
fastboot flash vbmeta_vendor vbmeta_vendor.img

Or use Odin, MTKClient, or EDL tools depending on your device.


---

🚀 Enter FastbootD Mode

Only fastbootd can flash and resize dynamic partitions (system, vendor, etc.).

✅ Reboot into fastbootd:

fastboot reboot fastboot

Then flash your images:

fastboot flash system system.img
fastboot flash vendor vendor.img

> ⚠️ TWRP cannot resize dynamic partitions. Always use fastbootd for large image flashing.




---

🛠 Devices Without FastbootD (e.g., Samsung)

Some Samsung devices don’t support fastbootd. You can patch your recovery to enable it:

🔗 Patch Samsung Recovery for fastbootd (GitHub)


---

🧠 Notes

If vbmeta is not flashed or disabled, boot will fail with Orange State or Red State

Using Magisk patched boot.img can bypass AVB on boot, but not for system/vendor

Always backup your original images (boot.img, vbmeta.img, etc.)



---

✅ Summary Table

Task	Tool

Flash vbmeta images	fastboot, odin, mtk
Flash system and vendor	fastbootd only
Resize partitions	fastbootd only
Patch recovery for fastbootd	Johx22’s Tool
Add root / Magisk	Patch boot.img and flash



---

> ✅ You’re now ready to flash system-level images safely and bypass AVB.



---
