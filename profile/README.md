<p align="center">
  <img src="https://raw.githubusercontent.com/PocoF3Releases-Recovery/.github/main/profile/assets/recovery-banner.png" alt="PocoF3Releases Recovery — native Android 17 recovery" width="100%" />
</p>

# Android 17 recovery for POCO F3

[ROM sources](https://github.com/PocoF3Releases) · [Build integration](https://github.com/PocoF3Releases-Recovery/local_manifests) · [All repositories](https://github.com/orgs/PocoF3Releases-Recovery/repositories) · [Telegram](https://t.me/PocoF3_Updates)


Native Evolution X recovery enhancements for Alioth: internal-storage unlocking, local OTA/recovery ZIP installation, guarded boot-image installation, touch credential entry, Magisk/APatch installers and recovery-only crypto dependencies. Standalone PBRP is a separate project.

## Native ROM recovery

These repositories use **`cnb`**. Sync the [local manifests](https://github.com/PocoF3Releases-Recovery/local_manifests/tree/cnb) to include their build and crypto dependencies. Native ROM recovery is separate from PBRP.

| Role | Repository |
| --- | --- |
| Recovery UI and installation | [android_bootable_recovery](https://github.com/PocoF3Releases-Recovery/android_bootable_recovery) |
| Storage decryption | [android_system_vold](https://github.com/PocoF3Releases-Recovery/android_system_vold) |
| SELinux policy | [android_system_sepolicy](https://github.com/PocoF3Releases-Recovery/android_system_sepolicy) |
| Build integration | [android_build](https://github.com/PocoF3Releases-Recovery/android_build) |

<details>
<summary>Recovery dependency repositories — cnb</summary>

| Role | Repositories |
| --- | --- |
| Keystore | [security](https://github.com/PocoF3Releases-Recovery/android_system_security) |
| Vendor policy | [legacy-um](https://github.com/PocoF3Releases-Recovery/android_device_qcom_sepolicy_vndr_legacy-um) |
| HAL interfaces | [hardware/interfaces](https://github.com/PocoF3Releases-Recovery/android_hardware_interfaces) · [system/hardware/interfaces](https://github.com/PocoF3Releases-Recovery/android_system_hardware_interfaces) |
| HIDL and VINTF | [hwservicemanager](https://github.com/PocoF3Releases-Recovery/android_system_hwservicemanager) · [libhidl](https://github.com/PocoF3Releases-Recovery/android_system_libhidl) · [libvintf](https://github.com/PocoF3Releases-Recovery/android_system_libvintf) |
| Crypto | [keymaster](https://github.com/PocoF3Releases-Recovery/android_system_keymaster) · [libcppbor](https://github.com/PocoF3Releases-Recovery/android_system_libcppbor) · [BoringSSL](https://github.com/PocoF3Releases-Recovery/android_external_boringssl) |
| Rust | [Android crates](https://github.com/PocoF3Releases-Recovery/android_external_rust_android-crates-io) · [cxx](https://github.com/PocoF3Releases-Recovery/android_external_rust_cxx) · [librustutils](https://github.com/PocoF3Releases-Recovery/android_system_librustutils) |
| Data and logging | [SQLite](https://github.com/PocoF3Releases-Recovery/android_external_sqlite) · [libselinux](https://github.com/PocoF3Releases-Recovery/android_external_selinux) · [logging](https://github.com/PocoF3Releases-Recovery/android_system_logging) |
| Platform libraries | [APEX](https://github.com/PocoF3Releases-Recovery/android_system_apex) · [incfs](https://github.com/PocoF3Releases-Recovery/android_system_incremental_delivery) · [flags](https://github.com/PocoF3Releases-Recovery/android_system_server_configurable_flags) · [AIDL](https://github.com/PocoF3Releases-Recovery/android_system_tools_aidl) · [libhardware_legacy](https://github.com/PocoF3Releases-Recovery/android_hardware_libhardware_legacy) |
| Filesystem tools | [extras](https://github.com/PocoF3Releases-Recovery/android_system_extras) · [NTFS](https://github.com/PocoF3Releases-Recovery/android_external_ntfs-3g) · [bzip2](https://github.com/PocoF3Releases-Recovery/android_external_bzip2) |

Recovery additions to the shared device trees and `frameworks_base` are distributed as patches against the ROM sources. Evolution-X and LineageOS forks retain their upstream relationships; dependencies from other mirror owners are standalone repositories with their original history.

</details>

## Shared ROM bases, small patch stack

Use the normal **PocoF3Releases** framework and device repositories. Recovery adds
four authored patches through the [manifest repository](https://github.com/PocoF3Releases-Recovery/local_manifests#readme), without duplicating the shared forks.

```sh
repo sync -j50
python3 .repo/local_manifests/apply-recovery-patches.py --check
python3 .repo/local_manifests/apply-recovery-patches.py
```

For a release build:

```sh
. build/envsetup.sh
lunch lineage_alioth-cp2a-user
m installclean
m evolution
```

For incremental development, omit `m installclean`. The runner checks every project
before applying changes, preserves authorship and skips an already-applied stack.

[Verification and limits](https://github.com/PocoF3Releases/Agents.md/blob/main/memory/evox-recovery.md) · [Organization logo](assets/recovery-logo.png)
