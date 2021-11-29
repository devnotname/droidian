# Droidian | Debian GNU/Linux 11.1


## What works and what doesn't
- Currently Droidian is in an experimental state, no bug list is created. Read the [Notes](#notes) section for more info.


## Requirements

- Android 10 firmware for your device:
  - Redmi Note 9 Pro joyeuse: [LINK](https://xiaomifirmwareupdater.com/archive/miui/joyeuse/)
  - Redmi Note 9s/9 Pro India curtana: [LINK](https://xiaomifirmwareupdater.com/archive/miui/curtana)
  - Redmi Note 9 Pro Max excalibur: [LINK](https://xiaomifirmwareupdater.com/archive/miui/excalibur/)
  - POCO M2 Pro gram: [LINK](https://xiaomifirmwareupdater.com/archive/miui/gram/)
- Download the latest rootfs:  [droidian-rootfs-api29gsi-arm64-xxxxxxxx.zip](https://github.com/droidian-images/rootfs-api29gsi-all/releases).
- Download the latest devtools: [droidian-devtools-arm64_xxxxxxxx.zip](https://github.com/droidian-images/rootfs-api29gsi-all/releases).
- Download the adaptation for miatoll: [droidian-adaptation-miatoll.zip](https://sourceforge.net/projects/miatoll-linux/files/Droidian/droidian-adaptation-miatoll.zip/download).
- Download [boot.img](https://sourceforge.net/projects/miatoll-linux/files/Droidian/boot.img/download), [dtbo.img](https://sourceforge.net/projects/miatoll-linux/files/Droidian/dtbo.img/download), [vbmeta.img](https://sourceforge.net/projects/miatoll-linux/files/Droidian/vbmeta.img/download).

## Installation
- Flash boot.img: `fastboot flash boot boot.img`.
- Flash dtbo.img: `fastboot flash dtbo dtbo.img`.
- Flash vbmeta.img: `fastboot --disable-verity --disable-verification flash vbmeta vbmeta.img`.
- Flash your favorite recovery.
- Format userdata as ext4 from inside the recovery or via fastboot: `fastboot format:ext4 userdata`.

- Sideload droidian-rootfs-api29gsi-arm64-xxxxxxxx.zip.
- Push droidian-devtools-arm64_xxxxxxxx.zip and droidian-adaptation-miatoll.zip to /tmp via `adb push`.
- Adb shell inside your device: `adb shell`.
- `cd /tmp`.
- `mkdir devtools`.
- `unzip -d devtools droidian-devtools*.zip`.
- `mkdir miatoll`.
- `unzip -d miatoll droidian-adaptation-miatoll.zip`.
- `mkdir mpoint`.
- `mount -o loop /data/rootfs.img mpoint` - At this point you should get an error: `mount: '/dev/block/loopX'->'/tmp/mpoint': Block device required`.
- `losetup -d /dev/block/loopX` - Replace X with the number from the error above.
- `losetup /dev/block/loopX  /data/rootfs.img` - Replace X with the number from the error above.
- `mount /dev/block/loopX mpoint` - Replace X with the number from the error above.
- `tar -C /tmp/mpoint -xvf /tmp/devtools/payload.tar`.
- `tar -C /tmp/mpoint -xvf /tmp/miatoll/payload.tar`.
- `reboot`


## Notes

- The default password is `1234`.
- Mobile data needs an APN to be set up from Settings -> Mobile -> Acess Point Names.
- RIL gets broken after switching airplane mode or modem off/on.
- Mobile data might stop working after making or recieving phone calls. Toggle Mobile Data from the settins off/on.
- Mobile data quick toggle doesn't work.
- Not every app will work as they might need aditional packages (eg: Telegram Desktop needs qtwayland5 to be installed to run). Google or [@Droidian](https://t.me/DroidianLinux) is your best friend in this case.
- Automatic app scaling [per app](https://forums.puri.sm/t/librem-5-scale-to-fit/11399/3) or globally: `gsettings set sm.puri.phoc scale-to-fit true`.
- [Tweaks](https://wiki.mobian-project.org/doku.php?id=tweaks).
- [Theming](https://wiki.mobian-project.org/doku.php?id=themes).
- **Droidian GSIs are experimental! Bugs and missing features are expected.**


# Support
- Device specific telegram group: [@ut_miatoll](https://t.me/ut_miatoll).
- Droidian telegram group: [@DroidianLinux](https://t.me/DroidianLinux).