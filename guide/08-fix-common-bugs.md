# 🐞 Fix Common Bugs After Porting

After booting a ported ROM or GSI, some essential components may be broken — like Wi-Fi, camera, audio, or cellular.  
Here’s a guide to fixing the most common issues using logs and patching techniques.

---

## 🛠 Tools Required

- **adb**
- **dmesg**
- **logcat**
- **WinMerge**
- Text editor (Notepad++, Sublime, etc.)

---

## 📋 Bug Categories & Fixes

---

### 📡 1. Wi-Fi / Bluetooth Not Working

#### ✅ Fix:
- Check for missing or incorrect `.ko` kernel modules:

/vendor/lib/modules/*.ko

➤ Copy them from your stock vendor or ROM

- Compare `/vendor/etc/init/wifi*` and `bt*` scripts  
- Patch your `init*.rc` files (especially `init.target.rc`)

#### 🧪 Log to check:
```bash
adb logcat | grep -i wlan


---

🎧 2. Audio Not Working

✅ Fix:

Check audio_policy.conf or audio_policy_configuration.xml in:

/vendor/etc/
/system/etc/

Replace with files from stock ROM if empty/missing

Edit build.prop and ensure:

persist.vendor.audio.fluence.voicecall=true
ro.vendor.audio.sdk.fluencetype=fluence


🧪 Log:

adb logcat | grep -i audio


---

📷 3. Camera Crashing or Not Opening

✅ Fix:

Add missing libs:

/vendor/lib*/libcamera*.so
/vendor/lib*/libmmcamera*.so

Copy media_codecs*.xml from stock ROM to:

/system/etc/

Add permissions in:

/vendor/etc/permissions/*.xml


🧪 Log:

adb logcat | grep -i camera


---

📶 4. No SIM / No Network / No RIL

✅ Fix:

Replace stock RIL blobs:

libril.so
libreference-ril.so
libsec-ril.so

Ensure these services exist in:

/vendor/etc/init/*.rc

Match with modem files if required (/vendor/firmware/)


🧪 Log:

adb logcat | grep -i ril


---

📳 5. Vibration Not Working

✅ Fix:

Replace:

/vendor/lib*/hw/vibrator*.so

Ensure vibrator service is declared in init.rc



---

🔒 6. Decryption / Encryption Issues

Handled in more detail in Guide 10.


---

✅ General Steps for Debugging Any Bug

1. Boot ROM


2. Connect device via USB and run:

adb logcat > log.txt
dmesg > dmesg.txt


3. Analyze log.txt and dmesg.txt


4. Identify missing services or errors


5. Compare with stock working logs




---

📘 Tip

Always backup logs from both working and broken ROMs and compare them line by line using tools like WinMerge or Meld.


---

> 🧪 Debug smartly — most bugs can be solved without source code by comparing working and non-working configs.



---
