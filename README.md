# Mac-Mini-Killer (Catalina)
Hackintosh setup based on i7-8700 | Gigabyte Z370N | RX560 | 16GB RAM

![telegram-cloud-photo-size-4-5870834206593103936-y](https://user-images.githubusercontent.com/15344287/158160136-0979a39c-001b-4e50-bdd8-fefca8da95da.jpg)

## About this guide 

This is a beginner guide to make a Hackintosh based on GIGABYTE Z370N WIFI motherboard. It focused on post-install setup. If you don't know how to make a bootable macOS Mojave flash drive and install the macOS Mojave, google it. There is a lot of detail instruction on YouTube. 

Current guide optimised for:
* macOS Catalina 10.15.7 (Installed from here https://apps.apple.com/us/app/macos-catalina/id1466841314?mt=12)
* F10 BIOS for z370n (F10 works OOB, [for F12 read this post](https://www.tonymacx86.com/threads/success-b1s-mac-mini-killer-with-macos-mojave-i7-8700-gigabyte-z370n-rx560-16gb-ram.260337/post-1934546))
* FileVault 2 encryption
* AMD RX560/RX570/RX580/RX5900 graphics (if you are going to use iGPU, [read this thread](https://www.tonymacx86.com/threads/guide-fanless-mini-mojave-i5-8600-gigabyte-z370n-wifi-intel-hd630.263345/))

I tried to make this guide as simple as possible. Some parts are still a little bit techy, but I'm going to rewrite them soon. 

## How to ask for help
If you have troubles during migrating to my EFI and settings, please attach «problem reporting» files to your post. The easiest way is to [install and run this script](https://github.com/corpnewt/EssentialsList). 

## My Hackintosh components
[Intel Core i7-8700 non K](https://www.amazon.com/dp/B07598HLB4/).

[GIGABYTE Z370N WIFI](https://www.amazon.com/dp/B076VD4XV4/).

[ASUS ROG-STRIX-RX560-O4G](https://www.amazon.es/gp/product/B071SJ61SZ/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)

[G.SKILL F4-3200C16D-16GTZRXSKILL x2](https://www.amazon.es/DDR4-16-GB-3200-CL16-Kit-16-gtzrx-3200-MHz-3200-C16d/dp/B07CYZCW4T/ref=sr_1_1?crid=LNIHKI60J3MS&keywords=G-SKILL+rgb&qid=1658580838&sprefix=g-skill+rgb%2Caps%2C102&sr=8-1).

[Crucial P2 1TB 3D NAND NVMe PCIe M.2 SSD).
I'm using this disk with a Bootloader partition with Clover and the other partition is the MacOS Catalina OS.

[Noctua NH-L9I](https://www.amazon.com/gp/product/B009VCAJ7W/).
Great low profile cooler that fits my SFF case.

[WiFi adapter from MacBook Air (BCM94360CS2)](http://ali.pub/2rzj90).
Before that, I've tried BCM943602BAED and BCM94352Z. Both of this cards require some kexts to work in macOS, and they will not let your BT keyboard work in BIOS and Clover.

[Mini ITX Small Aluminum Case from AliExpress + PCI-e express cable](https://es.aliexpress.com/item/1005001447085882.html?gatewayAdapt=glo2esp&spm=a2g0o.productlist.0.0.61f053f3bHtRrX&algo_pvid=665ab278-06a7-4b47-b14d-269ead3d401d&algo_exp_id=665ab278-06a7-4b47-b14d-269ead3d401d-0&pdp_ext_f=%7B%22sku_id%22%3A%2212000016141637177%22%7D&pdp_pi=-1%3B86.64%3B-1%3B-1%40salePrice%3BUSD%3Bsearch-mainSearch).

[Server Flex 400W PSU from AliExpress](https://es.aliexpress.com/item/33006830599.html?spm=a2g0o.productlist.0.0.19753195IDGnsV&algo_pvid=dc14efb1-4163-41c3-9a4c-054d4cf90d8d&algo_exp_id=dc14efb1-4163-41c3-9a4c-054d4cf90d8d-1&pdp_ext_f=%7B%22sku_id%22%3A%2267011307264%22%7D&pdp_pi=-1%3B54.63%3B-1%3B-1%40salePrice%3BEUR%3Bsearch-mainSearch) 

## BIOS settings for installation and boot (eGPU)
Actually, Hackintosh can boot even with default BIOS setting. But I made some additional changes: 

* Peripherals ▸ Initial Display Output = **PCIe 1 Slot**
* Chipset ▸ Wake on LAN Enable = **Disabled**

Fast boot, Vt-d and other options that usually recommended to disable not affect my system. 

## Config.plist
I have a few DSDT patches, darkwake=2, tweaks for Power Management and Hardware Acceleration with iGPU. SMBIOS is iMac19,1.

I've managed to figure out about all Config.plist settings and I keep them as minimal as possible. The same with drivers64UEFI folder and all efi's.

## ePGU settings for AMD RX560/570/580
MSI RX560 Aero working great with WhateverGreen.kext. iGPU for hardware acceleration working great too. I applied a few patches in config.plist and turned iGPU on in BIOS.

## BIOS settings for Hardware Acceleration with iGPU 

* Сhipset ▸ Internal Graphics = **Enabled**
* Сhipset ▸ DVMT Pre-Allocated = **64MB**
* Сhipset ▸ DVMT Total Gfx Mem = **128MB**

[How to test Hardware Acceleratio](https://www.tonymacx86.com/threads/success-b1s-mac-mini-killer-with-macos-mojave-i7-8700-gigabyte-z370n-rx560-16gb-ram.260337/page-18#post-1837792).

![](https://d.pr/i/4cFoa5+)

## Sound
Works great with AppleALC.kext and some necessary tweaks in config.plist.

## Networking
Left LAN port works smoothly with IntelMausiEthernet.kext. For right LAN you will need SmallTree-Intel-211-AT-PCIe-GBE.kext.

BT and WiFi work without any kexts. All related futures work too: unlock with Apple Watch, Connectivity, Hands-off, Airdrop, iMessege etc. Bluetooth keyboard and touchpad work in Clover, BIOS and during FileVault login.

Here are the [BCM94360CS2 WiFi/BT drivers for Windows](https://d.pr/f/0i4GOD).

The only problem is that MacBook Air card doesn't fit the standard metal case on the motherboard. So I just removed this case. Also with included internal antennas, I have a weak BT signal. I ordered [two external antennas](http://ali.pub/2sarv8), hope they will fix my problem.

UPD: Actually [it should fit the standard case](https://www.tonymacx86.com/threads/success-b1s-mac-mini-killer-with-macos-mojave-i7-8700-gigabyte-z370n-rx560-16gb-ram.260337/page-9#post-1826462), so you can use it to hold the card in place. Build in antenna connectors should work too.

## Sleep
Sleep and wake work with darkwake=2. Here is my actual pmset info:

![Captura de pantalla 2022-01-21 a las 1 03 55](https://user-images.githubusercontent.com/15344287/150441568-fb838826-03c8-4b51-bf89-300cdea71415.png)


To see your pmset parametrs:

`pmset -g`

To disable any parametr:

`sudo pmset parametr_name 0`

To match my config you need to:

`sudo pmset standby 0`

`sudo pmset womp 0`

`sudo pmset proximitywake 0`

`sudo pmset powernap 0`

`sudo pmset disksleep 0`

`sudo pmset sleep 10`

`sudo pmset autopoweroff 0`


If you want to restore defoult parametrs, go to:

`/Library/Preferences`

and delete all the com.apple.PowerManagement.* files. 

## USB

USB ports configured with [Hackintool](https://www.tonymacx86.com/threads/release-hackintool-v1-8-1.254559/). it is a simpler way to configure USB than [RehabMan's custom SSDT](https://www.tonymacx86.com/threads/guide-creating-a-custom-ssdt-for-usbinjectall-kext.211311/). Especially for beginners. 

Hackintool generates 3 files: SSDT-EC.aml, SSDT-UIAC.aml, SSDT-USBX.aml. 

1. USBInjectAll.kext goes to /Library/Extensions/
2. SSDT-EC.aml, SSDT-UIAC.aml, SSDT-USBX.aml to /EFI/ACPI/patched/

Be aware, that I made my config only for motherboards USB. It will not work with front USB on your case. If you use a front panel USB or connect anything to internal USB-port on the motherboard, you should make all files by ourself. You cand find all instruction in Hackintool (USB tab).

This method provides full USB power for my devices. I tried to charge my iPad Pro, and amperemeter shows that iPad now draws 1.6A. Before [it was 500 mAh max](https://www.tonymacx86.com/threads/success-b1s-mac-mini-killer-with-macos-mojave-i7-8700-gigabyte-z370n-rx560-16gb-ram.260337/page-36#post-1868201). No additional kexts and config needed. 

## Clover Boot options
I have 3 internal drives: System, Clone and Windows. Clover boot screen is a bit messy because of that. So I made FileVault compatible Custom boot entries to have only 3 icons. Other boot options are Hide. I can access them with F3 button.

You should reconfigure this Custom boot entries all just remove all of them.

Also, my system automatically boots to macOS. If you want the same behaviour, you should change my disk UUID to yours.

##  Thermals
CPU is delidded and undervolted to 1.135V. I used [3D printed tool](https://www.youmagine.com/designs/intel-kaby-lake-delid-tool) and [Thermal Grizzly liquid metal](https://amzn.to/2CNpmx5). 

The result is excellent: 34–37°C in idle and 66–69°C in the Blender Benchmark or Prime95 (24°C ambient). Before it easily hit 90+°C with my cooler. 


## What Works
Everything: WiFi, BT, LAN, Audio, iMessage, Wake & Sleep, Universal Clipboard, USB 3, USB-C, DP-audio, Hands-off, AirDrop, Hardware Acceleration, Shutdown, Unlock with Apple Watch, you name it. 

## What Doesn't Work
* [SoundflowerBed](https://github.com/mLupine/SoundflowerBed) is needed to regulate sound with function keys in some monitors that play sound through HDMI. Headset not affected.
* PowerNap is turned off, so no apps update during sleep. Maybe it works, I just not tested it.
* If I enable XMP profile in BIOS for automatic RAM overclock or overclock RAM manually, I have a warning «Disk not ejected properly». after waking from sleep. You need to reconnect external drives to make it work again. It can be critical for people who use external drives on a daily basis. There is three solution for that: 
  - Prevent sleep with free [Amphetamine app](https://itunes.apple.com/us/app/amphetamine/id937984704?mt=12). I like it because it let monitor fall asleep and/or enable screensaver. It’s crucial if you want your Hackintosh to lock automatically. 
  - Disable XMP. Fixes the problem entirely, but harms general performance. 
  - Use [Jettison app](https://www.stclairsoft.com/Jettison/) that unmount drives before sleep. I don’t test it personally. 
 
