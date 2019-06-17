# Fork for Nexus 5 (hammerhead) by Denir
The latest version of halium and pm-rootfs doesn't boot normally on Nexus 5 (hammerhead), so I try to downgrade to the old version of halium and pm-rootfs to resolve boot loop issue and rootfs load issue. After testing, the last combination that can be booted normally is as follows:
1. halium (20170623-085147) boot.img: https://images.plasma-mobile.org/halium/hammerhead/20170623-085147/boot.img
2. halium (20181029-111411) system.img: https://images.plasma-mobile.org/halium/hammerhead/20181029-111411/system.img
3. pm-rootfs-20180524-110808: https://images.plasma-mobile.org/legacy-rootfs/pm-rootfs-20180524-110808.tar.gz

# pm-flashtool
Tool for Flashing CM+PM as LXC Container

# Typical workflow.. (How it works)

- Waits for device to be in fastboot mode,
- Downloads twrp recovery and flashes into recovery
- Boots into recovery
- Downloads cm.zip and pushes it to /cache
- Creates command file with
```
--update_package=/sdcard/cm.zip
```
- pushes it to /cache/recovery/command
- Reboots into recovery
- recovery installs cm.zip
- reboots in system
- Installs lxc and plasma rootfs

# Howto use

To run..

```
git clone https://github.com/denir-li/pm-flashtool.git
cd pm-flashtool
./pm-flash_20170623.sh
```

Without options pm-flash script downloads all files again, pass '-c' to let it use cache instead

```
./pm-flash_20170623.sh -c
```

This

a) Downloads the files required in ~/.cache/plasmaphone
b) Flashes cyanogenmod
c) Puts togather lxc and plasma rootfs

After that you can run

```
adb root
adb shell
lxc-start -n system -F
```

to get login console and plasma started

Multirom version
----------------
See instructions here : https://community.kde.org/Plasma/Mobile/CyanogenModBase#MultiROM_instructions_.28For_dualboot.29
