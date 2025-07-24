# ⚡ Optimize Boot Time, Battery, and Thermal Performance in GSIs & Custom ROMs

After flashing a ROM or GSI, you may notice:
- Long first boot
- Overheating
- Laggy UI
- Fast battery drain

These issues are usually related to:
- Background services
- Logging, debugging tools left enabled
- Improper thermal configs
- Unoptimized kernel settings

This guide helps improve performance without compromising stability.

---

## ⏱️ Speed Up First Boot (or Reboot)

| Task                          | Tip                               |
|-------------------------------|------------------------------------|
| Boot takes 10+ minutes        | Flash clean, **format /data**     |
| `dex2oat` delay               | Avoid GSI builds with preopt disabled |
| System UI lag post-boot       | Wait until media scanner finishes |

Optional: Add boot-time logger to `logcat`:
```bash
adb logcat -b all > bootlog.txt


---

🔋 Reduce Battery Drain

1. Disable Logging

Disable logd, logcat, or verbose debugging:

setprop log.tag.* SUPPRESS

Or add to post-fs-data.sh in Magisk:

#!/system/bin/sh
stop logd


---

2. Remove Junk Apps or Services

Freeze or uninstall:

Google Partner Setup

Feedback apps

Analytics and crash reporting


Via Magisk:

pm disable-user com.google.android.feedback


---

3. Use Better Thermal Profiles

From /vendor/etc/thermal-engine*.conf or /vendor/etc/.tp/

Common tuning:

Lower target temps

Reduce throttling delay

Increase cooldown ramp


Be careful not to disable thermal limits entirely on hot chips (e.g. SD680, Helio G series)


---

❄️ Use Custom Kernel Tweaks

If using custom kernel (or ported):

Use EXKM, HKTweaks, or FrancoKernel Manager

Disable unused CPUs via hotplug

Undervolt if supported

Set I/O scheduler to noop or maple


> Be sure your kernel supports tweaking or exposes /sys/devices/system/cpu/




---

📊 Useful Debug Commands

top -n 1
cat /proc/stat
cat /proc/cmdline
dumpsys battery


---

🛠 Optional Tools

Tool	Use

Naptime	Force Doze on demand
LKT/MK Tweaks	Battery-friendly sysctl tuners (via Magisk)
Magisk Debloater	Disable bloatware systemlessly
Thermal Editor	OneUI-based thermal manager



---

✅ Summary

Problem	Fix

Long boot	Clean flash + format /data
Lag / heat	Thermal tweaks + less logging
Drain at idle	Kill analytics/logging, enable doze
Reboot = slow UI	GSI dex2oat → allow full settle time



---

> ⚙️ Once a ROM or GSI is stable, optimizing thermal + logging + battery can make it feel like a daily driver — not just a test build!



---
