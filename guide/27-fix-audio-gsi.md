# 🔊 Fixing No Audio / Mic / Speaker in GSIs or Ported ROMs

Flashing a custom ROM or GSI and getting **no sound**, **no mic**, or **broken calls**?  
This is usually due to missing or incompatible **audio HAL**, **mixer paths**, or **permission issues**.

Here’s how to fix it step by step.

---

## 🧪 Common Symptoms

| Symptom                      | Likely Cause                        |
|------------------------------|-------------------------------------|
| No speaker or earpiece sound | Wrong or missing `mixer_paths.xml` |
| Mic doesn’t work             | HAL/service blocked or denied       |
| No audio in calls only       | Audio policy or telephony service   |
| Media plays but silent       | Audio device routing fails          |

---

## ✅ Step 1: Pull Stock Audio Files

From your stock ROM (vendor partition or firmware dump), extract:

/vendor/etc/audio/ ├── audio_policy.conf ├── audio_policy_configuration.xml ├── mixer_paths.xml ├── mixer_paths_tavil.xml ├── audio_platform_info.xml

And HALs:

/vendor/lib*/hw/audio.primary.* /vendor/lib*/libaudio*.so

---

## ✅ Step 2: Add Files via Magisk Module

Create a module with:

system/ └── vendor/ ├── etc/audio/ ├── lib/ └── lib64/

Be sure:
- Permissions = `0644`
- Ownership = `root:root`

> See [Guide 23] for full Magisk module instructions.

---

## ✅ Step 3: Fix Permissions and Contexts

Push and fix permissions:

```bash
adb shell
su
chmod 0644 /vendor/etc/audio/*.xml
restorecon -v /vendor/etc/audio/

Also for HALs:

chmod 0644 /vendor/lib*/hw/audio.primary.*
restorecon -v /vendor/lib*/hw/


---

✅ Step 4: Debug with Logcat

adb logcat | grep -i audio

Look for:

audio_hw_primary: open failed

mixer: error opening devices

avc: denied (means SELinux blocked it)



---

✅ Step 5: Enable Debugging Props (Optional)

Set via Magisk or default.prop:

persist.audio.fluence.voicecall=true
persist.audio.fluence.speaker=true
persist.audio.fluence.voicecomm=true
persist.audio.fluence.mode=endfire

> May improve voice routing or echo.




---

🔧 Bonus: Fix Call Audio Only (VoIP or Telephony)

1. Flash vendor fix modules like GSI Audio Fix, or


2. Use audio_policy_configuration.xml from stock that includes:



<stream type="voice_call" />
<stream type="voip_call" />


---

✅ Summary

Task	Tool / Method

Restore audio HALs	From stock /vendor/lib*/hw
Add mixer paths/configs	/vendor/etc/audio/
Fix permissions	chmod + restorecon
Debug issues	`adb logcat
Systemless patching	Magisk module



---

> 🔊 Most GSI audio issues can be fixed by borrowing stock audio configs and HALs — always test via both media and call.



---
