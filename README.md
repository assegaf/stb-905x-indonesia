# stb-905x-indonesia
Adding support to Custom ROM based on your own compilation AOSP or extended AOSP

This project dedicated to make the Indonesian product of AMLOGIC 905x based STB to be an open source ROM. You can modify your own source code make your own automation or anything ...

Supported device :

- STB HG680p (2G Ram) also known in Indonesia as Fiberhome with chipset S905X and board known as P212_GLX (based on ARMBIAN information)

Weird thing is why no one compile the AOSP in latest version like Android 7.0, Android 8.1, Android 9, 10 or 11 .. ?
there is already ARMBIAN with ubuntu 20.x version already. So what is something that everybody missing ? The most rom is customized Android 6.0.1, not compiled from scratch.

Ok I got the USB-TTL setup, to see how things work for the AMLogic device/board. I focus on STB Fiberhome  (Indonesia) known as HG680p.



## Working Setup from Working Custom ROM Android 6.x, with root inside, and reboot recovery method to boot into default recovery then can do TWRP recovery.

found this log. means : the board
Fiberhome GPIOAO_4 power on!!!!!      Multi dtb tool version: v2 .
      Support 4 dtbs.
        aml_dt soc: gxl platform: p212 variant: 2gs
        dtb 0 soc: gxl   plat: p212   vari: 1g
        dtb 1 soc: gxl   plat: p212   vari: 1gs
        dtb 2 soc: gxl   plat: p212   vari: 2g
        dtb 3 soc: gxl   plat: p212   vari: 2gs
      Find match dtb: 3

 means : the board soc gxl, plat: p212, with 2gs variation
 
 on working android 6.0.1 linux kernel I found partition table list, just before kernel android load. it means bootloader do this.
 
 Partition table get from SPL is :
        name                        offset              size              flag
===================================================================================
   0: bootloader                         0            400000                  0
   1: reserved                     2400000           4000000                  0
   2: cache                        6c00000          20000000                  2
   3: env                         27400000            800000                  0
   4: logo                        28400000           2000000                  1
   5: recovery                    2ac00000           2000000                  1
   6: rsv                         2d400000            800000                  1
   7: tee                         2e400000            800000                  1
   8: crypt                       2f400000           2000000                  1
   9: misc                        31c00000           2000000                  1
  10: instaboot                   34400000          20000000                  1
  11: boot                        54c00000           2000000                  1
  12: system                      57400000          70000000                  1
  13: params                      c7c00000            800000                  4
  14: data                        c8c00000         109400000                  4





Booting Android Image at 0x01080000 ...

reloc_addr =73ef5c10
copy done
      Amlogic multi-dtb tool
      Single dtb detected
load dtb from 0x1000000 ......
   Uncompressing Kernel Image ... OK
   kernel loaded at 0x01080000, end = 0x0211cdc0
   Loading Ramdisk to 73d58000, end 73eb6800 ... OK
   Loading Device Tree to 000000001fff3000, end 000000001ffff791 ... OK
signature:
fdt_instaboot: no instaboot image


Starting kernel ...

uboot time: 3815958 us



nothing much information after this.












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


