🚧🚧🚧🚧🚧🚧

# Way to Hackintosh
## File structure of EFI

```
├── EFI
│   ├── APPLE
│   ├── BOOT
│   │   └── BOOTx64.efi
│   └── OC
│       ├── ACPI
│       │   ├── SSDT-AWAC.aml
│       │   ├── SSDT-EC-USBX.aml
│       │   ├── SSDT-EC.aml ##Disabled
│       │   ├── SSDT-HPET.aml ##Disabled
│       │   ├── SSDT-MCHC.aml
│       │   ├── SSDT-PLUG.aml
│       │   └── SSDT-PMC.aml ##Disabled
│       ├── Drivers
│       ├── Kexts
│       │   ├── AppleALC.kext
│       │   ├── FeatureUnlock.kext 
│       │   ├── IntelMausi.kext
│       │   ├── Lilu.kext
│       │   ├── RealtekRTL8111.kext
│       │   ├── SMCProcessor.kext
│       │   ├── SMCSuperIO.kext
│       │   ├── USBPorts.kext
│       │   ├── USBToolBox.kext
│       │   ├── UTBMap.kext
│       │   ├── VirtualSMC.kext
│       │   └── WhateverGreen.kext
│       ├── OpenCore.efi
│       ├── Resources
│       ├── Tools
│       │   ├── ControlMsrE2.efi
│       │   ├── OpenShell.efi
│       │   └── ResetSystem.efi
│       ├── config.plist
```
 Copy these file to EFI partition to boot your MacOS.

 You can find more details of choice of [SSDTs](https://dortania.github.io/Getting-Started-With-ACPI/ssdt-platform.html) and [Kexts](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#kernel) in the OpenCore install guide.

## Solving the issues
### iGPU HDMI not work
Hackintosh can identify the DP port automatically but not work with HDMI. If you are using the HDMI port for display you will meet nothing in the monitor after the system completed the loading bar and restart.

We need to change the framebuffer for WEG(whatevergreen.kext) and bind the port to the connector in MacOS manully, you can check this for detailed [guide1](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#kernel),[guide2](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#kernel).(Recommand do this via DP to monitor)

Share my config here:
![iGPU](../img/igpu_config.png)

If you see the VRAM is 7MB,please check the SMBIOS if set to close to you build. And check the framebuffer if set as right value Mostly the iGPU was not working.

Full intel GPU guide for whatevergreen: [FAQ.IntelHD](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md)

### Xcode issue
I try to complie a binary by an old version of Xcode but I cannot download it from App Store because the version of MacOS is too old. If you want to install an old version Xcode you need to have a developer account. So I choose upgrade to Sonoma.

### USB mapping
If you want a full experience of Hackintosh, you need to tell the opencore what is the correct port mapping of the USB mapping.
You can use the tool under Win11 PE or do it in pervious Windows OS if you have,[USB-mapping tool](). Here is the [guide](https://dortania.github.io/OpenCore-Post-Install/usb/manual/manual.html). Generally, you need to do these thing:

1. Download the tool and go to windows os(I test it in PE, it's fine)
2. Run the tool and plug in&out with USB 2&3 devices for every usb ports.
3. Copy the generated kext and patch to opencore config.

### HI-DPI for hackintosh

Run this command in terminal [Guide](https://github.com/xzhih/one-key-hidpi) : 
```
bash -c "$(curl -fsSL https://raw.githubusercontent.com/xzhih/one-key-hidpi/master/hidpi.sh)"
```

### HEVC hardware decoding

Remove or comment the item "AAPL,slot-name" from config.plist-Device

### CFGLOCK

Please check this [doc](https://dortania.github.io/OpenCore-Post-Install/misc/msr-lock.html#checking-if-your-firmware-supports-cfg-lock-unlocking) if you need to unlock the options for you BIOS.

### Theme for opencore

Check this: [OpenCore beauty treatment](https://dortania.github.io/OpenCore-Post-Install/cosmetic/gui.html#setting-up-opencore-s-gui)

### Tools for configuration and testing

1. [Hackintool](https://github.com/benbaker76/Hackintool)
2. [opencore configurator](https://mackie100projects.altervista.org/download-opencore-configurator/)
3. [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools)
4. [Geekbench6](https://www.geekbench.com/download/)
5. [Intel Power Gadget](https://www.techspot.com/downloads/7172-intel-power-gadget.html)
6. [VideoProc Converter (test hareware decoding,free trial ok)](https://www.videoproc.com/download.htm?ttpath=site-header)