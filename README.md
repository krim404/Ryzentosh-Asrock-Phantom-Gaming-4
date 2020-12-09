# Ryzentosh-Asrock-Phantom-Gaming-4
Hackintosh Setup for a Hackintosh with Ryzen on a AsRock Phantom Gaming 4 Mainboard as a iMacPro1,1  

## Read first (really)!
These files are created for my personal setup and should be used as reference files. I'm sure these files will not work with your setup out-of-the-box. Please follow the official OpenCore Vanilla Guide and use this for bugfixing. Use at your own risk!


## Ryzen iMac Pro build
**Prozessor:** AMD Ryzen 9 5900X  
**Motherboard:** AsRock X570 Phantom Gaming 4  
**Storage:** Mushkin Pilot-E (1000GB) M.2 NVMe PCIe  
**Video Card:** Sapphire Radeon RX 5700 XT Pulse  
**Fan Controller:** Corsair Commander Pro  

## Setup

### Kexts

The following information are relevant for your setup:
* For a working Ryzentosh you need VoodooTSCSyncAMD (Sync amound of CPU Cores/Threads with the OS). You need to edit this file in case you use a different CPU.
* RadeonBoost has been disabled, because of a bug in OSX 10.15.5. This Kext will increase the GPU processing power. As the issue is also present on a retail Mac, we need to wait for a fix from apple

### BIOS settings
- CSM: disabled
- Above 4G decoding: disabled (must be enabled for certain older graphics card)
- Fast boot: disabled
- Serial Port: disabled

### Specific informations
The supplied USB map disables the 2nd port of the internal usb2.0 header - see Known issues for more information  
In case of a newer firmware, the firmware lacks the posibility to disable the serial port, which will result in a black screen on boot on 11.0.1 - see Known issues

## Known issues
Microphone is not yet working  
Sleep is not working

### Sleep
Sleep is not working, yet. Based on the information from aluveitie, the secondary XHC controller (USB) is preventing sleep. Sadly this controller is providing support to a lot of the supplied usb ports. If you dont use all slots, you can try to disable the controller.

### Black Screen on Boot / Disable Serial Port
Navi-Cards from Sapphire will stuck on a black screen when a serial port is assigned. The Phantom Gaming 4 Mainboard has no option to disable the serial port on firmware 3.45. It is still possible to remove the serial port by using the following steps.
* Download https://github.com/LongSoft/UEFITool/releases & https://github.com/LongSoft/Universal-IFR-Extractor/releases
* Run UEFITool - Export the PE32 Image Section (can be found easily by searching for unicode serial) by right clicking on it and select "Extract Body"
* Run ifrextract ExtractedBody.dat Data.txt
* Search in the Data.txt for "Serial Port" and write down the offset and varstore, Example `Serial Port, VarStoreInfo (VarOffset/VarName): 0x0, VarStore: 0x17`
* Search at the top of Data.txt for the name of the VarStore, Example `VarStore: VarStoreId: 0x17 [560BF58A-1E0D-4D7E-953F-2980A261E031], Size: 0x3, Name: PNP0501_0_NV`
* Boot the file modGrubShell.efi from the folder Tools - if no bootloader like refind is installed, rename it to BOOTx64.efi
* Enter `setup_var OFFSET 0x0 NAME`, Example: `setup_var 0x0 0x0 PNP0501_0_NV`
* Reboot

### Corsair Commander Pro
This one is tricky! The corsair commander pro will identify itself as a UPS (Battery) device. Installing while this device is plugged into USB will result in a Segmentation Fault after picking the target storage device. You need to disable the USB port where the the Commander Pro is installed. The Commander Pro itself includes an USB2.0 hub and loops though the 2nd USB2.0 port - so you can still use one of the internal usb ports as normal.

## Cedits and links
* [Aluveities Setup](https://github.com/aluveitie/RyzenMacPro)
* [OpenCore Desktop Guide](https://github.com/dortania/OpenCore-Desktop-Guide)
* [AMD OC Ryzen](https://github.com/iGPU/AMD_OC_Ryzen)
* [CMMChris' RadeonBoost](https://www.hackintosh-forum.de/forum/thread/47791-radeonboost-kext-benchmark-scores-wie-am-echten-mac-unter-windows/?pageNo=1)
* [trulyspinach's SMCAMDProcessor](https://github.com/trulyspinach/SMCAMDProcessor)
* [khronokernel's SmallTree](https://github.com/khronokernel/SmallTree-I211-AT-patch)
* [VoodooTSCSync Configurator](https://www.insanelymac.com/forum/files/file/744-voodootscsync-configurator/)
* [Liquidctl](https://github.com/jonasmalacofilho/liquidctl)
