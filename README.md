# asus-tuf-15-opencore
OpenCore files for Asus TUF 15

# Asus TUF 15 FX506L OpenCore OSX EFI
ASUS TUF Dash F15 FX506LHB Opencore
i5-10300H 1GB integrated 10 generation with 8cores
Nvidia GeForce GTX 1660 GDDR6 4GB dedicated vm (128bits)
storage: 1TB SSSD two NVMe kingston512GB, mircron2210 16GB ram memory 
WiFi 6 
running catalina installer from gibmacOS-master APFS formated Intel UHD graphics fully working

use this to download os for isnaller gibmacOS-master https://github.com/corpnewt/gibMacOS
Catalina version 10.15

![Image](https://github.com/user-attachments/assets/c1deedf8-951b-4b49-b02c-7fd493b26dd3)

This repo was created after I was able to boot with the desktop files for Comet Lake platform.
Most of the work to get this to work was done by MaLd0n, which can be found here:
https://www.olarila.com/topic/12233-eblogexitbsstart-error-opencore-big-sur-111/?tab=comments#comment-138034
All credits for the DSDT file go to him.

[![license](https://img.shields.io/badge/license-Anti%20996-blue.svg)](https://github.com/996icu/996.ICU/blob/master/LICENSE)

**macOS Version: Catlina **

**OpenCore Version: 

MacOS on Asus FX506LHB

 MacOS Catalina version 10.15 tested
 :-------------------------:

 ![Uploading Screenshot 2023-04-06 at 8.27.06 AM.png…]()

 ## Updates
- 2021-06-03
Upgraded to MacOS 11.4 - USBports kext added - needed to make USB work
Updated OpenCore to 0.6.9 , Lilu 1.5.3 and WhateverGreen - modified config.plist for black screen delay
 
- 2021-01-16
Change layout id to 17 - headphones + headphones mic now work

- 2021-01-15 (later :) )
Added older WhateverGreen to fix backlight black for 3 minutes.
 
- 2021-01-15:

  * Initial release .

 ## Guide
 
 * Go to [GUIDE](https://dortania.github.io/vanilla-laptop-guide/)(**Official Guide**)

 ## ## System Information 💻
 
 | Part | Functional | Model | 
 | --- | --- | --- |
 | Machine | ✅ | Asus TUF 15 FX506LI |
 | BIOS | ✅ | 3.06 |
 | CPU | ✅ | Intel(R) Core(TM) i5-10300H CPU @ 2.50GHz |
 | RAM | ✅ | 8GB DDR4 SODIMM |
 | SSD | ✅ | 512GB NVMe |
 | iGPU | ✅ | Intel UHD Graphics 630 1536 MB |
 | WLAN | ✅ | Intel AX201 Wifi 6 Card |
 | Bluetooth | ✅ | Intel Bluetooth |
 | Ethernet | ✅ | Realtek 8111 Gigabit Ethernet |
 | Webcam | ✅ | Integrated 720P Webcam |
 | Audio | ✅ | Realtek HDA |
 | Microphone | ✅  | Integrated Microphone |
 | Internal Screen | ✅ | 15.6" 1920x1080 144Hz |
 | Trackpad | ✅/🚫 | I2C ELAN1201 |
 | Keyboard | ✅ | - |
 | dGPU | 🚫 | NVIDIA GTX 1650 4GB GDDR6 |
 
## Perfectly Working Features

- [x] Native Hardware NVRAM
- [x] Intel UHD630
- [x] Screen Brightness Control
- [x] Screen Brightness Memoriztion After Reboot
- [x] Native Screen Refresh Rate Settings
- [x] USB 3.1 Gen 1
- [x] Web Camera
- [x] Battery Percentage
- [x] Sleep & Wake

- [x] ...
  
 ## ## Issues & Solutions
 ### macOS
 * [Hackintool: The Swiss army knife of vanilla Hackintoshing.](https://github.com/headkaze/Hackintool)
 * [How to download a full ‘Install macOS’ gibmacOS-master](https://www.tonymacx86.com/threads/gibmacos-tutorial-how-to-download-macos-directly-from-apple.295248/)
 
 ## Generate your own SMbios

   Platforminfo

   For setting up the SMBIOS info, we'll use CorpNewt's GenSMBIOS and ProperTree application. https://github.com/corpnewt/GenSMBIOS https://github.com/corpnewt/ProperTree

   Because of the Comet Lake (10th Gen), we'll choose the MacBookPro16,4 SMBIOS:

   Run GenSMBIOS, pick option 1 for downloading MacSerial and Option 3 for selecting out SMBIOS. This will give us an output similar to the following:
   (do not use these values, they are unvalid - use your own so you will have unique values)
   Type: MacBookPro16,4

   Serial: C02WXXX2HV2B

   Board Serial: C02826303CDHXXC8B

   SmUUID: 88AA1336-8DF9-477A-A39F-03D016ED0807

   The order is Product | Serial | Board Serial (MLB)

   The Type part gets copied to Generic -> SystemProductName.

   The Serial part gets copied to Generic -> SystemSerialNumber.

   The Board Serial part gets copied to Generic -> MLB.

   The SmUUID part gets copied toto Generic -> SystemUUID.

   We set Generic -> ROM to either an Apple ROM (dumped from a real Mac), your NIC MAC address, or any random MAC address (could be just 6 random bytes, for this guide we'll use 11223300 0000. After install follow the Fixing iServices page on how to find your real MAC Address)

   Reminder that you want either an invalid serial or valid serial numbers but those not in use, you want to get a message back like: "Invalid Serial" or "Purchase Date not Validated"

   Apple Check Coverage page https://checkcoverage.apple.com/cn/zh/

### Monitor
* [Intel® Power Gadget](https://software.intel.com/en-us/articles/intel-power-gadget)
* [IO Registry Explorer](https://download.developer.apple.com/Developer_Tools/Additional_Tools_for_Xcode_11/Additional_Tools_for_Xcode_11.dmg)
* [iStat Menus](https://bjango.com/mac/istatmenus/)
* [HWSensors](https://github.com/kozlek/HWSensors)

### NTFS Writer
* [Mounty](http://enjoygineering.com/mounty/)
 
 ### Audio
 * KEXT required to enable Audio support : `AppleALC.kext`
 * Make sure you inject audio `layout-id = 17` in OpenCore - this is in the current config.plist
 
 ### ELAN Trackpad (TPAD)
 * Using the latest VoodooI2C as of now 2.6.3 with VoodooI2CHID
 * The touchpad works mostly fine, but the buttons only work when the tochpad is touched. both buttons work as left button, so can be used for drag and drop.
 * occassionally there is some delay/tear, right click works by enabling double finger click 
 
 ### Wifi & Bluetooth
 * In order to get Bluetooth and Wifi working, you can use the drivers from https://github.com/OpenIntelWireless/itlwm for wifi
 * For bluetooth https://github.com/OpenIntelWireless/IntelBluetoothFirmware
 * For the UI, there is HeliPort: https://github.com/OpenIntelWireless/HeliPort
 * I like to hide the wireless icon for the builtin card, dozer is a great tool for that: https://github.com/Mortennn/Dozer
 * add heliport to your startup items under login and hide the orginal with dozer and it's hard to see the difference
 
 ### GPU
 ##### iGPU

 * HDMI Port :
    * Long story short, it won't work. Why? Because all display output is hard wired to the NVIDIA GPU. You can confirm this by going into NVIDIA controler panel in Windows and see PhysX, and you can see all display output is wired to the NVIDIA card, while the eDP in screen display is wired to the iGPU. Therefore, since NVIDIA card won't work, also Optimus won't work, the HDMI port or USB-C display output just won't work because the display output is not wired to the iGPU ( and dGPU is disabled) - note this works fine with a USB-c dock that has HDMI/display port on board
    
 ##### dGPU
 * NVIDIA GTX1650 is not supported (for now only in High Sierra it seems) and is disabled 
 * [Apple and Nvidia Are Over: NVIDIA drops CUDA support for macOS.](https://gizmodo.com/apple-and-nvidia-are-over-1840015246)
 * Currently, there is nothing we can do. Let's hope Apple and NVIDIA work together again. 
 
 ### Power Management
 * seems ok, can be improved by
   [CPUFriendFriend](https://github.com/corpnewt/CPUFriendFriend)

   Instructions on how to build a power management profile for any other CPU types can be found here:

   https://github.com/PMheart/CPUFriend/blob/master/Instructions.md
   
 ### Sleep script
 To have the laptop go to sleep when the battery is low, try:
 https://www.tonymacx86.com/threads/release-sleeponlowbattery-solb.264785/
 

## Credits

- [acidanthera](https://github.com/acidanthera) for providing almost all kexts and drivers
- [alexandred](https://github.com/alexandred) for providing VoodooI2C
- [headkaze](https://github.com/headkaze) for providing the very useful [Hackintool](https://www.tonymacx86.com/threads/release-hackintool-v2-8-6.254559/)
- [daliansky](https://github.com/daliansky) for providing the awesome hotpatch guide [OC-little](https://github.com/daliansky/OC-little/) and the always up-to-date hackintosh solutions [XiaoMi-Pro-Hackintosh](https://github.com/daliansky/XiaoMi-Pro-Hackintosh) [黑果小兵的部落阁](https://blog.daliansky.net/)
- [RehabMan](https://github.com/RehabMan) for providing numbers of [hotpatches](https://github.com/RehabMan/OS-X-Clover-Laptop-Config/tree/master/hotpatch) and hotpatch guides
- [corpnewt](https://github.com/corpnewt/CPUFriendFriend) for CPUFriendFriend
- And all other authors that mentioned or not mentioned in this repo
 
 ## License
 * This work is issued under the [996 License](https://github.com/996icu/996.ICU/blob/master/LICENSE) and [MIT License](https://opensource.org/licenses/MIT).
