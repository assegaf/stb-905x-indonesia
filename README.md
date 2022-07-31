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



-------------- UPDATE IMG from Custom Compilation and with error about different partition table

.................................................

U-Boot 2015.01 (Jun 10 2019 - 20:37:17)

DRAM:  2 GiB
Relocation Offset is: 76ec9000
gpio: pin GPIOAO_6 (gpio 106) value is 0
gpio: pin GPIOH_8 (gpio 57) value is 1
gpio: pin GPIOH_9 (gpio 58) value is 0
gpio: pin GPIOAO_9 (gpio 109) value is 0
gpio: pin GPIOAO_5 (gpio 105) value is 1
register usb cfg[0][1] = 0000000077f5f9e8
vpu: error: vpu: check dts: FDT_ERR_BADMAGIC, load default parameters
vpu: clk_level = 7
vpu: set clk: 666667000Hz, readback: 666660000Hz(0x300)
vpp: vpp_init
boot_device_flag : 1
Nand PHY Ver:1.01.001.0006 (c) 2013 Amlogic Inc.
init bus_cycle=6, bus_timing=7, system=5.0ns
reset failed
get_chip_type and ret:fffffffe
get_chip_type and ret:fffffffe
chip detect failed and ret:fffffffe
nandphy_init failed and ret=0xfffffff1
MMC:   aml_priv->desc_buf = 0x0000000073ec9dd0
aml_priv->desc_buf = 0x0000000073ecc0f0
SDIO Port B: 0, SDIO Port C: 1
emmc/sd response timeout, cmd8, status=0x1ff2800
emmc/sd response timeout, cmd55, status=0x1ff2800
[mmc_init] mmc init success
mmc read lba=0x14000, blocks=0x400
      Amlogic multi-dtb tool
      Multi dtb detected
gpio: pin GPIOAO_6 (gpio 106) value is 0
gpio: pin GPIOH_8 (gpio 57) value is 1
gpio: pin GPIOH_9 (gpio 58) value is 0
gpio: pin GPIOAO_9 (gpio 109) value is 0
gpio: pin GPIOAO_5 (gpio 105) value is 1
GPIOAO_4 value board_id_gpio = 0
saradc: check dts: FDT_ERR_BADMAGIC, load default parameters
-----board_version[9]
      unified board, board id adc = 9
Fiberhome GPIOAO_4 power on!!!!!      Multi dtb tool version: v2 .
      Support 4 dtbs.
        aml_dt soc: gxl platform: p212 variant: 2gs
        dtb 0 soc: gxl   plat: p212   vari: 1g
        dtb 1 soc: gxl   plat: p212   vari: 1gs
        dtb 2 soc: gxl   plat: p212   vari: 2g
        dtb 3 soc: gxl   plat: p212   vari: 2gs
      Find match dtb: 3
start dts,buffer=0000000073ece970,dt_addr=0000000073eeb970
parts: 12
00:      logo0000000002000000 1
01:  recovery0000000002000000 1
02:       rsv0000000000800000 1
03:       tee0000000000800000 1
04:     crypt0000000002000000 1
05:      misc0000000002000000 1
06: instaboot0000000020000000 1
07:      boot0000000002000000 1
08:    system0000000070000000 1
09:     cache0000000020000000 2
10:    params0000000000800000 4
11:      dataffffffffffffffff 4
get_dtb_struct: Get emmc dtb OK!
overide_emmc_partition_table: overide cache 
[mmc_get_partition_table] skip partition cache.
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
mmc read lba=0x12000, blocks=0x2
mmc read lba=0x12002, blocks=0x2
mmc_read_partition_tbl: mmc read partition OK!
eMMC/TSD partition table have been checked OK!
mmc env offset: 0x27400000 
In:    serial
Out:   serial
Err:   serial
reboot_mode=cold_boot
board_late_init,defenv!
hpd_state=1
[1080p60hz] is invalid for cvbs.
set hdmitx VIC = 16
config HPLL = 2970
HPLL: 0xc000027b
config HPLL done
j = 4  vid_clk_div = 1
hdmitx phy setting done
hdmitx: set enc for VIC: 16
rx version is 1.4 or below  div=10
hdmtix: set audio
[store]To run cmd[emmc dtb_read 0x1000000 0x40000]
read emmc dtb
      Amlogic multi-dtb tool
      Multi dtb detected
