title: MIUI sd
id: 1262
categories:
  - Android
date: 2014-06-23 14:23:17
tags:
  - MIUI
---

## Vold 2.0 Generic fstab
## - San Mehat (san@android.com)
##

#######################
## Regular device mount
##
## Format: dev_mount <label> &lt;mount_point&gt; &lt;sysfs_path1...&gt;
## label - Label for the volume
## mount_point - Where the volume will be mounted
## part - Partition # (1 based), or 'auto' for first usable partition.
## &lt;sysfs_path&gt; - List of sysfs paths to source devices
######################</label>

## Example of a standard sdcard mount for the emulator / Dream
# Mounts the first usable partition of the specified device
dev_mount sdcard /storage/sdcard1 emmc@fat /devices/platform/goldfish_mmc.0 /devices/platform/mtk-msdc.0/mmc_host
dev_mount sdcard2 /storage/sdcard0 auto /devices/platform/goldfish_mmc.1 /devices/platform/mtk-msdc.1/mmc_host
## Example of a dual card setup
# dev_mount left_sdcard /mnt/sdcard1 auto /devices/platform/goldfish_mmc.0 /devices/platform/mtk-sd.0/mmc_host/mmc0
# dev_mount right_sdcard /mnt/sdcard2 auto /devices/platform/goldfish_mmc.1 /devices/platform/mtk-sd.2/mmc_host/mmc2

## Example of specifying a specific partition for mounts
# dev_mount sdcard /mnt/sdcard 2 /devices/platform/goldfish_mmc.0 /devices/platform/msm_sdcc.2/mmc_host/mmc1

# usb otg disk
dev_mount usbotg /mnt/usbotg auto /devices/platform/mt_usb /devices/platform/musbfsh_hdrc