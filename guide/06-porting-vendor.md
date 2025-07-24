# 🏗️ How to Port a Vendor Image

The **vendor partition** contains drivers, configs, modules, and libraries that are specific to your device's hardware (Wi-Fi, camera, touch, etc.).  
Correctly porting the vendor is crucial for booting and ensuring everything works.

---

## 🛠 Tools Required

- **CRB Kitchen** (best for EXT4 vendors)
- **7Zip ZS**
- **WinMerge**
- **Notepad++** or XML/RC/PROP editor

---

## 📦 Step 1: Unpack Both Vendor Images

You need:
- Your **stock vendor**
- The **donor/vendor to be ported**

Use CRB Kitchen or 7Zip to extract both.

---

## 🔄 Step 2: Replace Key Files

### ✅ Copy These From Stock to Ported Vendor:
- `vendor/firmware/*`
- `vendor/etc/fstab.*`
- `vendor/etc/init/hw/init*.rc`

> Replace all **fstab mount lines**, especially inside `init*.rc`

### 🧠 Tips:
- Use **WinMerge** to compare `init_target.rc` and `init.rc` from both vendors
- Keep the **stock modprobe lines** (kernel module loaders)

---

## 🧩 Step 3: Kernel Drivers — `.ko` Modules

Look for:
```text
vendor/lib/modules/*.ko

These .ko files are kernel drivers for:

Touchscreen

Wi-Fi

Bluetooth

Graphics

FM Radio

GPS


> Replace .ko files with your stock ones if available.




---

📏 Step 4: Resize If Needed

If the final ported vendor.img is too large or small, resize it using:

make_ext4fs

resize2fs

or CRB Kitchen



---

🧠 Porting Between Architectures

You can port a 64-bit vendor to a 32-bit device if:

You use a 64-bit kernel

The vendor layout and SoC family are compatible


Check kernel config from boot.img:

CONFIG_ARM64=y


---

🔁 Matching Android Versions

Vendor Version	Use With Boot.img Version

Android 13	Boot.img from Android 13
Android 12	Boot.img from Android 12
Android 11	Boot.img from Android 11


> Mismatched boot/vendor can lead to bootloop, no display, or crashes.




---

📺 Reference Video

▶️ Watch on YouTube:
How to Port Basic Vendor


---

✅ Summary Checklist

[x] Unpack both stock and donor vendors

[x] Replace firmware, fstab, init.rc lines

[x] Copy .ko modules from stock

[x] Match Android version with boot.img

[x] Resize if needed

[x] Repack and test boot



---

> 🧪 Test with adb logcat and dmesg after flashing. Fix bugs based on logs.



---
