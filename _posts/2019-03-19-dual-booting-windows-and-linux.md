---
layout: post
title: Notes on dual-booting Linux/Windows 10 with BitLocker and Secure Boot
read_time: true
comments: true
category: Secure Computing
tags: [ Secure Computing, Linux Tutorials]
---

![Boot menul](/assets/windows-linux.png)

These **notes** are meant to help you setup a dual-booting system on a computer running **Windows 10** Professional using BitLocker Device Encryption, Modern Standby (a.k.a. Fast Boot), and Secure Boot.

**Linux** installation is covered briefly as we will focus on preserving the Windows pre-boot UEFI environment in such a setup.

**MAKING PREPARATIONS**

Before proceeding you should **backup all** important data to an external disk or your preferred online backup provider. Remember... there is a not insignificant risk of permanently breaking the Windows 10 installation in a non-recoverable fashion as you’ll be making changes to the UEFI partition in your computer.

You should also print a copy of your BitLocker recovery key as it may be needed during this process. This is **not** your BitLocker **PIN** or **password**, but a separate numeric key. Print this key from Control Panel: System and Security: BitLocker Drive Encryption.

Please note that ***the recovery key changes every time you disable and re-enable BitLocker Device Encryption***.
Be sure you have several copies of the most recent recovery key or you may loose access to all your encrypted data! I'd recommend creating a [script](https://blog.ahasayen.com/how-to-backup-bitlocker-keys/) that backups your key to a secure place on the cloud.

[Download and prepare Windows 10 Installation Media](https://www.microsoft.com/en-us/software-download/windows10) (a 16 GB+ USB stick) for recovery purposes. *And do not forget your Linux installation media as I did...*

To mop it up, double-check that you have the latest firmware updates installed, especially your **Trusted Platform Module** (TPM) firmware. Vendors might not auto-update the TPM using their regular driver and firmware update utilities.

**FREEING UP SPACE ON THE DRIVE**

To install a second operating system - whether another copy of Windows, Linux, or something more exotic (FreeBSD?), you'll need space on your system drive. You could also use a second drive, but this is probably not the option for laptop users and small-form-factor devices.

Try to free up at least 20 GB for a Linux installation. Some distribution installers (for example Ubuntu and Fedora) will install themselves alongside Windows with fully guided installation options if you prepare your disk in this way.

Optionally, if your partition layout allows for it you should also grow your UEFI System Partition to about 1 GiB. Some manufacturers only ship 100 MiB partitions or smaller. As multiple operating systems will be storing their UEFI blobs (and possibly multiple versions during system upgrades), it can be beneficial in the future to have more space available on this partition. You may not be able to accomplish this without reinstalling Windows from scratch, and it’s not absolutely necessary — although it might save you some troubleshooting at a later time.

You can resize and manage your partitions with the built-in Disk Management utility in Windows. You can find it by searching for “Create and manage hard disk partitions” in Windows Search or Cortana.

If this is a new device that you’ve never stored any personal data on, I’d recommend that you first disable BitLocker Device Encryption temporarily before making changes to your drive partitions. Windows is fairly decent at self-repairing any accidental damage or problems that can occur when you manipulate your partitions on a native NTFS drive, this in contrary to a BitLocker encrypted drive.
After disabling BitLocker Device Encryption from Windows Settings, you must wait some time for the decryption to complete. Then you can proceed to shrink the main drive. Both of these operations can take hours, depending on the drive. When you’ve shrunk your partition and freed up space, you can re-enable BitLocker Device Encryption. You should reboot your system and wait several hours for the process to complete before proceeding to avoid running into issues later.

If you’ve already stored personal data on the drive, you should first backup everything, leave BitLocker Device encryption enabled, and then just resize the encrypted drive and hope for the best. Don’t format or partition the freed up space afterwards, leave this to the Linux installer.

**INSTALLING THE SCEONDARY OS**

Linux installers vary a lot, so I’ll only give some general pointers on the installation process. You shouldn’t need to disable Secure Boot to install a modern Linux distribution. Refer to the documentation for your distribution for specifics. Depending on your device, you may have to boot into your installation media from the Windows Settings app: System and Updates: Recovery: Advanced Startup.

You shouldn't select to use the entire drive. The graphical installers for Fedora and Ubuntu will automatically suggest using the space you freed up on your system drive earlier. You should always verify that the installers aren’t going to format your Windows or UEFI partitions before accepting their suggestions.

Windows 10 and Linux share the same partition for their UEFI blobs. However, you can not install multiple versions of Windows or multiple version of the same Linux distribution on the same UEFI system partition. Each will install into a folder named after the operating system, e.g. “Fedora”, “Microsoft”, and “Ubuntu”, but this naming scheme doesn’t allow for more than one version at the time. If you need to install multiple version of e.g. Windows, then you also need to create separate UEFI system partitions for each one. This will require that you disable BitLocker Device Encryption as changing the boot partition will upset the TPM.

Older versions of Windows and some Linux installers would sometimes overwrite the entire UEFI partition, but this has been a problem for some years now. You’ll want to mount the existing Windows UEFI partition without formatting it to /boot/efi on your Linux system. You should use a shared UEFI partition, even if you’re installing Linux to a secondary drive as it will give you an easier time with Secure Boot, BitLocker, and GRUB2.

OS-prober should auto-detect Windows and create a boot menu item for it alongside Linux in GRUB2. Windows Update requires multiple reboots, so you’ll want to configure GRUB to remember your last boot menu selection (GRUB_DEFAULT=saved; GRUB_SAVEDEFAULT=true). This will allow either operating system to trigger multiple reboots to perform updates and have it boot into the correct operating system. It’ll also get you back into the same operating system that you used the last time you booted your system.

**You may be prompted for your BitLocker Recovery key after completing the installation**.

I hope you’ll now feel a little bit more prepared to create a dual-booting system with Secure Boot and BitLocker Device Encryption. Things really should just work, but the boot process is delicate so you must take precautions in case you need to restore your system. Good luck!
