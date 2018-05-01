# Download distribution

First I downloaded the x86_64 DVD image from https://software.opensuse.org/distributions/leap. This page also contains useful links about how to burn a DVD from an image under Windows or how to create a bootable USB stick.

I decided to create a DVD. Under Windows 7 this is very easy: right-click on the image file and select "Burn DVD". Easy!

# Installation

Then I booted from the DVD and followed the default installation procedure. As I had an additionad SSD installed in my computer, I offered only this drive to the installer.

There was nothing special in the installation procedure, it just worked! 

# Dual boot

It finally installed a grub bootloader on the new SSD which offers to select from either Linux or Windows. I therefore activated the new hard disk as first boot device in the BIOS setup and selected to have Windows as default for the time being. This adjustment can easily be done from Yast, selecting to adjust the bootloader configuration.
