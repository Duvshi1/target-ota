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
| V1.02.09-20260828 | V1.02.02-20260521 | `UI1215_2026.08.26.rar` |

## Manifests

The on-device `FotaUpdater` app (`com.imotor.ota`) makes two separate HTTP
calls, not one — confirmed by decompiling `FotaUpdater.apk`:

- `CheckUpgradeTask` hits a "check" endpoint first. The response tells the
  client whether an update exists, but never carries a download URL.
- Only if that says an update is available does `DownloadUpgradeFileTask`
  make a second, separate call to a "download" endpoint — that response
  repeats the same fields *plus* `Download_link`, which is what's actually
  used to fetch the file.

`check.json` and `download.json` in this repo mirror those two response
shapes exactly (field names match the `@SerializedName` annotations found in
the decompiled `UpgradeInfo`/`AvailableInfo` classes). Raw URLs to hand the
supplier for registering this release:

- Check: `https://raw.githubusercontent.com/Duvshi1/target-ota/main/check.json`
- Download: `https://raw.githubusercontent.com/Duvshi1/target-ota/main/download.json`
