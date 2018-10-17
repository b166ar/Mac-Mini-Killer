# Mac-Mini-Killer
Hackintosh setup based on i7-8700 | Gigabyte Z370N | RX560/HD630 | 16GB RAM

## About this guide 

This is a beginner guide to make a Hackintosh based on GIGABYTE Z370N WIFI motherboard. It focused on post-install setup. If you don't know how to make a bootable macOS Mojave flash drive and install the macOS Mojave, google it. There is a lot of detail instruction on YouTube. 

Current guide optimised for:
* macOS Mojave 10.14.0
* F10 BIOS for z370n
* FileVault 2 encryption
* AMD RX560/RX570/RX580 or HD630 graphics

I tried to make this guide as simple as possible. Some parts are still a little bit techy, but I'm going to rewrite them soon. 

## How to ask for help
If you have troubles during migrating to my EFI and settings, please attach «problem reporting» files to your post. The easiest way is to [install and run this script](https://github.com/corpnewt/EssentialsList). 

## My Hakintosh components
[Intel Core i7-8700 non K](https://www.amazon.com/dp/B07598HLB4/?tag=macosworldru-20).

[GIGABYTE Z370N WIFI](https://www.amazon.com/dp/B076VD4XV4/?tag=macosworldru-20).

[G.SKILL 16GB (2 x 8GB) DDR4 3200MHz](https://www.amazon.com/dp/B017RKV4N2/?tag=macosworldru-20).

[250GB Samsung 970 EVO M.2](https://www.amazon.com/dp/B07BN5FJZQ/?tag=macosworldru-20).
I'm using two of this disk: one for macOS and one for Windows 10 (gaming).

[250GB SanDisk Ultra II SATA III 2.5-Inch](https://www.amazon.com/dp/B00M8ABEIM/?tag=macosworldru-20).
I'm using this disk for a bootable clone of macOS Mojave.

[Noctua NH-L9I](https://www.amazon.com/gp/product/B009VCAJ7W/?tag=macosworldru-20).
Great low profile cooler that fits my SFF case.

[WiFi adapter from MacBook Air (BCM94360CS2)](http://ali.pub/2rzj90).
Before that, I've tried BCM943602BAED and BCM94352Z. Both of this cards require some kexts to work in macOS, and they will not let your BT keyboard work in BIOS and Clover.

[Flex 4.5L case and SeaSonic 300W 80+ Gold PSU](https://smallformfactor.net/forum/threads/custom_mod-sx-mid-6-8l.1786/).
This is the custom made SFF case that comes with moded server PSU. 

## BIOS settings for installation and boot
Actually, Hackintosh can boot even with default BIOS setting. But I made some additional changes: 

- Disabled Wake on LAN;
- Manually overclocked RAM to 3600 MHz (16-19-19-38, DRAM Voltage 1.4V);
- Undervolt CPU: VCore=1,35V;
- Disable motherboard RGB;
- Set macOS UEFI partition first boot option. 

Fast boot, Vt-d and other options that usually recommended to disable not affect my system. 