gpio: pin GPIOAO_6 (gpio 106) value is 0
gpio: pin GPIOH_8 (gpio 57) value is 1
gpio: pin GPIOH_9 (gpio 58) value is 0
gpio: pin GPIOAO_9 (gpio 109) value is 0
gpio: pin GPIOAO_5 (gpio 105) value is 1
GPIOAO_4 value board_id_gpio = 0
saradc: check dts: FDT_ERR_BADMAGIC, load default parameters
-----board_version[9]
      unified board, board id adc = 9
Fiberhome GPIOAO_4 power on!!!!!      Multi dtb tool version: v2 .
      Support 4 dtbs.
        aml_dt soc: gxl platform: p212 variant: 2gs
        dtb 0 soc: gxl   plat: p212   vari: 1g
        dtb 1 soc: gxl   plat: p212   vari: 1gs
        dtb 2 soc: gxl   plat: p212   vari: 2g
        dtb 3 soc: gxl   plat: p212   vari: 2gs
      Find match dtb: 3
Net:   dwmac.c9410000
wipe_data=successful
wipe_cache=successful
upgrade_step=2
[OSD]load fb addr from dts
[OSD]failed to get fb addr for logo
[OSD]use default fb_addr parameters
[OSD]fb_addr for logo: 0x3d800000
[OSD]load fb addr from dts
[OSD]failed to get fb addr for logo
[OSD]use default fb_addr parameters
[OSD]fb_addr for logo: 0x3d800000
[CANVAS]canvas init
[CANVAS]addr=0x3d800000 width=5760, height=2160
amlkey_init() enter!
[EFUSE_MSG]keynum is 4
[KM]Error:f[key_manage_query_size]L507:key[deviceid] not programed yet
gpio: pin GPIOAO_2 (gpio 102) value is 1
InUsbBurn
noSof
Hit Enter or space or Ctrl+C key to stop autoboot -- :  1  0 
gxl_p212_v1#


gxl_p212_v1#


gxl_p212_v1#


gxl_p212_v1#


gxl_p212_v1#


gxl_p212_v1#


gxl_p212_v1#


gxl_p212_v1#


gxl_p212_v1#


gxl_p212_v1#


gxl_p212_v1#


gxl_p212_v1#run update


InUsbBurn
noSof
card in
[mmc_init] mmc init success
Device: SDIO Port B
Manufacturer ID: 3
OEM: 5344
Name: SC16G 
Tran Speed: 50000000
Rd Block Len: 512
SD version 3.0
High Capacity: Yes
Capacity: 14.8 GiB
mmc clock: 40000000
Bus Width: 4-bit
[MSG]Reload bmps env.
Err imgread(L472):Logo header err.
[MSG]ini sz 0x18aB
[fat]Filesize is 0x18aB[0M]
[fat]0x:leftSz 18a < BPS 2000, gotSz 18a

=========sdc_burn_paras=====>>>
[common]
erase_bootloader = 0
erase_flash      = 1
reboot           = 0x0
key_overwrite    = 0x0

[burn_ex]
package          = aml_upgrade_package.img
media            = 

[burn_parts]
burn_num         = 0

<<<<=====sdc_burn_paras======

