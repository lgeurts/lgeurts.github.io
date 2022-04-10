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

[Download and prepare Windows 10 Installation Media](https://www.microsoft.com/en-us/software-download/windows10) (a 16 GB+ USB stick) for recovery purposes. And <span style="text-decoration: underline">do not forget your Linux installation media</span> as I did...

To mop it up, double-check that you have the latest firmware updates installed, especially your **Trusted Platform Module** (TPM) firmware. Vendors might not auto-update the TPM using their regular driver and firmware update utilities.

**FREEING UP SPACE ON THE DRIVE**

To install a second operating system you obviously need space on your system drive. You could also use a second drive, but this is probably not a good option for laptop users and small-form-factor devices.

Try to free up at least 20 GB for a Linux installation. Some distros (like Ubuntu and Fedora) install themselves semi-automatically next to Windows with fully guided installation options if you prepare your disk in this way.

Optionally, if your partition layout allows for it you should also grow your UEFI System Partition to circa 1 GB. Multiple operating systems will be storing their UEFI blobs (and possibly multiple versions during system upgrades), and it can be beneficial in the near future to have more space available on this partition.

You can resize and manage your partitions with the built-in Disk Management utility in Windows (search for *“Create and manage hard disk partitions”* in your Windows Search box or Cortana).

If this is a new device that you’ve never stored personal data on, I recommend that when activated you first **disable** BitLocker Device Encryption temporarily before making changes to the drive partitions.
After disabling BitLocker Device Encryption from Windows Settings, you must wait some time for decryption to complete. Then you can proceed to shrink the main drive. Both operations can take hours, depending on the drive. When you shrunk your partition and freed up space, you can **re-enable** BitLocker Device Encryption. Reboot your system and wait for the process to complete before moving on -- this to avoid running into issues later.

If you already stored some data on the drive, you should first create a backup, leave BitLocker Device Encryption enabled, and then just resize the encrypted drive and hope for the best. Don’t format or partition the freed up space, leave this to the Linux installer.

**INSTALLING THE SCEONDARY OS**

Linux installers vary a lot, so I’ll only give general pointers on the installation process. You shouldn’t need to disable Secure Boot to install a modern Linux. Refer to the wiki for your distribution for specifics. Depending on your device, you may have to boot into your installation media from the Windows Settings app: *"System and Updates: Recovery: Advanced Startup"*.

You shouldn't select to use the whole drive. The graphical installers for Fedora and Ubuntu will automatically suggest using the freed up space on the system drive. Always verify that the installers aren’t going to format your Windows or UEFI partitions before accepting their suggestions!

Windows 10 and Linux share the same partition for their UEFI blobs. However, you can't install multiple versions of Windows or the same Linux distro on the same UEFI system partition. Each OS will install into its own named folder e.g. "Microsoft", “Fedora”, or "Ubuntu”, and this naming scheme does not allow for more than one unique version at the time. If you really need to install multiple versions of lets say Ubuntu, then you also have to create separate UEFI system partitions for each one. This requires disabling BitLocker Device Encryption as changing the boot partition will upset the TPM.

Older versions of Windows and some Linux installers will sometimes overwrite the entire UEFI partition. To prevent this type of often fatal errors, **always use shared UEFI partitions**, even when installing to a secondary drive as this will give you an easier time dealing with Secure Boot, BitLocker, and GRUB2.

The OS-prober should auto-detect Windows and create a boot menu item for it alongside Linux in GRUB2. Because Windows Update requires multiple reboots, you must configure GRUB bootloader to remember the most recent boot menu: (GRUB_DEFAULT=saved; GRUB_SAVEDEFAULT=true). This allows an operating system to trigger multiple reboots when performing updates and boot back into the correct base.

**You might be prompted for a BitLocker recovery key after completing the installation**.
