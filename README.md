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
  >(In the driver's Info.plist I added the option "fallbackMAC" to "Driver Parameters". "fallbackMAC" is a string which may be used to supply your original MAC address. It is used only if retrieving a valid MAC address fails. In the default configuration, the string is empty. In case you need it, please fill in your MAC with the following syntax "xx:xx:xx:xx:xx:xx" in which every x represents exactly one hexadecimal digit.)
