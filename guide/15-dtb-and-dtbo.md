# 🧬 DTB and DTBO: Kernel Device Tree Basics

The **Device Tree Blob (DTB)** and **Device Tree Blob Overlay (DTBO)** describe hardware configuration to the Linux kernel during boot.  
If your device has no display, no touch, or crashes early, DTB/DTBO is often the reason.

This guide shows how to extract, patch, and repack DTB/DTBO for recovery and ROM boot success.

---

## 🧠 What Is DTB/DTBO?

| Term   | Meaning                            |
|--------|------------------------------------|
| **DTB**  | Base hardware description (SoC, RAM, GPIO, etc.) |
| **DTBO** | Extension overlay (used in A/B or dynamic boot setups) |

They are embedded in `boot.img` or exist as standalone partitions.

---

## 🔍 How to Know If DTB Is the Problem

- Blank screen after flashing recovery
- Display flickers or freezes
- Touch not working in recovery but works in ROM
- No boot (especially on A/B devices)

---

## 📦 Extracting DTB from `boot.img`

1. Use **AIK** or **Android Boot Image Editor**  
2. Look for a file like:

boot.img-dtb

3. Use `dtc` (Device Tree Compiler) to decompile:

```bash
dtc -I dtb -O dts -o output.dts input.dtb

> You can now read it in plain text (.dts file)




---

🔧 Common DTB Fixes

Display issues: Match panel config from stock DTB

Touch issues: Fix touchscreen I2C/driver lines in DTB

Recovery fails: Merge stock DTB into ported recovery



---

🔄 Replacing DTB in Boot or Recovery

1. Extract boot.img or recovery.img


2. Find DTB file (usually at the end of image)


3. Use mkbootimg or unmkbootimg tools with --dtb flag



mkbootimg --kernel zImage --ramdisk ramdisk.gz --dtb dtb.img ...

> Some tools like CRB Kitchen support DTB patching automatically.




---

📦 Handling dtbo.img

Some devices have a separate dtbo.img partition.

To extract:

lpmake --extract-dtbo dtbo.img output_dir/

To patch:

Use MagiskBoot or AIK if embedded in boot

Use device-specific tool if standalone


To flash:

fastboot flash dtbo dtbo.img


---

📺 Video References

▶️ How DTB/DTBO Affects ROM Boot
▶️ Fix No Display / Touch by DTB Patch


---

✅ Summary

Action	Tool

Extract DTB	AIK, unmkbootimg, MagiskBoot
Decompile DTB	dtc
Patch DTB	Merge or edit .dts
Repack with new DTB	mkbootimg or kitchen
Handle dtbo.img	lpmake, fastboot flash



---

> 🔧 Mastering DTB/DTBO is key for recovery porting, display/touch fixes, and deep hardware debugging.



---
