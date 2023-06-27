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
