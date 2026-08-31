# target-ota

Firmware release hosting for the Target/UZ708 (`auto_rk_t10`) platform.

The actual OTA check-in/download API is the supplier's own service
(`ota.bpin.online`, package `com.imotor.ota` on-device) — this repo exists
only to host the update binaries themselves as GitHub Release assets, since
the supplier's platform lets a customer register an external download URL
per release rather than uploading the file directly to them.

## Releases

| Build | Base version | Source package |
|---|---|---|
| V1.02.09-20260828 | — | `UI1215_2026.08.26.rar` |
