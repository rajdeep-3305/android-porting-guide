# 🔁 Fixing Bootloop on Reboot (ROM Boots Once Then Fails)

Some custom ROMs or GSIs boot fine the first time — but **bootloop, freeze, or crash** after a reboot.  
This is often caused by:
- Encryption issues
- SELinux problems
- `post-fs` scripts
- Dirty `data` partition
- Magisk or DFE misbehaving

This guide helps fix persistent reboot issues.

---

## 🧪 Common Symptoms

| Symptom                       | Likely Cause                  |
|-------------------------------|-------------------------------|
| ROM boots first time only     | `forceencrypt`, missing DFE   |
| Reboot = stuck at logo        | FBE encryption enabled        |
| Magisk breaks on reboot       | Module misbehaving            |
| Internal storage 0MB after reboot | Encrypted data not decrypted |

---

## ✅ Fix #1: Patch DFE / Disable Encryption

If device supports FBE (File-Based Encryption), and ROM does not decrypt it correctly on second boot, you’ll bootloop.

### Options:

#### A. Flash DFE Zip (Disable Force Encrypt)

- Use a DFE `.zip` from trusted source
- Flash after ROM install
- Reboot to recovery once before system

#### B. Patch `fstab` in vendor:

Edit:

/vendor/etc/fstab.*

Change:
```fstab
/data ext4 ... forceencrypt

To:

/data ext4 ... encryptable=footer

Then repack and flash boot.img or vendor.img.


---

✅ Fix #2: Format Data Properly

In recovery:

1. Wipe → Format Data (not just wipe cache/data)


2. Reboot to recovery again


3. Flash ROM + DFE + Magisk if needed



> ⚠️ Rebooting recovery after formatting is critical to avoid encryption fallback.




---

✅ Fix #3: Magisk Troubleshooting

If you're using Magisk:

Patch with latest stable version

Avoid modules that write to /data/adb

Use logcat to catch crash on boot:


adb logcat -d > log.txt

Disable all modules temporarily:

adb shell magisk --remove-modules


---

✅ Fix #4: Boot Script Conflicts

Some GSIs or ROMs include broken scripts in:

/system/bin/init.rc
/vendor/bin/init.*
/system/bin/post-fs-data

Look for:

chmod, mount, or resetprop calls

SELinux denials in logcat


Try replacing scripts with stock equivalents if broken.


---

✅ Fix #5: Permissions & Ownership

Make sure these have correct perms:

Path	Perms/Owner

/data	0771 / system
/data/media/0	0770 / media_rw
/data/adb/modules	0755 / root


Use:

chown system:system /data
chmod 0771 /data


---

🛠 Bonus: Persistent Logs on Reboot

Add this to default.prop or via Magisk post-fs-data.sh:

logcatd.start=1

This helps capture logs even on boot loops.


---

✅ Summary

Problem	Fix

Boot OK once, loop on reboot	Flash DFE or patch fstab
Internal storage 0MB	Format /data + disable encryption
Magisk breaks reboot	Remove conflicting modules
ROM flashes but can't reboot	Mount props / post-fs issues



---

> 🔁 A reboot bootloop is nearly always related to /data, encryption, or SELinux — patch smart, and test before reboot!



---
