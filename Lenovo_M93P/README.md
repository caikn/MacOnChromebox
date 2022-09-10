# Lenovo ThinkCentre mini M93P 
## Hardware 

### Intel HD Graphics 4600:

    - Chipsatz-Modell:	Intel HD Graphics 4600
    - VRAM (dynamisch, maximal):	1536 MB
    - Geräte-ID:	0x0412
    - Versions-ID:	0x0006
    - Metal-Familie:	Unterstützt, Metal GPUFamily macOS 1
  
### Displays: Lenovo TIO22Gen3
  
    - Auflösung:	1920 x 1080 (1080p FHD - Full High Definition)
    - UI sieht aus wie:	1920 x 1080 @ 60.00Hz
    - Framepuffertiefe:	24-Bit Farbe (ARGB8888)
    - Display-Seriennummer:	V304TP6X    

### Wifi/Bluetooth Card: DW 1550

Broadcom BCM94352HMB DW1550 tvff 3 802.11AC WLAN Wifi Karte + Bluetooth 4.0 2.4/5 GHz (26.65€ on ebay)

![wifi](https://github.com/caikn/MacOnChromebox/blob/master/image/wifi_dw1550.jpg?raw=true "Wifi")

+ Bluetooth: 
    - Catalina & BigSur: follow this guide https://github.com/acidanthera/BrcmPatchRAM, load BrcmPatchRAM3.kext BrcmFirmwareData.kext BrcmBluetoothInjector.kext with OpenCore
    - Airdrop, Bluetooth audio, unlocking with iWatch work as designed

+ Apple Bluetooth-Softwareversion:	8.0.5d7
    - Adresse:	18-CF-5E-4E-84-9C
    - Bluetooth Low Energy wird unterstützt:	Ja
    - Handoff wird unterstützt:	Ja
    - Instant Hotspot unterstützt:	Ja
    - Hersteller:	Broadcom
    - Transport:	USB
    - Chipsatz:	20702A3
    - Firmwareversion:	v14 c5545
    - Hersteller-ID:	0x413C
    - Produkt-ID:	0x8143
    - Bluetooth-Kernspezifikation:	4.0 (0x6)
    - HCI-Revision:	0x15A9
    - LMP-Version:	4.0 (0x6)
    - LMP-Unterversion:	0x220E

+ Wifi issue in BigSur See: https://www.tonymacx86.com/threads/solved-iokit-daemon-kernelmanagerd-stall-0-240s-pxsx.303324/

    - Solution: After booting into Big Sur I found a second PXSX property in IORegistryExplorer. Which was related to the Broadcom Wi-Fi card. And Wi-Fi was something that I hadn't got working under Big Sur, even if I added brcmfx-driver=2 as a boot argument. After I disabled all AirportBrcmFixup kexts and rebooted the issue went away. Then I remembered that I've read somewhere that one kext has to be disabled under Big Sur. And yeah, AirPortBrcm4360_Injector.kext needs to be removed (see bottom of this page: https://github.com/acidanthera/AirportBrcmFixup). I disabled the kext and re-enabled AirportBrcmFixup and now the computer boots normally, with working Wi-Fi.

+ en2:
  	- Kartentyp:	AirPort Extreme  (0x14E4, 0x17)
  	- Firmware-Version:	Broadcom BCM43xx 1.0 (7.77.111.1 AirPortDriverBrcmNIC-1680.11)
  	- MAC-Adresse:	18:cf:5e:4e:84:9b
  	- Länderkennung:	US
  	- Unterstützte PHY-Modi:	802.11 a/b/g/n/ac
  	- AirDrop:	Unterstützt
  	- AirDrop-Kanal:	149
  	- Automatisches Entsperren:	Unterstützt


### Webcam
In Lenovo Display integrated HD 720P Webcam

### Ethernet
    - Bus:	PCI
    - Hersteller-ID:	0x8086
    - Geräte-ID:	0x153a
    - Subsystem-Hersteller-ID:	0x17aa
    - Subsystem-ID:	0x30a3
    - Versions-ID:	0x0005
    - Kext-Name:	IntelMausi.kext
    - Ort:	/Library/Extensions/IntelMausi.kext

## Install MAC OS
### Working software version
- macOS High Sierra 10.13.5
- macOS Mojave 10.14.6
- macOS Catalina 10.15.7
- macOS BigSur 11.6.8
- OpenCore 
- WhateverGreen 
- Lilu 
  

  
## Usefull Tools
  - Hackintool: https://github.com/headkaze/Hackintool/releases
  - KextBeast: https://www.tonymacx86.com/resources/categories/tonymacx86-downloads.3/
  - IORegistryExplorer: https://github.com/vulgo/IORegistryExplorer
  - Clover Configurator: https://mackie100projects.altervista.org
  - etcher: https://www.balena.io/etcher/  flash os image to usb
