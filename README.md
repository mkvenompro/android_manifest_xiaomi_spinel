# Redmi Note 15 4G (spinel) — Local Manifest

Local manifest for building LineageOS 23 (Android 15) for the Redmi Note 15 4G (spinel) / MediaTek MT6789 (Helio G100 Ultra).

## Usage

1. Initialize a LineageOS 23.2 tree:

   ```bash
   repo init -u https://github.com/LineageOS/android.git -b lineage-23.2
   ```

2. Add this local manifest:

   ```bash
   mkdir -p .repo/local_manifests
   curl -o .repo/local_manifests/roomservice.xml \
     https://raw.githubusercontent.com/mkvenompro/android_manifest_xiaomi_spinel/main/local_manifest.xml
   ```

3. Sync and build:

   ```bash
   repo sync -c -j$(nproc --all)
   source build/envsetup.sh
   lunch lineage_spinel-userdebug
   mka bacon -j$(nproc --all)
   ```

## Included projects

| Project | Path | Branch |
|---|---|---|
| `mkvenompro/android_device_xiaomi_spinel` | `device/xiaomi/spinel` | `lineage-23.2` |
| `mkvenompro/android_device_xiaomi_spinel-kernel` | `device/xiaomi/spinel-kernel` | `lineage-23.2` |
| `mkvenompro/proprietary_vendor_xiaomi_spinel` | `vendor/xiaomi/spinel` | `lineage-23.2` |
| `LineageOS/android_hardware_mediatek` | `hardware/mediatek` | `lineage-23.2` |
| `LineageOS/android_device_mediatek_sepolicy_vndr` | `device/mediatek/sepolicy_vndr` | `lineage-23.2` |
| `LineageOS/android_hardware_xiaomi` | `hardware/xiaomi` | `lineage-23.2` |
| `LineageOS/android_hardware_lineage_compat` | `hardware/lineage/compat` | `lineage-23.2` |
| `mkvenompro/lineage_vendor_keys` | `vendor/private/keys` | `main` |

## Notes

- `hardware/google/interfaces`, `hardware/google/pixel`, and `hardware/lineage` dependencies are provided by the main LineageOS manifest — no need to add them here.
- `hardware/mediatek/libmtkperf_client`, `libaedv`, and `wlan/wifi_hal` are part of the `LineageOS/android_hardware_mediatek` repository.
- Signing keys are synced to `vendor/private/keys` to match `device.mk` (`vendor/private/keys/keys.mk`).
- Optional: `vendor/mediatek/ims` is not included; add a project for it if you want MTK IMS support.
