# stb-905x-indonesia
Adding support to Custom ROM based on your own compilation AOSP or extended AOSP

This project dedicated to make the Indonesian product of AMLOGIC 905x based STB to be an open source ROM. You can modify your own source code make your own automation or anything ...

Supported device :

- STB HG680p (2G Ram) also known in Indonesia as Fiberhome with chipset S905X and board known as P212_GLX (based on ARMBIAN information)


Weird thing is why no one compile the AOSP in latest version like Android 7.0, Android 8.1, Android 9, 10 or 11 .. ?
there is already ARMBIAN with ubuntu 20.x version already. So what is something that everybody missing ? The most rom is customized Android 6.0.1, not compiled from scratch.

I got good idea by people who stuck the logo for new rom,

I managed to install atvXperience 2FF on this board,

Here the steps:
- unpack level 1, atvXperience 2FF 2GB ROM
- unpack level 1, original X96 ROM
- replace the boot.partition and system.partition in extracted Original ROM
- replace meson1.dtb with attached meson1.dtb

Before replace the boot.partition, you need to extract the atvXperience boot.partition, using Android Image Kitchen,
add following lines to cmd-line

Code:

from 
buildvariant=userdebug
to
androidboot.selinux=permissive buildvariant=userdebug


then repack, replace the boot.partition in stock rom folder
Repack all the image, and burn it using Usb burning tool v2.1.7.0

good luck


