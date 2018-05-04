# Download distribution

First I downloaded the x86_64 DVD image from [https://software.opensuse.org/distributions/leap](https://software.opensuse.org/distributions/leap). This page also contains useful links about how to burn a DVD from an image under Windows or how to create a bootable USB stick.

I decided to create a DVD. Under Windows 7 this is very easy: right-click on the image file and select "Burn DVD". Easy!

# Installation

Then I booted from the DVD and followed the default installation procedure. As I had an additionad SSD installed in my computer, I offered only this drive to the installer. However the proposed partitioning was to use a 40GB root partition and to allocate the rest to the /home pratition. In my case however most of my data is on an extra drive - the one where they are from the Windows installation, and they also will be there after the Linux migration. On `/home` I only expect a larger amount of data in the dot directories, where profile data, caches and other will be stored.

In order to adjust the sizes I had to use the expert mode to define the partitions. This is however also straight forward. In my case I used 300GB of the 500GB drive for root and the rest for home. I confirmed the choices to use a btrfs for the root partition and a xfs for the home partition, as I wanted to stick as close as possible to the original choices and I did not have any reason to switch to another file system.

Besides that, there was nothing special in the installation procedure, it just worked! 

After installation, the system installed a bunch of updates. Then everything was ready!

# Dual boot

The installer finally installed a grub bootloader on the new SSD which offers to select from either Linux or Windows. I therefore activated the new hard disk as first boot device in the BIOS setup and selected to have Windows as default for the time being. This adjustment can easily be done from the Yast bootloader configuration.

# Mounting the NTFS file system

When startibng the Dolphin file manager the Windows partitions are indicated under "Devices" with a red icon. When you klick on this icon you have to enter your password. The partition is then automatically mounted under some subdirectory of `/run/media`. However this procedure has to be followed after each reboot.

I wanted to have the partition mounted immediately after booting Linux. Do achieve this I followed the following steps:

First create a directory which can act as mount point for the partition. I chose `/windows/d` and created the directory with the command `sudo mkdir -p /windows/d`

Then open a Konsole and enter the command `ls -l /dev/disk/by-uuid/`. This gives you some output like

```
lrwxrwxrwx 1 root root 10  4. Mai 15:07 4078961A78960EB2 -> ../../sda2
lrwxrwxrwx 1 root root 10  4. Mai 15:07 666A8B5F6A8B2B3F -> ../../sda1
lrwxrwxrwx 1 root root 10  4. Mai 15:07 86840bcb-52b8-46c7-9e24-319322e71e6c -> ../../sde2
lrwxrwxrwx 1 root root 10  4. Mai 15:07 86941f9b-dd5d-47f8-8b25-346f91850258 -> ../../sde3
lrwxrwxrwx 1 root root 10  4. Mai 15:07 CA04184404183643 -> ../../sdb1
lrwxrwxrwx 1 root root 10  4. Mai 15:07 e506251e-497e-4780-800b-7a1d0e4a2260 -> ../../sde1
```
`sda` is most probably the drive where your Windows boot partition is located, which corresponds to C:. I can see two partitions here, where one of them is a system rescue partition, the other is C:.

`sdb` is probably the second hard drive, mapped to D: under windows. This is the drive I want to access under Linux. Copy the UUID to the clipboard.

Then edit the `/etc/fstab` file using the command `SUDO_EDITOR=kate sudoedit /etc/fstab`. Add the following line:

```
UUID=CA04184404183643   /windows/d    ntfs-3g user,users,uid=myuser,gid=users,umask=0002  0 0
```

Replace the UUID with the value you got in the previous step and the uid `myuser` with the name of the user who should own the files on this drive. 

After the next reboot the drive will be automatically mounted and Dolphin shows a green icon from the beginning.
