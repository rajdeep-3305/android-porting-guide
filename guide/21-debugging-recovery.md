# 🧯 Debugging TWRP / OrangeFox / Custom Recovery Boot Issues

If your ported TWRP or custom recovery shows a black screen, bootloops, or can’t decrypt data, this guide helps you debug and fix it.

---

## 🧪 Symptoms of Recovery Failure

| Symptom                      | Possible Cause                      |
|------------------------------|--------------------------------------|
| Black screen after boot      | DTB or framebuffer mismatch          |
| Bootloop or fastboot reboot  | Broken ramdisk or invalid kernel     |
| Recovery boots but no touch  | Missing touchscreen driver in DTB    |
| Cannot mount `/data`         | Encryption or fstab problem          |
| Touch is misaligned          | Wrong screen resolution in DTB       |

---

## 🧩 1. Check DTB/DTBO Compatibility

- Use stock recovery's `dtb` or `dtbo.img` when porting
- Replace DTB in `recovery.img` with the stock one:
  ```bash
  unmkbootimg → replace DTB → mkbootimg

> Use tools like AIK, MagiskBoot, or mkbootimg.




---

🛠 2. Fix Touchscreen Issues

Touch not working = usually DTB problem (I2C driver not loading)

Try patching or replacing DTB from stock recovery


> If display works but touch doesn't, 99% chance it's the DTB.




---

📄 3. Patch fstab for Decryption & Mounts

Inside recovery ramdisk:

/vendor/etc/fstab.*

Remove forceencrypt

Add encryptable=footer

Match partition names (/data, /vendor, etc.)


✅ Use OrangeFox or skkk TWRP if official TWRP doesn’t support encryption.


---

🔥 4. Watch Logs During Recovery Boot

From PC (if recovery supports ADB):

adb logcat > recovery_log.txt
adb shell dmesg > recovery_dmesg.txt

Look for:

E/ or F/ errors

init: cannot mount /vendor

touchscreen firmware not found

FBE failed to decrypt



---

🧪 5. Recovery Freezes at Logo?

Likely cause:

Kernel is wrong (from wrong ROM base)

init.rc is broken or missing mount paths

zImage and ramdisk mismatch


✅ Use stock recovery's zImage and patch with your ramdisk


---

✅ Flashing a Debug Build

Flash recovery using:

fastboot flash recovery recovery.img

Or boot directly (for testing):

fastboot boot recovery.img


---

💡 Bonus: Force Logging on Early Boot

Add this line to default.prop or init.rc in ramdisk:

logcatd.start=1

It may help capture logs even before touch/display appears.


---

✅ Summary

Problem	Likely Fix

Black screen	Replace DTB from stock
No touch	DTB or missing touchscreen config
Bootloop on flash	Use correct kernel/zImage
/data not mounting	Patch fstab + disable encryption
No logs / no ADB	Enable debugging props in ramdisk



---

> 🛠 A working custom recovery is your #1 tool for ROM and GSI testing — fix it once, and debugging becomes 10× easier.



---
