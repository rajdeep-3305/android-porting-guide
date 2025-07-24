# 🔐 Fixing Permissions and SELinux Issues in Custom ROMs and GSIs

If your GSI or ported ROM boots but critical services (camera, Wi-Fi, RIL) don’t work — it might not be a HAL issue, but **permissions or SELinux denials**.

This guide helps you fix:
- `Permission denied` errors in logcat
- SELinux blocking system components
- Apps failing to access protected hardware

---

## 🧪 Identify SELinux or Permission Issues

Use `logcat`:
```bash
adb logcat | grep denied

Typical output:

avc: denied { read write } for path="/dev/binder" dev="tmpfs" ...
avc: denied { connect } for pid=892 ...

This means SELinux blocked access.


---

✅ Step 1: Switch to Permissive Mode (Testing Only)

A. Temp (runtime):

adb shell setenforce 0

B. Permanent (via Magisk):

Create a Magisk module with service.sh:

#!/system/bin/sh
setenforce 0

✅ This disables SELinux enforcement — only for testing/debugging.


---

✅ Step 2: Patch File & Folder Permissions

Incorrect file ownership and mode can break things even with permissive SELinux.

Common Fixes:

chown system:system /data
chmod 0771 /data

chown media_rw:media_rw /data/media/0
chmod 0770 /data/media/0

chown root:root /system/lib64/libwifi-hal.so
chmod 0644 /system/lib64/libwifi-hal.so


---

✅ Step 3: Patch sepolicy.rule (Advanced, for Enforcing Mode)

Use tools like:

Magisk Policy Patch Module

magisk --sepolicy-inject (CLI)

SuperSu SEPolicy Modifier (deprecated)


Example custom rule:

allow hal_wifi_default system_file:dir search;
allow hal_camera_default camera_device:chr_file { read write open };

Place into:

/data/adb/modules/<yourmodule>/sepolicy.rule


---

✅ Step 4: Fix init.rc or uevent Permission Issues

Inside /vendor/etc/ueventd.rc or init.*.rc, ensure:

/dev/xyz      0660  system system
/dev/binder   0666  root   root

And in fstab:

/data ext4 ... context=u:object_r:system_data_file:s0


---

🧪 Tips to Debug SELinux

Command	Use

adb shell getenforce	Check SELinux state
`adb logcat	grep avc`
ls -Z	Show SELinux context of files
restorecon -v /your/path	Restore correct context



---

✅ Summary

Fix Task	Tool or Method

Permission denied	setenforce 0 + proper chmod
File unreadable	chown, chmod, restorecon
Persistent permissive mode	Magisk module → service.sh
Enforcing mode sepolicy patch	sepolicy.rule in Magisk



---

> 🧠 SELinux and permission bugs are silent killers in GSIs — a working HAL or lib may still get blocked without proper policies or access rights.



---
