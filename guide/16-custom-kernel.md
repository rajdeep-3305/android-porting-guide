# 🛠️ Using a Custom Kernel with Your ROM or Recovery

Sometimes your ROM won’t boot, or key features like touch, display, or encryption are broken.  
In such cases, replacing or patching the **kernel** (inside `boot.img`) can fix the issue or unlock performance and root capabilities.

This guide shows how to **use**, **build**, or **patch** a custom kernel.

---

## 🧠 What Is the Kernel?

The Android kernel is a Linux-based core that handles:
- Booting
- Hardware access
- Device drivers
- Battery, CPU, GPU, storage, etc.

It’s stored inside `boot.img` or `kernel` partition.

---

## 🧩 When Should You Replace the Kernel?

| Symptom                  | Kernel-Related?         |
|--------------------------|-------------------------|
| No display/touch         | ✅ Yes (check DTB too)  |
| Bootloop at early stage  | ✅ Yes                  |
| Magisk root fails        | ✅ Yes (use patched kernel) |
| GSI fails to boot        | ✅ Often fixed by kernel swap |
| RIL/Wi-Fi bugs           | ❌ Usually vendor-related |

---

## ✅ Method 1: Use a Custom Kernel Zip

If available for your device:

1. Flash the custom kernel `.zip` using recovery (TWRP/OrangeFox)
2. OR extract the `boot.img` from the zip and flash manually:
   ```bash
   fastboot flash boot custom_boot.img

> ✅ Done — test the ROM again.




---

🔧 Method 2: Patch Stock Kernel (e.g. for Magisk)

1. Extract boot.img from your ROM


2. Patch with Magisk (see Guide 12)


3. Flash patched boot.img:

fastboot flash boot magisk_patched.img




---

🏗️ Method 3: Compile Your Own Kernel (Advanced)

To build from source:

Prerequisites:

GCC/Clang toolchain

Device-specific kernel source

.config or defconfig for your device

A Linux build environment


Build commands:

export ARCH=arm64
export CROSS_COMPILE=aarch64-linux-android-
make your_defconfig
make -j$(nproc)

> You’ll get a Image.gz-dtb which can be packed into boot.img




---

🔄 Repack Boot with Custom Kernel

You can use:

AIK (Android Image Kitchen)

MagiskBoot

mkbootimg/unmkbootimg


Replace only the kernel binary:

boot.img-zImage or kernel = Image.gz-dtb

Then repack and flash:

fastboot flash boot new_boot.img


---

🧪 Troubleshooting Kernel Issues

Problem	Likely Fix

No display	Wrong DTB / incompatible framebuffer
Recovery boots, no touch	Missing touchscreen driver in kernel
Bootloop at splash	Mismatched kernel version or wrong config
ROM boots, no Magisk	Patch boot.img again with Magisk



---

✅ Summary

Task	Tool/Method

Flash custom kernel zip	TWRP / Fastboot
Patch kernel with Magisk	Magisk app
Repack kernel into boot	AIK / mkbootimg / CRB Kitchen
Build kernel from source	GCC/Clang toolchain (Linux)



---

> 🧠 The kernel is the heart of Android. If the ROM is fine but won’t boot — always test a different or patched kernel first.



---
