# asus-x555l-hackintosh
This repository contains all the supporting files to install and run macOS High Sierra 10.13.6 on ASUS F555L (X555 and F555 model) laptop.

-------
**Specs :**

 - Processor : Intel Core i7 5500U 2.4 Ghz turbo boost 3.0 Ghz
 - IGPU : Intel HD Graphics 5500
 - RAM : 12GB DDR3L 1600MHz (8GB external + 4GB onboard)
 - Built-in Audio : ALC233
 - Wifi : AR9485 without Bluetooth
 - Ethernet : Realtek RTL8168GU/8111GU
 - SSD: Colorful SL500 240GB
 - Bootloader : CLoverEFI
 

**Working :**

 - Native Power Management
 - Intel HD Graphics 5500
 - Ethernet
 - USB ports
 - Battery status
 - Keyboard
 - TrackPad (Two finger)
 - Internal Audio & Microphone
 - Wifi AR9485
 - Brightness
 - Backlight Control
 - VGA Ports
 - HDMI Ports
 - Shutdown / Reboot
 - Sleep
 - iMessage
 - Webcam

----------

**Setup guide**
-----------

**BIOS Configuration**

Bios Config | Setting 
:---:| :---:
Security -> Secure Boot | Disabled
Intel Virtualization    | Disabled
VT-d | Disabled
Graphics Configuration -> DVMT Pre-Allocation | 64M
SATA Mode | AHCI
Boot -> Launch CSM | Enabled (For Reducing boot graphics glitch)

-------------
**Create USB Installer**
-------------

1. Download macOS from the Mac App Store. It downloads to your Applications folder as a single ”Install” file, such as Install macOS High Sierra.

2. When the installer opens, quit it without continuing installation.

3. Open Terminal, which is in the Utilities folder of your Applications folder.

4. Type one of the following commands in Terminal. These all assume that the installer is in your Applications folder, and the name of the volume that you're using for the bootable installer is `MyVolume`. If your volume is named differently, replace `MyVolume` with the name of your volume.

**High Sierra :**

    sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
    
5. **DO NOT** Close Terminal until it finish copying all files on the USB.

-------------

**Installing CLover Bootloader on the USB Installer**
-------------

[![Clover Setting](http://img.ziggi.org/Q7mMDAVg.png "Clover Setting")](http://img.ziggi.org/Q7mMDAVg.png "Clover Setting")

1. Download Clover Bootloader from this link : [CloverEFI Bootloader](https://sourceforge.net/projects/cloverefiboot/ "CloverEFI")

2. Open `Clover_v*.pkg` in the Tools directory of this repository or from the link above and install it on your USB, customize and select 

3. Open `/Volumes/EFI/Clover/` , Copy and Replace the entire `EFI/CLOVER` Folder in the ESP of your USB Drive with `EFI/CLOVER` folder in this repository.

4. Open `EFI/CLOVER/config.plist` in the ESP of your USB Drive. Run Clover Configurator included in the `Tools/` folder in the repository. Use Macbook Air 6,2 / Macbook Pro 12,1. Generate Serial Number, BoardSerialNumber, SmUUID in SMBIOS tab.

5. Also copy Clover Bootloader installer .pkg file  & other files you need to your install macOS USB  for Post-installation.

6. Boot the USB Installer !

----------------

**Post-install**
----------------

- Install Clover EFI Bootloader to your **HDD** and select Clover UEFI.

- Copy Clover files from your USB to yout HDD. *like you did with your USB Installer before*
--------------

**Summary of problems and fixes**
--------------

Features  |   Fixes
:------------: | :------------:
Intel HD 5500 QE/Ci | Inject Intel  ig-platform **0x16260006** & SMBIOS MBP12.1
Audio | AppleALC.kext & Lilu.kext + LayoutID **3**
Wifi AR9485 | IO80211Family.kext to S/L/E
Brightness | Use AppleBacklight method https://www.tonymacx86.com/threads/guide-laptop-backlight-control-using-applebacklightinjector-kext.218222/
Fn Control Key | AsusNBFnKeys.kext & patch DSDT
Touchpad & Keyboard | ApplePS2SmartTouchpad.kext 
Battery Status | ACPIBatteryManager.kext & patch DSDT 

----------------

**DSDT Patches**
---------------

Patches are from Rehabman Laptop Patches repo Source :  http://raw.github.com/RehabMan/Laptop-DSDT-Patch/master

- Generic Fixes
- HPET Fix
- IRQ Fix
- _PTS Fix
- _WAK Fix
- Add IMEI and MCHC
- OSYS Fix
- IAOE Reference Fix
- SMBUS Fix
- Battery Patch
- _PRW 0x6D Fix
- Fn Key Patches
- WiFi BT Toggle + Status Patch

--------------------
