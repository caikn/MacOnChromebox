# MacOnChromebox
## Hardware 
Asus Chromebox CN60
- CPU: Intel i7 2700U
- GPU: Intel HD 4400
- RAM: Samsung 2x4GB DDR3 1600 MHZ
- Audio: Intel Haswell HDA Controller
- LAN: RTL 8168G/8111G
- Wifi/Bluetooth: AzureWave AW-NB110H
- SSD: SanDisk 16G      (replaced with Transcend 256GB SATA III 6Gb/s MTS430S 42 mm M.2 SSD)

## UEFI boot
to install macos on chromebox, we need to do some hw and firmware changes first to enable UEFI boot.
### Remove write-protect screw
https://kodi.wiki/view/Chromebox#Disable_Firmware_Write_Protect

### Install custome firmware
https://mrchromebox.tech/#fwscript

Install Custom coreboot Firmware (Full ROM). During the installation you should save a backup of the original firmware, in case you want to run chromeOS again.

## Install MAC OS
### Software version
- macOS High Sierra 10.13.5(17F77)
- Clover 4512
  >(useful link: https://mirrors.dtops.cc/iso/MacOS/daliansky_macos/)
  
- RealtekRTL8111-V2.3.0d7.kext
 
  >In the driver's Info.plist I added the option "fallbackMAC" to "Driver Parameters". "fallbackMAC" is a string which may be used to supply your original MAC address. It is used only if retrieving a valid MAC address fails. In the default configuration, the string is empty. In case you need it, please fill in your MAC with the following syntax "xx:xx:xx:xx:xx:xx" in which every x represents exactly one hexadecimal digit.  https://www.insanelymac.com/forum/topic/287161-new-driver-for-realtek-rtl8111/?page=56&tab=comments#comment-2686166

## Post Installation

### Ethernet

### Video & Audio
working settings for graphics. These values below are default with standar config.plist withat many customized propertiy settings.
| Property             | Value    |
|----------------------|----------|
|AAPL,ig-platform-id   |08002e0a  |
|device-id             |12040000  | 

AppleHDA HDMI Audio_v2 [Guide]https://www.tonymacx86.com/threads/applehda-hdmi-audio-guide.234735/
https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md

https://github.com/RehabMan/Lenovo-U430-Touch-DSDT-Patch

english(too old): https://www.tonymacx86.com/threads/guide-intel-igpu-hdmi-dp-audio-all-sandy-bridge-kaby-lake-and-likely-later.189495/


### Wifi/Bluetooth

ToDo: buy wifi card

- Broadcom BCM94360NG NGFF 802.11AC BT 4.0 Card  (43.3€ on aliexpress)
  > https://www.tonymacx86.com/threads/working-bcm94360ng-native-support-for-catalina-vs-bcm94352-dw1560.292767/
- Broadcom BCM94352Z NGFF 802.11AC BT 4.0 Card
- DW1820A (difficult) https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html


## Usefull Tools
  - Hackintool: https://github.com/headkaze/Hackintool/releases
  - edit plist file:  https://www.fatcatsoftware.com/plisteditpro/
  - IORegistryExplorer: https://github.com/vulgo/IORegistryExplorer
  - PlistEditPro: https://www.fatcatsoftware.com/plisteditpro/
