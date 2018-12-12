# Mac-Mini-Killer
Hackintosh setup based on i7-8700 | Gigabyte Z370N | RX560/HD630 | 16GB RAM

![](https://d.pr/i/WRdLru+) 

## About this guide 

This is a beginner guide to make a Hackintosh based on GIGABYTE Z370N WIFI motherboard. It focused on post-install setup. If you don't know how to make a bootable macOS Mojave flash drive and install the macOS Mojave, google it. There is a lot of detail instruction on YouTube. 

Current guide optimised for:
* macOS Mojave 10.14.2
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

## BIOS settings for installation and boot (eGPU)
Actually, Hackintosh can boot even with default BIOS setting. But I made some additional changes: 

* Peripherals ▸ Initial Display Output = *PCIe 1 Slot*
* Chipset ▸ Wake on LAN Enable = *Disabled*

Fast boot, Vt-d and other options that usually recommended to disable not affect my system. 

## Config.plist
I have a few DSDT patches, darkwake=2, tweaks for Power Management and Hardware Acceleration with iGPU. SMBIOS is iMac18,3.

I've managed to figure out about all Config.plist settings and I keep them as minimal as possible. The same with drivers64UEFI folder and all efi's.

## Kexts
I moved kexts to /Library/Extensions/, and left in Other only essential kexts that I might be needed during recovery mode. You can find all my kexts from /Library/Extensions/ in the attachment below.

When you copy kexts to /L/E/, don't forget to:

config.plist ▸ System Parameters ▸ Inject Kexts = **Detect**
config.plist ▸ RT Variables ▸ CsrActiveConfig = **0x01** (enable unsigned kexts).

Don't copy kext with Finder, use terminal:

`sudo cp -R KextToInstall.kext /Library/Extensions`

and then:

`sudo kextcache -i /`

Otherwise, they will not be injected properly.

![](https://d.pr/i/crvJMe+) 

## ePGU settings for AMD RX560/570/580
MSI RX560 Aero working great with WhateverGreen.kext. iGPU for hardware acceleration working great too. I applied a few patches in config.plist and turned iGPU on in BIOS.


## iGPU settings for HD630
If you want to run my build with iGPU only, you need to make some changes in config.plist:

* Change SMBIOS from iMac 18.3 to *Mac mini 8* (new Mac mini has 8Gen CPU and don't have eGPU too);
* Set config.plist ▸ Graphics ▸ ig-platform-id = *0x3E9B0007* (you can also try 0x3E920003)

And in BIOS:

* Peripherals ▸ Initial Display Output = *iGFX*
* Сhipset ▸ DVMT Pre-Allocated = *128MB*
* Сhipset ▸ DVMT Total Gfx Mem = *128MB*

Another settings in config.plist and kexts should be the same.

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

![](https://d.pr/i/5YypxK+)

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
[I followed Rehabman's directions to create an SSDT](https://www.tonymacx86.com/threads/guide-creating-a-custom-ssdt-for-usbinjectall-kext.211311/) to inject only the USB ports on the motherboard. You can find it in ACPI → patched folder. If you use a front panel USB or connect anything to internal USB-port on the motherboard, you should make your own custom SSDT. Mine SSDT is only for back panel USBs.

USB 3.0 and USB-C works perfectly without any port limit patches in Clover.

## Clover Boot options
I have 3 internal drives: System, Clone and Windows. Clover boot screen is a bit messy because of that. So I made FileVault compatible Custom boot entries to have only 3 icons. Other boot options are Hide. I can access them with F3 button.

![](https://d.pr/i/N095A2+)

You should reconfigure this Custom boot entries all just remove all of them.
![](https://d.pr/i/NwKyCB+)

Also, my system automatically boots to macOS. If you want the same behaviour, you should change my disk UUID to yours.
![](https://d.pr/i/0L6Tsm+)

##  Thermals
CPU is delidded and undervolted to 1.135V. I used [3D printed tool](https://www.youmagine.com/designs/intel-kaby-lake-delid-tool) and [Thermal Grizzly liquid metal](https://amzn.to/2CNpmx5). 

The result is excellent: 34–37°C in idle and 66–69°C in the Blender Benchmark or Prime95 (24°C ambient). Before it easily hit 90+°C with my cooler. 

![](https://d.pr/i/6Re7Ys+)

## What Works
Everything: WiFi, BT, LAN, Audio, iMessage, Wake & Sleep, Universal Clipboard, USB 3, USB-C, DP-audio, Hands-off, AirDrop, Hardware Acceleration, Shutdown, Unlock with Apple Watch, you name it. 

## What Doesn't Work
* PowerNap is turned off, so no apps update during sleep. Maybe it works, I just not tested it.
* If I enable XMP profile in BIOS for automatic RAM overclock or overclock RAM manually, I have a warning «Disk not ejected properly». after waking from sleep. You need to reconnect external drives to make it work again. It can be critical for people who use external drives on a daily basis. There is three solution for that: 
  - Prevent sleep with free [Amphetamine app](https://itunes.apple.com/us/app/amphetamine/id937984704?mt=12). I like it because it let monitor fall asleep and/or enable screensaver. It’s crucial if you want your Hackintosh to lock automatically. 
  - Disable XMP. Fixes the problem entirely, but harms general performance. 
  - Use [Jettison app](https://www.stclairsoft.com/Jettison/) that unmount drives before sleep. I don’t test it personally. 
  
## Donations

If my configuration helped you to set up and run Hackintosh, feel free to support my work.

It is not necessary, but always welcome.

Paypal — akh420@nyu.edu 
