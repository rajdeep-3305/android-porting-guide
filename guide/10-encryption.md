# 🔒 Encryption, Decryption & Forced Encryption Fixes

Many modern Android devices ship with **File-Based Encryption (FBE)** or **Full Disk Encryption (FDE)** enabled by default.  
If your custom ROM or recovery can’t decrypt `/data`, or you get bootloops after formatting, this guide is for you.

---

## 🧠 Types of Encryption

| Type | Description                  |
|------|------------------------------|
| **FDE** | Full disk encryption (older) |
| **FBE** | File-based encryption (newer) |

FBE devices typically use a directory structure like:

/data/system/ce /data/system/de

---

## 🧪 Symptoms of Encryption Issues

- ROM boots, but you can't access internal storage  
- Recovery says `/data` is encrypted  
- Bootloop after wiping `/data`  
- Format succeeds but ROM won’t boot

---

## 🔧 Solutions

---

### ✅ Method 1: Use a Decrypting Recovery

Some custom recoveries can decrypt `/data` on FBE devices:

- Use **latest TWRP**, **OrangeFox**, or **skkk recovery**  
- Ensure **recovery supports your device’s encryption method**

> If recovery fails to decrypt, format `/data` → reboot to recovery → then flash ROM

---

### ✅ Method 2: Format Data Properly

From recovery:
1. Format `/data` via **FORMAT DATA** (not just wipe)
2. Reboot recovery once
3. Then flash ROM/GSI

This ensures proper remount and avoids encryption-related bootloops.

---

### ✅ Method 3: Patch `fstab` to Disable Encryption

Inside `vendor/etc/fstab*`, look for lines like:

/data ext4 ...

Add or modify flags:

encryptable=footer forceencrypt=footer

🧨 To disable encryption completely:
```bash
remove forceencrypt
add: encryptable=footer


---

✅ Method 4: Use DFE or Forcedecrypt Zip

Flash a DFE (Disable Force Encryption) zip after flashing your ROM:

Examples:

Universal DFE ZIP (XDA)

OrangeFox built-in DFE toggle (Settings → DFE)



---

🛠 Extra Tweaks

Add ro.crypto.state=unencrypted to build.prop

Add ro.crypto.type=none to force no encryption

Remove /system/bin/init*encryption* scripts if present (advanced)



---

⚠️ Warnings

Disabling encryption reduces data security

On Android 12+, forced encryption is harder to bypass

Don’t remove encryption blobs unless you're sure



---

✅ Summary

Action	Tool/Step

Recovery can't decrypt	Use decrypt-capable recovery
Want to disable encryption	Use DFE or edit fstab
Data format issue	Use Format Data, not wipe
Advanced fix	Patch build.prop + fstab



---

> 🔐 Encryption is device- and Android-version-specific. Always test thoroughly after disabling it.



---
