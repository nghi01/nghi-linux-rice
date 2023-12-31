# Linux Rice Setup

Personal linux rice setup. Btw I use Arch.

This is technically a guide for a fresh installation of Arch Linux. I dual-booted Arch on my Windows, and at any time we're having trouble with installing, refer to the great [Arch Linux Installation Guide](https://wiki.archlinux.org/title/installation_guide) for help. Without further ado, let's start installing.

## Preparation
What you need to prepare is making sure you're able to access your BIOS (or UEFI) settings. Most systems use F2, F10, or F12 while booting up to access the BIOS/UEFI settings page, but you can also hold Shift while pressing restart to reach this menu.

Another important thing is either an USB drive or a CD/DVD (I'd prefer an USB drive). This will be our installation medium. While it's also possible to install without an USB drive, this is not something we'd go deeply into right now.

Optionally, before installing Arch Linux, please create a recovery drive using a spare USB in case anything happens.

## Download an Installation image
The ISO file that we need to install Arch is available [here](https://archlinux.org/download/). Either download via BitTorrent or through the different available mirrors from your desired countries.

It's optional, but you can also verify the image signature to ensure the integrity of the file. You can download [gpg](https://gnupg.org/download/) to do it.

## Prepare bootable medium
Our next step is to prepare a bootable medium, ideally a bootable USB drive. You would need to mount the previously downloaded ISO file to the USB. The steps would be:

- Plug in your USB.
- Download [Rufus](https://rufus.ie/en/), a program that helps us format and create bootable USB flash drives.
- Launch Rufus.
- On "Boot selection", choose the previously downloaded ISO file.
- On "Device", choose your USB drive.
- On "Partition scheme", if you're using a newly released machine, it's most likely GPT, with the "Target system" being UEFI. (BIOS is the legacy system, while UEFI is the new one).
- Press "Start" and wait until the formatting is done.
## Allocate free space for Arch Linux (If dual boot)
If you're planning to dual boot both Windows and Linux, we need to make sure there's space available in the disk for an Arch installation.
- Press Windows + R. Run diskmgmt.msc. This will lead you to the Disk management interface.
- It depends on your disks, but you can find your SSD name and your HDD name if you have one.
- Now you'll need to decide how much memory you want to spend for the Arch Linux installation. I'd recommend leaving at least 15~20GB + your RAM GB of SSD for this Arch installation. You can add more HDD allocation based on your preferences.
- Once you decide the amount, right click on each disk, and click "Shrink volume".
- Fill in your decided amount of memory. Wait approximately 10 minutes for the shrinking to be done.
- Once you see the black unallocated space, congratulations, you're done with allocating disk space.

To understand this more clearly, we need enough memory space for / (root), home, and swap. Root will be the place where system files and softwares are installed. For this reason, root will need to have the SSD space to run Linux as fast as possible. Home is where your user home directories are, for the less intensive softwares or just storage space for softwares that do not require a lot of speed. We typically use HDD for this one, as there could be multiple users with multiple home directories that need a lot of storage space. Swap space is basically a virtual memory which supports our computers if they run out of memory and require some additional memory. Swap's just incredibly beneficial to memory allocation of our machines. For this reason, swap is much more beneficial to be on SSD.

Personally, I'd go with 50 GB of free space on SSD and 150 GB of free space on HDD. Remember that Swap and Root needs SSD to be optimized. There are also some cases where you need your /home to be on SSD as well, but we will not go too much into that as you can customize later on based on your preferences. As a rule of thumb, we will allocate 1x or 2x of your RAM for swap space, and 30-40 GB of SSD for root. All of HDD can be used for home.

## BIOS Setup Check
Now, with your USB still connected, the next step is to check for BIOS settings. With this, we'll need to enter the BIOS settings. The steps are:
- Restart your computer, mash F2, F10 or F12 (this depends on your computer and I have no idea) while booting up to enter BIOS. This is definitely harder than it sounds, especially for newer machines where the boot up is very fast. Alternatively, you can instead hold Shift + Click Restart to automatically enter the advanced settings, where you can enter UEFI Firmware settings (It's UEFI for newer machines and BIOS for older machines, depending on your system).
- Firstly, turn off Fast Boot and Intel Rapid Start Technology (if applicable). If you've done so, please restart and enter the BIOS/UEFI settings page again.
- Afterwards, rotate to Boot settings, we can see the Boot Order. What we want to do is adjust so that our USB is at the top of the boot order. After doing so, save the changes and restart the computer.
- Afterwards, you'll successfully enter Linux Installation Stage via your USB.

## Linux Installation
What you see now is a black console screen. This is basically the fresh Arch Linux experience, where you'll need to configure a bunch of things to continue.
1. Connect to Internet
	* If you're using an Internet cable, type in the command to verify if you're having Internet.
`
ping archlinux.org 
`
	* If you want to use Wi-fi, you'll need to connect to Wifi using `iwctl`.
 
	* Type `iwctl`, which will bring you to the iwd console program.

	* Type `device list` to find available station devices.
	* Now you know the name of the station you want to connect, type `station stationname scan` where stationname is the name of the station to scan for available wifi networks. Afterwards, type `station stationname get-networks`. Finally, connect the station to the wifi network using `station stationname connect wifiname`. Type in password if necessary.
 	* `ping archlinux.org` to check if you have Internet.
2. Change fonts
Type `setfont ter-132e` for a bigger font. Again, as Arch is a custom-based OS, you can see available fonts by typing `ls /usr/share/kbd/consolefonts/`.

3. Change keyboard layouts
I keep the original keyboard layout which is the latin keyboard layout. However, you can check for available keyboard layouts:
```
ls /usr/share/kbd/keymaps/**/*.map.gz
```
and then load the keyboard layouts to use them.
```
loadkeys de-latin1
```
4. Verify boot mode
This is totally optional, but you can verify the boot mode to make sure if you're booting into 32-bit or 64-bit.
Type:
```
cat /sys/firmware/efi/fw_platform_size
```
If it returns 32, that means you're booted into BIOS, if it's 64, you've booted into UEFI.

5. Update timezone
Type `timedatectl status` to check your current timezones. In order to see available timezones, type `timedatectl list-timezones`. Afterwards, you can set your timezone by typing `timedatectl set-timezone America/New_York` or whichever your preferred timezone to be. Type `timedatectl status` to check your progress.

6. Partitioning disks (Important!)
Alright, now is a very important part. You'll need to allocate and partition the disks accordingly to run Arch properly. As explained previously, you'll need a root partition, a home partition, and a swap partition. I'd personally allocate the root partition and swap partition on SSD, and leave the home partition on HDD. For your reference, my root is 30 GB, swap is 16 GB, and home is 150 GB.

Firstly, check all your available partitionable devices by typing either `lsblk` or `fdisk -l`
