# Mac-Mini-Killer (Monterey / Ventura)
Hackintosh setup based on i7-8700K | Gigabyte Z370N | RX560 | 32GB RAM

![telegram-cloud-photo-size-4-6032617185022687135-y](https://user-images.githubusercontent.com/15344287/184409403-1f5fd9d9-e4ac-4914-b341-7cd3f5ceab81.jpg)

![telegram-cloud-photo-size-4-6035095278073264334-y](https://user-images.githubusercontent.com/15344287/184496650-326dc8a5-49b0-4d89-a10d-e15ddb029339.jpg)

## About this guide 

This is a beginner guide to make a Hackintosh based on GIGABYTE Z370N WIFI motherboard. If you are only interested in installing Monterey on your Hackintosh and you have the same Motherboard, go directly to [Installation](https://github.com/kn0wm4d/Mac-Mini-Killer/blob/master/README.md#bios-settings-for-installation-and-boot-egpu)

Current guide optimised for:
* macOS Monterey 12.5 (Installed from here https://apps.apple.com/es/app/macos-monterey/id1576738294?mt=12)
* F14 BIOS for z370n 
* AMD RX560/RX570/RX580/RX5900 graphics

## How to ask for help
If you have troubles during migrating to my EFI and settings, please attach «problem reporting» files to your post. The easiest way is to [install and run this script](https://github.com/corpnewt/EssentialsList). 

## My Hackintosh components
[Intel Core i7-8700K](https://www.amazon.es/Intel-Core-i7-8700K-Procesador-procesadores/dp/B07598VZR8).

[GIGABYTE Z370N WIFI](https://www.amazon.com/dp/B076VD4XV4/).

[ASUS ROG-STRIX-RX560-O4G](https://www.amazon.es/gp/product/B071SJ61SZ/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)

[G.Skill Trident Z Neo - DDR4, 32 GB (2 x 16 GB)](https://www.amazon.es/G-Skill-Tident-32GB-32Gtzn-2x16GB/dp/B07X19HT3S/ref=sr_1_1?crid=3EZG5BU0XMO9D&keywords=G.SKILL+F4-3200C16D-32&qid=1660325283&s=computers&sprefix=g.skill+f4-3200c16d-32%2Ccomputers%2C77&sr=1-1).

[Crucial P2 1TB 3D NAND NVMe PCIe M.2 SSD](https://www.amazon.com/-/es/Crucial-NAND-NVMe-hasta-2400MB/dp/B089DNM8LR/ref=sr_1_9?__mk_es_US=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=2492832EO5741&keywords=1tb+ssd+m.2&qid=1658580923&sprefix=1+tb+ssd+m.2%2Caps%2C146&sr=8-9).
I'm using this disk with a Bootloader partition with Clover and the other partition is the MacOS Monterey OS.

[Noctua NH-L9I](https://www.amazon.com/gp/product/B009VCAJ7W/).
Great low profile cooler that fits my SFF case.

[Noctua NF-A4x20](https://www.pccomponentes.com/noctua-nf-a4x20-pwm-ventilador-caja-40x20mm).
The Flex PSU with this fan does not make any noise.

[WiFi adapter from MacBook Air (BCM94360CS2)](http://ali.pub/2rzj90).
Before that, I've tried BCM943602BAED and BCM94352Z. Both of this cards require some kexts to work in macOS, and they will not let your BT keyboard work in BIOS and Clover.

[Mini ITX Small Aluminum Case from AliExpress + PCI-e express cable](https://es.aliexpress.com/item/1005001447085882.html?gatewayAdapt=glo2esp&spm=a2g0o.productlist.0.0.61f053f3bHtRrX&algo_pvid=665ab278-06a7-4b47-b14d-269ead3d401d&algo_exp_id=665ab278-06a7-4b47-b14d-269ead3d401d-0&pdp_ext_f=%7B%22sku_id%22%3A%2212000016141637177%22%7D&pdp_pi=-1%3B86.64%3B-1%3B-1%40salePrice%3BUSD%3Bsearch-mainSearch).

[Server Flex 500W PSU from AliExpress](https://es.aliexpress.com/item/4000502320987.html?spm=a2g0o.order_list.0.0.21ef194dWiYb5q&gatewayAdapt=glo2esp)

## BIOS settings for installation and boot (eGPU)

Actually, Hackintosh should boot even with default BIOS settings until Catalina. 
But for Monterey, I needed to make some additional changes: 

* **Load optimised defaults**
* MIT &gt; Enhanced Multi-Core Performance &gt; **Enabled**
* MIT &gt; FCLK Frequency for Early Power On &gt; **Normal (800Mhz)**
* MIT &gt; Extreme Memory Profile(X.M.P.) &gt; **Disabled**
* MIT &gt; System Memory Multiplier &gt; **26.66** _(use plus and minus keys to update)_
* MIT &gt; Memory Ref Clock &gt; **133**
* MIT &gt; Memory Boot Mode &gt; **Enable Fast Boot**
* MIT &gt; Memory Enhancement Settings &gt; **Enhanced Performance**
* SmartFan &gt; Fan Control Mode &gt; **PWM**
* BIOS &gt; FastBoot &gt; **DISABLED**
* BIOS &gt; CSM Support &gt; **DISABLED**
* BIOS &gt; Windows 8/10 Features &gt; **Windows 8/10 WHQL**
* BIOS &gt; Secure Boot &gt; **DISABLED**
* Peripherals &gt; Initial Display Output &gt; **PCIe 1 Slot**
* Peripherals &gt; Above 4G Decoding &gt; **ENABLED**
* Peripherals &gt; Re-Size Bar &gt; **DISABLED**
* Peripherals &gt; Intel PTT &gt; **DISABLED**
* Peripherals &gt; SGX &gt; **DISABLED**
* Peripherals &gt; Trusted Computing &gt; **DISABLED**
* Peripherals &gt; SATA and RST Configuration &gt; SATA Mode Selection &gt; **AHCI**
* Peripherals &gt; SATA and RST Configuration &gt; Aggressive LPM Support &gt; **DISABLED**
* Peripherals &gt; SATA and RST Configuration &gt; Sata **N** _(all ports)_ &gt; Hot Plug &gt; **DISABLED**
* Peripherals &gt; USB Config &gt; Legacy &gt; **DISABLED**
* Peripherals &gt; USB Config &gt; XHCI Handoff &gt; **ENABLED**
* Peripherals &gt; USB Config &gt; Port 60/64 emulation &gt; **DISABLED**
* Chipset &gt; VT-d &gt; **DISABLED**
* Chipset &gt; Wake On Lan &gt; **DISABLED** _(remind to disable it on adapters too)_
* Power &gt; Platform Power Management &gt; **ENABLED** _(enable child items **PEG**, **PCH** and **DMI ASPM**)_
* Power &gt; AC BACK &gt; **Always Off**
* Power &gt; ErP &gt; **ENABLED**
* Power &gt; Soft-Off by PWR-BTTN &gt; **Delay 4 Sec.**
* Power &gt; Power Loading &gt; **DISABLED**
* Power &gt; CEC 2019 Ready &gt; **DISABLED**
* Save and restart

Fast boot, Vt-d are important to be DISABLED.

## Config.plist

Use [ProperTree](https://github.com/corpnewt/ProperTree) to edit the **`config.plist`** file and change **PlatformInfo** values to your own machine:
- **MLB**, **SystemSerialNumber** and **SystemUUID** can be generated by [GenSMBIOS utility](https://github.com/corpnewt/GenSMBIOS);
- Before use a generated **SystemSerialNumber**, check it on [Apple Database](https://checkcoverage.apple.com) _(If it is valid, generate another and repeat if necessary until find an invalid and unused one)_; 
- **ROM** is the Mac address of the **en0** network adapter _(on Gigabyte z370N WIFI 1.0 is the Intel i219v gigabit port)_. Use the **Network Settings > Advanced > Hardware** panel to copy the Mac address _(only numbers and letters, without the : chars)_;
- Inside the **`config.plist`** search and replace **AAAAAAAAAAAA** with your generated _SystemSerialNumber_ value, **BBBBBBBBBBBBBBBBBB** with _MLB_ value, **CCCCCC-CCCC-CCCC-CCCC-CCCCCCCCCCCC** with _SystemUUID_ value and **DDDDDDDD** with _ROM_ value:
```xml
<key>PlatformInfo</key>
<dict>
	<key>Automatic</key>
	<true/>
	<key>CustomMemory</key>
	<false/>
	<key>Generic</key>
	<dict>
		<key>MaxBIOSVersion</key>
		<false/>
		<key>AdviseFeatures</key>
		<false/>
		<key>SystemMemoryStatus</key>
		<string>Auto</string>
		<key>MLB</key>
		<string>BBBBBBBBBBBBBBBBBB</string>
		<key>ProcessorType</key>
		<integer>0</integer>
		<key>ROM</key>
		<data>DDDDDDDD</data>
		<key>SpoofVendor</key>
		<true/>
		<key>SystemProductName</key>
		<string>MacPro7,1</string>
		<key>SystemSerialNumber</key>
		<string>AAAAAAAAAAAA</string>
		<key>SystemUUID</key>
		<string>CCCCCC-CCCC-CCCC-CCCC-CCCCCCCCCCCC</string>
	</dict>
	<key>UpdateDataHub</key>
	<true/>
	<key>UpdateNVRAM</key>
	<true/>
	<key>UpdateSMBIOS</key>
	<true/>
	<key>UpdateSMBIOSMode</key>
	<string>Create</string>
	<key>UseRawUuidEncoding</key>
	<false/>
</dict>
```

## MacOS 12 Monterey Upgrade

- Can be direct downloaded from Apple using [App Store](https://www.apple.com/br/macos/monterey/) on a regular MacOS computer; 
- Make a **USB** install disk _(the example below uses a USB device named USB and makes Monterey installation disk)_:
```bash
sudo /Applications/Install\ macOS\ Monterey.app/Contents/Resources/createinstallmedia --volume /Volumes/USB
```
- Use [git repo](https://github.com/kn0wm4d/Mac-Mini-Killer) to download the **EFI** folder 

```bash
git clone git@github.com/kn0wm4d/Mac-Mini-Killer.git
```
- Mount the **EFI partition** of the **USB** disk using [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) and **copy the EFI folder** inside **`/Volumes/EFI`**
- **Boot** the target machine with **USB** disk you just made.
- Press Space in the bootloader
- Select **Modified GRUB Shell**, and disable **CFG Lock** first with command below:
```bash
setup_var_3 0x5A4 0x00
```
**Please note that hardcoded value is for F14 BIOS version of the Gigabyte z370N WIFI 1.0 motherboard**, if you use another BIOS version or another motherboard, [UPGRADE THE BIOS FIRST](https://download.gigabyte.com/FileList/BIOS/mb_bios_z370n-wifi_f14.zip?v=1721a09678605dfe57bab703fbc37e1d):

| Gigabyte Z370N WiFi BIOS | CFG Lock offset |
| :----------------------: | --------------- |
|         **F10**          | _0x0585_        |
|         **F14**          | _Ox05A4_        |

- Use **Clear NVRAM** and reboot to make a clean install
- Use **Disk Utility** to erase a **APFS GUI** volume and **install MacOS**
- Finish **normal** MacOS setup


## ePGU settings for AMD RX560/570/580
ASUS ROG STRIX RX560 working great with WhateverGreen.kext. iGPU for hardware acceleration working great too. I applied a few patches in config.plist and turned iGPU on in BIOS.

## Sound
Works great with AppleALC.kext and some necessary tweaks in config.plist.

## Networking
Left LAN port works smoothly with IntelMausiEthernet.kext. For right LAN you will need SmallTree-Intel-211-AT-PCIe-GBE.kext.

BT and WiFi work without any kexts. All related futures work too: unlock with Apple Watch, Connectivity, Hands-off, Airdrop, iMessege etc. Bluetooth keyboard and touchpad work in Clover, BIOS and during FileVault login.

Here are the [BCM94360CS2 WiFi/BT drivers for Windows](https://d.pr/f/0i4GOD).

## Sleep
Sleep and wake work with darkwake=2. Here is my actual pmset info:

![Captura de Pantalla 2022-08-12 a las 19 19 46](https://user-images.githubusercontent.com/15344287/184410888-91c47312-d341-4be7-bf43-24fc21098258.png)

To see your pmset parametrs:

```bash
pmset -g
```

Sometimes after sleep the computer will **wake every few minutes**. Normal Macs do this for several reasons, like other devices near. If you require a deep sleep without random wakeups, use the commands below to **disable this features**:
```bash
sudo pmset proximitywake 0
```
This is a desktop machine, you may want to **disable hibernation**:
```bash
sudo pmset hibernatemode 0
```
If you want to **restore the default** factory settings:
```bash
sudo pmset -a restoredefaults
```

## USB Ports

The included **`USBMap.kext`** with USB mapping is for the **Gigabyte z370N WiFi 1.0 and MacPro7,1 SMBIOS only** with some **USB 3** ports, one **USB type C** and one **internal Bluetooth USB** port enabled.

Keep in mind that **you have to choose what ports to enable**, because **MacOS has a 15 logical ports limit** and each port has 2 logical ports _(one physical port has one USB 2 and one USB 3 personality, and USB Type C has different ports for each side... so **2 logical ports per physical port**)_ and you have to **reserve a port for Bluetooth card**.

![Motherboard](https://user-images.githubusercontent.com/15344287/184415158-15ba7799-2a8b-42f6-87c9-639766be6fd7.png)

**List of the 15 ports ENABLED**:

| Label | Name               |  Type  | Comment                                                             |
| :---: | ------------------ | :----: | ------------------------------------------------------------------- |
| **I** | HS01, **SS01**     |  0, 3  | _USB 2.0 & **3.1** front 1_                                         |
| **I** | HS02, **SS02**     |  0, 3  | _USB 2.0 & **3.1** front 2_                                         |
| **F** | HS03, **SS03**     |  0, 3  | _USB 2.0 & **3.1** rear 5_                                          |
| **G** | HS04, **SS04**     |  0, 3  | _USB 2.0 & **3.1** rear 6_                                          |
| **C** | HS05               |   0    | _USB 2.0 rear 3_                                                    |
| **D** | HS06               |   0    | _USB 2.0 rear 4_                                                    |
| **E** | HS09               |   0    | _USB 2.0 only rear **Type C**_                                      |
| **H** | HS10               |  255   | _USB 2.0 **internal** (bluetooth)_                                  |
| **J** | HS11               |   0    | _USB 2.0 **internal** (wireless keyboard or mouse dongle)_          |
| **E** | **SS09**, **SS10** | 10, 10 | _USB **3.1** only rear **Type C** (for each side of the connector)_ |

**List of ports DISABLED**:

|  Label   | Port                     | Comment                       |
| :------: | ------------------------ | ----------------------------- |
|  **C**   | _SS05_                   | _Only USB 2.0 active on HS05_ |
|  **D**   | _SS06_                   | _Only USB 2.0 active on HS06_ |
|  **A**   | _HS07, SS07_             | _Only to power my desklight_  |
|  **B**   | _HS08, SS08_             | _Only to power my soundbar_   |
|  **J**   | _HS12_                   | _Not used in macOS_           |
| _hidden_ | _HS13, HS14, USR1, USR2_ | _Not used in macOS_           |

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
 
