# Lenovo ThinkCentre mini M93P 
## Hardware 

### Intel HD Graphics 4600:

  Chipsatz-Modell:	Intel HD Graphics 4600
  Typ:	GPU
  Bus:	Integriert
  VRAM (dynamisch, maximal):	1536 MB
  Hersteller:	Intel
  Geräte-ID:	0x0412
  Versions-ID:	0x0006
  Metal-Familie:	Unterstützt, Metal GPUFamily macOS 1
  Displays:
  TIO22Gen3:
    Auflösung:	1920 x 1080 (1080p FHD - Full High Definition)
    UI sieht aus wie:	1920 x 1080 @ 60.00Hz
    Framepuffertiefe:	24-Bit Farbe (ARGB8888)
    Display-Seriennummer:	V304TP6X    
    Hauptdisplay:	Ja
    Synchronisierung:	Aus
    Eingeschaltet:	Ja
    Rotation:	Unterstützt
    Helligkeit automatisch anpassen:	Ja
    Verbindungstyp:	Thunderbolt/DisplayPort


### Audio:

Line-Eingang (integriert):

  Eingabekanäle:	2
  Hersteller:	Apple Inc.
  Aktuelle SampleRate:	44100
  Transport:	Integriert
  Eingangsquelle:	Line-In

Ausgang (integriert):

  Hersteller:	Apple Inc.
  Ausgangskanäle:	2
  Aktuelle SampleRate:	44100
  Transport:	Integriert
  Ausgangsquelle:	Kopfhörer

DisplayPort:

  Hersteller:	Apple Inc.
  Ausgangskanäle:	2
  Aktuelle SampleRate:	48000
  Transport:	DisplayPort
  Ausgangsquelle:	TIO22Gen3

Thinkcentre TIO22Gen3 for USB-audio:

  Standardeingabegerät:	Ja
  Eingabekanäle:	2
  Hersteller:	Lenovo
  Aktuelle SampleRate:	44100
  Transport:	USB
  Eingangsquelle:	Standard

Thinkcentre TIO22Gen3 for USB-audio:

  Standardausgabegerät:	Ja
  Standard-Systemausgabegerät:	Ja
  Hersteller:	Lenovo
  Ausgangskanäle:	2
  Aktuelle SampleRate:	48000
  Transport:	USB
  Ausgangsquelle:	Standard


![pcie devices](https://github.com/caikn/MacOnChromebox/blob/master/image/pcie.png?raw=true "PCIe devices")

## UEFI boot
to install macos on chromebox, we need to do some hw and firmware changes first to enable UEFI boot.
### Remove write-protect screw
https://kodi.wiki/view/Chromebox#Disable_Firmware_Write_Protect

### Install custome firmware
https://mrchromebox.tech/#fwscript

Install Custom coreboot Firmware (Full ROM). During the installation you should save a backup of the original firmware, in case you want to run chromeOS again.

## Install MAC OS
### Working software version
- macOS High Sierra 10.13.5
- macOS Mojave 10.14.6
- macOS Catalina 10.15.4
- Clover 5033
- WhateverGreen 1.3.8
- Lilu 1.4.3
  
### Boot Arguments  
> -lilubetaall debug=0x100 -disablegfxfirmware -v darkwake=8
 
### Display Port
> HDMI is used during the installation and works also afterwards.
  

## Post Installation

### Ethernet
Use driver RealtekRTL8111-V2.3.0d7.kext

thanks mieze to provide this work around for the empty MAC address issue
> "In the driver's Info.plist I added the option "fallbackMAC" to "Driver Parameters". "fallbackMAC" is a string which may be used to supply your original MAC address. It is used only if retrieving a valid MAC address fails. In the default configuration, the string is empty. In case you need it, please fill in your MAC with the following syntax "xx:xx:xx:xx:xx:xx" in which every x represents exactly one hexadecimal digit."  https://www.insanelymac.com/forum/topic/287161-new-driver-for-realtek-rtl8111/?page=56&tab=comments#comment-2686166

### Display
To use the acerlerated driver for Intel HD4400, the only key to be modified in config.plist is Graphics->ig-platform-id = 0x0d220003

Default working settings for intel gpu (IGPU@2) are as following. check those value with IORegistryExplorer, if the display doesn't work correctly.

| key    | Property             | Value       |
|--------|----------------------|-------------|
| igpu@2 | AAPL,ig-platform-id  | 0300220d    |
| igpu@2 | device-id            | 12040000    |
| igpu@2 | hda-gfx              | "onboard-1" |
| AppleIntelFramebuffer@0 | connector-type | 00080000 |

### Audio
HDMI Audio works with VoodooHDA 2.9.2 kext. Only surround sound playing has strange issue, the central channel (mainly speech) is very blurry and quiet. 

Onboard Realtek ALC283 is not shown as audio device. Still working on that.
AppleHDA HDMI Audio_v2 [Guide]https://www.tonymacx86.com/threads/applehda-hdmi-audio-guide.234735/
https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md



### Wifi/Bluetooth
the AR9462 doesn't work, no wifi device is identified. The ATH9KFixup doesn't help in Mojave and Catalina.
Bluetooth driver is loaded, but no bluetooth device can be found.

I have tried the following two wifi/bluetooth combo cards

#### Broadcom BCM94360NG NGFF 802.11AC BT 4.0 Card  (43.3€ on aliexpress)
  > https://www.tonymacx86.com/threads/working-bcm94360ng-native-support-for-catalina-vs-bcm94352-dw1560.292767/
  It is supported natively by macos, no extra kext is needed.
  
#### Broadcom BCM94352HMB DW1550 tvff 3 802.11AC WLAN Wifi Karte + Bluetooth 4.0 2.4/5 GHz (26.65€ on ebay)
  - Wifi works with Clove + AirportBrcmFixup, follow guide: https://www.tonymacx86.com/threads/broadcom-wifi-bluetooth-guide.242423/
  - Bluetooth: 
    - Mojave: follow the above guide, USB ports are all correct with USBInjectAll.kext , custom SSDT is not needed
    - Catalina: follow this guide https://github.com/acidanthera/BrcmPatchRAM, load BrcmPatchRAM3.kext BrcmFirmwareData.kext BrcmBluetoothInjector.kext with Clover
  - Airdrop, Bluetooth audio, unlocking with iWatch work as designed

## Usefull Tools
  - Hackintool: https://github.com/headkaze/Hackintool/releases
  - KextBeast: https://www.tonymacx86.com/resources/categories/tonymacx86-downloads.3/
  - IORegistryExplorer: https://github.com/vulgo/IORegistryExplorer
  - Clover Configurator: https://mackie100projects.altervista.org
  - etcher: https://www.balena.io/etcher/  flash os image to usb
