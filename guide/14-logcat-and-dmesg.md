# 🪵 Using `logcat` & `dmesg` to Debug ROM Boot and Bugs

When a ported ROM or GSI fails to boot, has missing features, or crashes randomly, **logs are your best friend**.  
This guide shows how to capture and analyze `logcat` and `dmesg` to fix almost any Android-side bug.

---

## 🧰 What You’ll Need

- ADB installed on your PC or phone
- USB debugging enabled (if device boots)
- Working recovery or recovery with ADB support (TWRP, OrangeFox, etc.)

---

## 🧪 1. `logcat` — Android Log Output

### When to use:
- Device boots but something crashes (e.g., Wi-Fi, RIL, camera)
- App force closes
- Bootloop stuck at logo

### 📤 Capture `logcat`:

```bash
adb logcat > log.txt

✅ This captures live logs. Start logging before boot for early crash detection.

🔍 Filter for specific modules:

adb logcat | grep -i wifi
adb logcat | grep -i camera
adb logcat | grep -i ril


---

⚙️ 2. dmesg — Kernel Debug Messages

When to use:

Kernel panics

Boot fails before Android UI

Low-level hardware issues


📤 Capture dmesg:

adb shell dmesg > dmesg.txt

Or from recovery:

adb shell su -c dmesg > dmesg.txt


---

🧠 How to Analyze

In logcat:

E/ = Error

F/ = Fatal

W/ = Warning

Look for stack traces (java.lang.RuntimeException)

Crashes usually show:

fatal exception: main
signal 6 (SIGABRT)
signal 11 (SIGSEGV)


In dmesg:

Look for:

init: starting service
SELinux denied
kernel panic
watchdog bite

Missing .ko modules or incorrect DTBs also show up here.



---

📦 Bonus: last_kmsg for Bootloops

If the device rebooted during boot, check last_kmsg:

adb shell su -c "cat /proc/last_kmsg" > kmsg.txt

Works only before next reboot, so capture immediately.


---

🔁 Compare Logs

Best method: compare logs between:

Working stock ROM

Your broken port


Use tools like:

WinMerge (Windows)

Meld (Linux)



---

🧪 Real-World Use Cases

Bug	Log Source	What to Look For

Wi-Fi not working	logcat	WCNSS errors, wlan HAL not starting
Camera crashes	logcat	libcamera, HAL, permission denied
Bootloop	dmesg	kernel panic, init stuck, watchdog
No RIL (SIM)	logcat	ril-daemon, IccCard, radio off
Touch not working	dmesg	input, hid, touch firmware lines



---

✅ Summary

Command	Use Case

adb logcat	Android system/app bugs
adb shell dmesg	Kernel/hardware/boot errors
last_kmsg	Bootloop recovery
grep	Isolate specific error modules



---

> 🔍 Log reading is 90% of ROM porting. If you read logs properly, you can fix almost anything — no sources required.



---
