# Ryzentosh-Asrock-Phantom-Gaming-4
Hackintosh Setup for a Hackintosh with Ryzen on a AsRock Phantom Gaming 4 Mainboard as a iMacPro1,1  

## Read first (really)!
These files are created for my personal setup and should be used as reference files. I'm sure these files will not work with your setup out-of-the-box. Please follow the official OpenCore Vanilla Guide and use this for bugfixing. Use at your own risk!


## Ryzen iMac Pro build
**Prozessor:** AMD Ryzen 9 3900X  
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

### Specific informations
The supplied USB map disables the 2nd port of the internal usb2.0 header - see Known issues for more information

## Known issues
Microphone is not yet working  
Sleep is not working

### Sleep
Sleep is not working, yet. Based on the information from aluveitie, the secondary XHC controller (USB) is preventing sleep. Sadly this controller is providing support to a lot of the supplied usb ports. If you dont use all slots, you can try to disable the controller.

### Corsair Commander Pro
This one is tricky! The corsair commander pro will identify itself as a UPS (Battery) device. Installing while this device is plugged into USB will result in a Segmentation Fault after picking the target storage device. You need to disable the USB port of the Commander Pro.

## Cedits and links
* [Aluveities Setup](https://github.com/aluveitie/RyzenMacPro)
* [OpenCore Desktop Guide](https://github.com/dortania/OpenCore-Desktop-Guide)
* [AMD OC Ryzen](https://github.com/iGPU/AMD_OC_Ryzen)
* [CMMChris' RadeonBoost](https://www.hackintosh-forum.de/forum/thread/47791-radeonboost-kext-benchmark-scores-wie-am-echten-mac-unter-windows/?pageNo=1)
* [trulyspinach's SMCAMDProcessor](https://github.com/trulyspinach/SMCAMDProcessor)
* [khronokernel's SmallTree](https://github.com/khronokernel/SmallTree-I211-AT-patch)
* [VoodooTSCSync Configurator](https://www.insanelymac.com/forum/files/file/744-voodootscsync-configurator/)
* [Liquidctl](https://github.com/jonasmalacofilho/liquidctl)
