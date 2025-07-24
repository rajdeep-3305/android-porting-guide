# ✅ Port Result: Redmi Note 8 Pro (MT6785)

| Feature     | Status | Notes                                           |
|-------------|--------|--------------------------------------------------|
| Boot        | ✅      | Needed permissive + signed boot.img             |
| Wi-Fi       | ✅      | Injected `qcom_cfg.ini` from stock vendor       |
| Audio       | ⚠️      | No in-call audio — patched `audio_policy.conf`  |
| Camera      | ❌      | Lib mismatch, needed HAL wrapper                |
| Touch       | ✅      | Stock dtbo worked                               |
| RIL         | ✅      | With custom modemconfig                         |
| SELinux     | Permissive | Needed to avoid early boot crash            |