[fat]Filesize is 0x34fee4e4B[847M]
[fat]0x:leftSz c40 < BPS 2000, gotSz 6c40
[MSG]image version [0x00000002]
[fat]Seek 0xfff40 from 0x6c40
[MSG]itemSizeNotAligned 0xc0
[MSG]align 4 mmc read...[fat]0x:leftSz 1ea2 < BPS 2000, gotSz df62
[MSG]Down(mem) part(dtb) sz(0xdf62) fmt(normal)
[MSG]Burn Start...
[MSG]load dt.img to 0x0000000001000000, sz=0xdf62
[MSG]Burn complete
[MSG]echo video prepare for upgrade
hpd_state=1
[OSD]load fb addr from dts
[OSD]fb_addr for logo: 0x7f800000
[OSD]load fb addr from dts
[OSD]fb_addr for logo: 0x7f800000
[CANVAS]addr=0x7f800000 width=5760, height=2160
[1080p60hz] is invalid for cvbs.
set hdmitx VIC = 16
config HPLL = 2970
HPLL: 0xc000027b
config HPLL done
j = 4  vid_clk_div = 1
hdmitx phy setting done
hdmitx: set enc for VIC: 16
rx version is 1.4 or below  div=10
hdmtix: set audio
[MSG]dw,dh[1920, 1080]
[MSG]w,h[4,14]
[MSG]Exit before re-init
command:store  exit
      Amlogic multi-dtb tool
      Single dtb detected
start dts,buffer=0000000007700000,dt_addr=0000000007700000
parts: 17
00:      logo0000000000800000 1
01:  recovery0000000001800000 1
02:      misc0000000000800000 1
03:      dtbo0000000000800000 1
04:  cri_data0000000000800000 2
05:     param0000000001000000 2
06:      boot0000000001000000 1
07:       rsv0000000001000000 1
08:  metadata0000000001000000 1
09:    vbmeta0000000000200000 1
10:       tee0000000002000000 1
11:    vendor000000001c000000 1
12:       odm0000000008000000 1
13:    system0000000064000000 1
14:   product0000000008000000 1
15:     cache0000000046000000 2
16:      dataffffffffffffffff 4
emmc/sd response timeout, cmd8, status=0x1ff2800
emmc/sd response timeout, cmd55, status=0x1ff2800
[mmc_init] mmc init success
switch to partitions #0, OK
mmc1(part 0) is current device
Device: SDIO Port C
Manufacturer ID: 15
OEM: 100
Name: 8GTF4 
Tran Speed: 52000000
Rd Block Len: 512
MMC version 4.0
High Capacity: Yes
Capacity: 7.3 GiB
mmc clock: 40000000
Bus Width: 8-bit
[store]amlmmc erase 1emmckey_is_protected : protect
 start = 0,end = 57343


Caution! Your devices Erase group is 0x400
The erase range would be change to 0x36000~0xe8ffff

start = 221184,end = 15269886
start erase dtb......
start = 81920,end = 82943
dev # 1,  , several blocks erased OK
[store]To run cmd[emmc dtb_write 0x0000000001000000 0x40000]
write emmc dtb
overide_emmc_partition_table: overide cache 
[mmc_get_partition_table] skip partition cache.
Partition table get from SPL is : 
        name                        offset              size              flag
===================================================================================
   0: bootloader                         0            400000                  0
   1: reserved                     2400000           4000000                  0
   2: cache                        6c00000          46000000                  2
   3: env                         4d400000            800000                  0
   4: logo                        4e400000            800000                  1
   5: recovery                    4f400000           1800000                  1
   6: misc                        51400000            800000                  1
   7: dtbo                        52400000            800000                  1
   8: cri_data                    53400000            800000                  2
   9: param                       54400000           1000000                  2
  10: boot                        55c00000           1000000                  1
  11: rsv                         57400000           1000000                  1
  12: metadata                    58c00000           1000000                  1
  13: vbmeta                      5a400000            200000                  1
  14: tee                         5ae00000           2000000                  1
  15: vendor                      5d600000          1c000000                  1
  16: odm                         79e00000           8000000                  1
  17: system                      82600000          64000000                  1
  18: product                     e6e00000           8000000                  1
  19: data                        ef600000          e2a00000                  4
