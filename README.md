# Fastbootx & Switch-OS Magisk Module

## Overview
This Magisk module provides utilities for efficient management of Android boot partitions directly on the device (without a PC, but root rights are required). It includes the `fastbootx` script (the suffix -x is because there was another [fastboot](https://github.com/Magisk-Modules-Repo/adb-ndk) module) for flashing partitions and more, as well as the `switch-os` script for quickly switching between different OS images (simply quick flashing of .img files stored at /data/adb/boot/[partition] osname.img by the specified osname). The module has added `bootctl` for managing active Android slots.

It's important to note that there may be errors that I'm not yet aware of. Some parts of this module, including manuals and this README file, were generated by a neural network. Please be careful when using these functions.

***Proceed at your own risk. I am not responsible for any adverse outcomes.***

## Features
- **fastbootx**: A script for flashing partitions and performing related operations.
- **switch-os**: A script for rapidly switching between different OS images, including flashing a group of images and changing the active boot slot.

## Installation
1. Download the module ZIP file.
2. Open the Magisk Manager app on your Android device.
3. Tap on the "Modules" section.
4. Tap on the "+" button and select the downloaded ZIP file.
5. Wait for the installation to complete and reboot your device.

## Usage
## fastbootx

```
Usage: fastbootx [COMMAND] ...
Available commands:
    flash or -f:      Writes an image to the specified partition.
    erase or -e:      Erases a partition.
    backup or -b:     Creates a backup of a partition.
    slot or -s:       Sets the active boot slot.
    bootctl or -bc:   Executes the bootctl command with specified arguments.
    partitions, parts or -ps: Displays a list of partitions.
    partition, part or -p:    Displays information about a partition.

Example:
fastbootx flash boot -b backup.img boot.img
```
### fastbootx flash
```
Usage: fastbootx flash [PARTITION] [OPTIONS] [FILE]

Available options:
    -b backup_file_path:             Creates a backup of the flashed partition at the specified backup_file_path.
    -o:                                 Flashes the image to the opposite slot (if slots are used).
    -y:                                 Confirms the operation without prompting.
    -r:                                 Reboots after flashing the image.

Example:
fastbootx flash boot -b backup.img -o -y boot.img
```
### fastbootx erase
```
Usage: fastbootx erase [PARTITION] [OPTIONS]

Available options:
    -b backup_file_path:             Creates a backup of the erased partition at the specified backup_file_path.
    -o:                                 Erases the partition on the opposite slot (if slots are used).
    -y:                                 Confirms the operation without prompting.
    -r:                                 Reboots after erasing the partition.

Example:
fastbootx erase dtbo -oyrb backup_dtbo.img
```
### fastbootx backup
```
Usage: fastbootx backup [PARTITION] [OPTIONS] [FILE]

Available options:
    -o:                                 Creates a backup of the partition in the opposite slot (if slots are used).
    -y:                                 Confirms the operation without prompting.
    -r:                                 Reboots after creating the backup.

Example:
fastbootx backup boot -oy backup.img
```
### fastbootx slot
```
Usage: fastbootx slot [OPTIONS] [SLOT]

Available values for SLOT:
        number - prints the slot number (0 or 1).
        suffix - prints the slot suffix (_a or _b).
        other - activates the opposite slot.
        0 or 1 - slot number to activate.
Available options:
    -o:                                 Switches to the opposite slot.
    -p:                                 Prints a message about the current slot.
    -y:                                 Confirms the operation without prompting.
    -r:                                 Reboots after changing the slot.

Example:
fastbootx slot -y other
```
### fastbootx partition
```
Usage: fastbootx partition [PARTITION] [OPTIONS]

Available options:
    -p, --path:                       Displays the path to the partition.
    or other ls command flags (except -l, which is already used).

Example:
fastbootx partition userdata -p
```
### fastbootx partitions
```
Usage: fastbootx partitions [OPTIONS]

Available options:
    ls command flags.

Example:
fastbootx partitions -a
``` 
## switch-os
```
Usage: switch-os [OPTIONS] [NAME OS]

Available options:
  -h        Display this help message.
  -b        Create a backup.
  -r        Restore a backup.
  -c        Remove all backups.

Example:
switch-os -b windows
```
## Credits
- **Author**: [...HappyEnd...](https://github.com/roihershberg/bootctl-binary?tab=readme-ov-file) ([4PDA](https://4pda.to/forum/index.php?showuser=8611316))
- **Bootctl**: [Roee Hershberg](https://github.com/roihershberg/bootctl-binary?tab=readme-ov-file)
