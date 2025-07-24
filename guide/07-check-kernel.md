# 🧠 Check If Kernel is ARM32 or ARM64

Before you port or flash a ROM/GSI, it's important to confirm if your device is using a **32-bit or 64-bit kernel**.  
Even if your device supports 64-bit userspace, the **kernel architecture** matters most for compatibility.

---

## 🧩 What’s the Difference?

| Term         | Meaning                                   |
|--------------|-------------------------------------------|
| **ARM32**    | 32-bit kernel (cannot run 64-bit GSIs)    |
| **ARM64**    | 64-bit kernel (can run 64-bit GSIs/apps)  |

---

## 🛠 How to Check Architecture (3 Methods)

---

### ✅ Method 1: Use Boot Image

1. Extract `boot.img` using **Android Image Kitchen (AIK)**
2. Open `config.gz` (inside `ramdisk` or `split_img`)
3. Search for these lines:

CONFIG_ARM64=y CONFIG_64BIT=y

> 🔍 If both are present: it’s **ARM64 kernel**

If not:

CONFIG_ARM64 is not set

CONFIG_32BIT=y

> ⚠️ Then it's **ARM32 kernel**

---

### ✅ Method 2: Check from Recovery Terminal

In TWRP or any custom recovery with terminal:

```bash
uname -m

Output: aarch64 → 64-bit kernel

Output: armv7l or arm → 32-bit kernel



---

✅ Method 3: Use ADB

If the device is booted:

adb shell uname -m

Same outputs:

aarch64 = ARM64

armv7l or armhf = ARM32



---

🧠 Why This Matters

Task	Kernel Needed

Flashing 64-bit GSI	ARM64 only
Installing 64-bit Magisk modules	ARM64 only
Running 64-bit apps	ARM64 only



---

🚫 Don’t Be Fooled

Even if your device CPU is ARM64, the stock ROM may use an ARM32 kernel (especially in low-end devices like early Galaxy M series, MTK phones, etc.).


---

✅ What If I Want to Upgrade to 64-bit?

To move from ARM32 to ARM64 kernel:

You need a 64-bit kernel source for your SoC

Compile or find a 64-bit boot.img compatible with your vendor

Match kernel version and DTB with your device’s bootloader



---

> ⚠️ Flashing a 64-bit GSI on an ARM32 kernel will result in boot failure or crash loops.



---