mmc read lba=0x12000, blocks=0x2
mmc read lba=0x12002, blocks=0x2
mmc_read_partition_tbl: mmc read partition OK!
mmc_partition_verify: version OR part_num is different!
Partition table verified ERROR!
Following is the partition table stored in eMMC/TSD: 
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
mmc write lba=0x12000, blocks=0x2
mmc write lba=0x12002, blocks=0x2
mmc_write_partition_tbl: mmc write partition OK!
 partition table success
      Amlogic multi-dtb tool
      Single dtb detected
[burn_parts]
burn_num         = 10
burn_part0       = _aml_dtb
burn_part1       = boot
burn_part2       = dtbo
burn_part3       = logo
burn_part4       = odm
burn_part5       = product
burn_part6       = recovery
burn_part7       = system
burn_part8       = vbmeta
burn_part9       = vendor


[MSG]=====>To burn part [_aml_dtb]
[MSG]itemSizeNotAligned 0xc0
Can not find partition name "_aml_dtb"
get partition info failed !!
amlmmc - AMLMMC sub system

Usage:
amlmmc read  <partition_name> ram_addr addr_byte# cnt_byte
amlmmc write <partition_name> ram_addr addr_byte# cnt_byte
amlmmc erase <partition_name> addr_byte# cnt_byte
amlmmc erase <partition_name>/<device num>
amlmmc rescan <device_num>
amlmmc part <device_num> - show partition infomation of mmc
amlmmc list - lists available devices
amlmmc switch <device_num> <part name> - part name : boot0, boot1, user
amlmmc status <device_num> - read sd/emmc device status
amlmmc ext_csd <bit> <value> - read/write sd/emmc device EXT_CSD [bit] value
amlmmc response <device_num> - read sd/emmc last command response
amlmmc controller <device_num> - read sd/emmc controller register

amlmmc cmd <NULL> failed
store - STORE sub-system

Usage:
store store init flag
store read name addr off|partition size
    read 'size' bytes starting at offset 'off'
    to/from memory address 'addr', skipping bad blocks.
store write name addr off|partition size
    write 'size' bytes starting at offset 'off'
    to/from memory address 'addr', skipping bad blocks.
store rom_write add off size.
write uboot to the boot device
store erase boot/data: 
erase the area which is uboot or data 
store erase partition <partition_name>: 
erase the area which partition in u-boot 
store erase dtb 
store erase key 
store disprotect key 
store rom_protect on/off 
store scrub off|partition size
scrub the area from offset and size 
store dtb iread/read/write addr <size>
read/write dtb, size is optional 
store key read/write addr <size>
read/write key, size is optional 

cmd store size failed 
ERR(../drivers/usb/gadget/v2_burning/v2_sdc_burn/optimus_sdc_update.c)L104:Fail to get size for part _aml_dtb
ERR(../drivers/usb/gadget/v2_burning/v2_sdc_burn/optimus_sdc_update.c)L127:partCapInByte 0x[0, 0] < imgItemSz 0x[0, df62]
ERR(../drivers/usb/gadget/v2_burning/v2_sdc_burn/optimus_sdc_burn.c)L157:fail in sdc_burn_buf_manager_init, rcode 128
ERR(../drivers/usb/gadget/v2_burning/v2_sdc_burn/optimus_sdc_burn.c)L260:Fail in burn part _aml_dtb
ERR(../drivers/usb/gadget/v2_burning/v2_sdc_burn/optimus_sdc_burn.c)L665:Fail when burn partitions
[MSG]to close image
[MSG]=====Burn Failed!!!!!
[MSG]PLS long-press power key to shut down

























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


MODIFIED FILE


device/khadas/kvim/fstab.system.amlogic
device/khadas/kvim/fstab.ab.amlogic

./device/khadas/common/products/mbox/upgrade_4.9/aml_upgrade_package_avb.conf







