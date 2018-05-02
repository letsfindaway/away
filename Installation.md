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
