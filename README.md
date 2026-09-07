# NOS-microg

Root module for replacing Google applications on stock Android 11-17 with open-source alternative.

## Install

0. Turn on ADB for fixing crashing in bootloop case [check troubleshooting](#bootloop)
1. Download latest version from [releases](https://github.com/vladislav1947/NOS-microg/releases)
    - Or build it yourself
2. Install through Magisk or KSU
3. Reboot
4. In Magisk/KSU click "Action" button next to module to grant permissions
    - Or open microG app and grant them through Self-Check
5. Ensure all permission boxes are checked in Self-Check
    - If not, tap them to set the correct option
6. Check signature spoofing status at the top
    - If your ROM doesn't support signature spoofing, you must add it: [check troubleshooting](#signatures-are-not-correct)
7. If you have issues with microG crashing, install microG as user apps: [check troubleshooting](#microg-crashing)
    - You can do it quickly using `scripts/install-user-apks.sh`

## Build

1. Install `zip`, `curl`, `jq` if not present
2. [Download APKs manually](https://microg.org/download.html) and place in `apk/` directory
3. Run `scripts/build-noogle-microg.sh`
    - Check `-h` flag for help with build options
    - Module will be created in `dist/`
4. Or run `scripts/install-noogle.sh` to build and install through ADB

## Tested


## Troubleshooting

### Signatures are not correct
In order for microG apps to have the correct signatures visible by Android, your ROM must allow for [signature spoofing](https://github.com/microg/GmsCore/wiki/Signature-Spoofing). If it does not (like any stock Android), this is the way I recommend:

1. Enable Zygisk implementation in Magisk/KSU 's settings
2. Download and install LSPosed through Magisk
    - [JingMatrix fork](https://github.com/JingMatrix/LSPosed/releases) up to Android 16
    - Any other verified implementation
3. Download and install [FakeGApps](https://github.com/whew-inc/FakeGApps/releases) APK
4. Reboot
5. Open LSPosed from notifications and enable FakeGapps module
    - Leave default System Framework selected only
6. Reboot
7. Check in microG Self-Check if signatures are correct now

### microG crashing
If you want to use other modules interacting with microG, like Play Integrity Fix on top of this module, it's necessary to install both microG Services and microG Companion (same APKs as in this module, from [official site](https://microg.org/download.html)) on top, as user updates. Then Play Integrity Fix will work properly. In the future this workaround may be not necessary.

### Bootloop
In this case if you have ADB debugging enabled just connect your phone to PC and run `scripts/disable-noogle.sh` in terminal. It will disable Noogle microG module and reboot your device.

If you don't have ADB enabled, you may try to restart the device a few times (holding Power + Vol-) while keeping Vol- for a while until animalted boot animation will start. This will trigger Magisk safe mode and modules will be disabled. More about this in [official documentation](https://topjohnwu.github.io/Magisk/faq.html).

## QA
- Q: What is the difference between this and other microG installers?
- A: This module aims for stock Android support with Google apps preinstalled and doesn't require debloating Google apps first. Should work on AOSP-based as well.
