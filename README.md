Asus-S500CA-OSX
===============

Guide for installing OSX Mavericks 10.9.4 on Asus VivoBook S500CA/V500CA
The Asus S500CA is a great looking laptop, feels like the real thing.
I bought it the knowing that hackintoshing it won't be easy, as several users reported - many power issues and such.
Anyway, I took the challenge and got it last week :)

So here goes..

### Spec
- Asus VivoBook S500CA/V500CA
- CPU: i7 3537U 2.0Ghz Ivy Bridge
- Chipset: Intel HM76 Express
- GPU: Intel HD 4000
- Touch Screen: Atmel maXTouch Digitizer 880a
- Max Res: 1366x768x32
- Audio: ALC269
- Ethernet: Atheros AR8161
- WIFI: Atheros AR9485

### What's Working?!

- Fully supported power management with following P states: 8, 16, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 31
- Sleep (+wake by lid)
- Graphics
- Touch Screen!
- Audio (still with issues)
- Ethernet
- Bluetooth
- Battery Indicator
- Trackpad
- Webcam
- VGA port
- FN Keys

### Whats NOT Working?!
- Internal wifi (i'm using D-Link DWA-133 instead)
- No speakers sound after wake from sleep - headphones does work after sleep.

### Whats not tests?
- HDMI Video/Audio
- SD Card

Ok, good enough for me, now tell me how to install the damn thing.

### Tools needed
- UniBeast USB with Mavericks 10.9.4 (not lower!)
- MultiBeast
- Kext Wizard
- Chameleon Wizard
- MaciASL
- Clover
- Clover Configurator
- DPCIManager
- Intel Power Gadget
- GeekBench
- A human brain (optional)

## Overview
1. BIOS setup
2. UniBeast installation
3. Install Kexts
4. Patch DSDT
5. Install Clover
6. Verification

### 1. BIOS Setup
- Hit F2 to enter BIOS
- Advanced -> VT-d -> Disabled
- Security -> Secure Boot Control -> Disabled
- Save & Exit -> Save Changes and Exit
- Hit F2 to enter BIOS
- Boot -> Launch CSM -> Enabled
- Boot -> Add new Boot Option
- Add boot option -> “EFI” (you may call it whatever)
- Select Filesystem -> just make sure you have something like PCI(1F|2)\DevicePath(Type 3,…..
- Path for boot option -> \EFI\BOOT\BOOTX64.EFI
- Create
- Save & Exit -> Save Changes and Exit

## 2. UniBeast Installation
- Insert UniBeast USB and boot into Mavericks installer, no flags are required, at least wasn't in my case.
If installer doesn’t start, check your BIOS settings again or try GraphicsEnabler=Yes, etc.
- Once the installation is finished; reboot.
- Boot using UniBeast USB again but select your HD with flags -x -f.

## 3. Install Kexts
- Run MultiBeast with following:
-	  Drivers -> Misc -> FakeSMC
- 	Drivers -> Misc -> FakeSMC Plugins
- 	Drivers -> Misc -> FakeSMC HWMonitor Application
- 	Drivers -> Misc -> USB 3.0 - Universal
- 	Drivers -> Network -> Atheros -> ALXEthernet
- 	Drivers -> System -> Patched AppleIntelCPUPowerManagement -> OS X 10.9.0
- 	BootLoadres -> Chimera vX.Y.Z
- 	Customize -> Boot options -> Basic Boot Options
- 	Customize -> Boot options -> Generate CPU States
- 	Customize -> Boot options -> Hibernate mode - Laptop
- 	Customize -> Boot options -> Verbose boot
- 	Customize -> Boot options -> System Definition -> Mac mini 6,2
- Build

#### Download following kexts:
- Latest VoodooHDA
- ELAN Touchpad: google 1948-elan-touchpad-driver-mac-os-x
- Battery Indicator: [url]https://bitbucket.org/RehabMan/os-x-acpi-battery-driver/downloads[/url]
- FN Keys: google 1968-fn-hotkey-driver-for-asus-notebooks
- Touch screen (not free, only optional and at your own risk): [url]http://www.touch-base.com/[/url]

Use KextsWizard to install and rebuild cache + permissions.

### 4. Patch DSDT
- Run MaciASL
- Preferences -> iASL -> ACPI 5.0
- Preferences -> Sources -> +
- 	name=repo
- 	URL=http://raw.github.com/RehabMan/Laptop-DSDT-Patch/master
- Close Preferences
- Patch -> "Fix php/pnp lower case Error” -> Apply -> Close -> File -> Save As -> /Extra/Vanila-DSDT.aml
- Patch -> HD4000 Low Resolution -> Apply
- Patch -> ASUS N55SL/VivoBook -> Apply
- Patch -> DTGP -> Apply -> Close -> Compile -> File -> Save As -> /Extra/DSDT.aml

Reboot using UniBeast USB again but select your HD with -f

You should have full graphics support and everything else working except full power management, will be achieved after installing Clover.

###5. Install Clover
TBD

###6. Verification
TBD
