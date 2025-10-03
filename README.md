# OpenCore EFI for ASRock H610M-HDV/M.2

Monterey, Ventura, Sonoma, Sequoia and (partially) Tahoe OpenCore EFI configuration for ASRock H610M-HDV/M.2

![](https://i.imgur.com/jHFOiBt.png)

---

## System Configuration

* ASRock H610M-HDV/M.2 **Tested on BIOS ver. 4.02 (factory BIOS), 9.01 - 19.03*
* Intel Core i3-12100F
* Sapphire Pulse RX 560 2G G5 14 CU (45W)
* Team T-create Classic 2*8GB DDR4 3200Mhz
* SK hynix BC901 NVMe 256GB

## Confirmed Working

* AppleID
* Sleep & wake
* Intel I219-V ethernet
* Realtek ALC897 audio **Includes front panel audio*
* All USB ports **Includes front panel USB 2.0 & 3.0*
* All SATA ports
* M.2/NGFF NVMe SSD & WiFi/BT **Need specific [WiFi card](https://dortania.github.io/Wireless-Buyers-Guide) & [kext](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#wifi-and-bluetooth)*
* Intel VT, power management & sensors
* Radeon graphics acceleration, power management & sensors **Will just work on [native Radeon GPU](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html#native-amd-gpus)*

## Create macOS USB installer

You can follow [Dortania's guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer) or follow this easy guide

### Create a macOS recovery USB on Windows (Easy way, not really)

* Fetch macOS recovery image

First download and install [Python 3](https://www.python.org/downloads), then open PowerShell and run

```bash
mkdir 'C:\macOS Recovery'
cd 'C:\macOS Recovery'
Invoke-WebRequest -Uri 'https://raw.githubusercontent.com/kholia/OSX-KVM/master/fetch-macOS-v2.py' -OutFile 'C:\macOS Recovery\fetch-macOS-v2.py'
py fetch-macOS-v2.py
```

* Fetch EFI

```bash
Invoke-WebRequest -Uri 'https://github.com/abdul-royyaq/OC-ASRock-H610M-HDV-M.2/archive/refs/heads/main.zip' -OutFile 'C:\macOS Recovery\main.zip'
Expand-Archive -Path 'C:\macOS Recovery\main.zip' -DestinationPath 'C:\macOS Recovery'
```

* Create USB recovery

```bash
Format-Volume -DriveLetter M -FileSystem FAT32 -NewFileSystemLabel "MACOS-USB" -Force -Confirm:$false
mkdir 'M:\com.apple.recovery.boot'
Copy-Item -Path 'C:\macOS Recovery\BaseSystem*' -Destination 'M:\com.apple.recovery.boot' -Recurse
Copy-Item -Path 'C:\macOS Recovery\OC-ASRock-H610M-HDV-M.2-main\EFI' -Destination 'M:\EFI' -Recurse
Get-WmiObject -Query "SELECT * FROM Win32_Volume WHERE DriveLetter = 'M:'" | ForEach-Object { $_.Dismount($true, $true) }
```

**Remember disk X is your USB device, be careful you can destroy your data, use diskpart `list disk` to see all list of storage devices.*

### Create a macOS recovery USB on Linux (Easy way)

* Fetch macOS recovery image

Open Linux terminal and run

```bash
mkdir macOS\ Recovery
cd macOS\ Recovery
wget https://raw.githubusercontent.com/kholia/OSX-KVM/master/fetch-macOS-v2.py
python fetch-macOS-v2.py
```


* Fetch EFI

```bash
wget https://github.com/abdul-royyaq/OC-ASRock-H610M-HDV-M.2/archive/refs/heads/main.zip
unzip main.zip
```

* Create USB recovery

```bash
sudo mkfs.fat -F 32 /dev/sdX -n 'MACOS-USB'
sudo mount /dev/sdX /mnt
sudo mkdir /mnt/com.apple.recovery.boot
sudo cp -r BaseSystem.* /mnt/com.apple.recovery.boot/
sudo cp -r OC-ASRock-H610M-HDV-M.2-main/EFI /mnt
sudo unmount /mnt
```

**Remember sdX is your USB device, be careful you can destroy your data, use `sudo fdisk -l` to see all list of storage devices.*

## Installation

For the installation process please refer to [Dortania's guide](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#booting-the-opencore-usb).

**Take a note, please create a EFI partition at lease 200M at partitioning stage.*

## Post-installation

Install EFI on macOS HDD/SSD.

* Mount EFI partition

Open macOS terminal and run

```bash
sudo mkdir /Volumes/EFI
sudo mount -t msdos /dev/diskXsY /Volumes/EFI
```

**Remember diskXsY is your EFI disk partiton, use `sudo diskutil list` to see all list of storage devices*

* Copy EFI folder to EFI partition

```bash
sudo cp -rv /Volumes/MACOS-USB/EFI /Volumes/EFI
sudo umount /Volumes/EFI
sudo rm -r /Volumes/EFI
```

Have problems after installation?, please refer to [Dortania's guide](https://dortania.github.io/OpenCore-Post-Install).

## Important Notes

* `CpuTopologyRebuild.kext` is disabled by default, enable it if you have a CPU with P-Core and E-Core.

* If getting trouble with iServices generate new SMBIOS using macserial utility.

```bash
./macserial --model "MacPro7,1"
```

Output will looks like this (SN left, MLB right):

```bash
F5KGLNYDP7QM | F5K143802GUK3F7AD
F5KCFCZUP7QM | F5K0112074NK3F7JA
F5KF6NY6P7QM | F5K105609GUK3F78C
F5KH9JZBP7QM | F5K208101CDK3F7UE
F5KJV4ZEP7QM | F5K251100GUK3F71H
F5KLDVZFP7QM | F5K3373104NK3F7A8
F5KZ40Y7P7QM | F5K930102GUK3F78C
F5KL1HYEP7QM | F5K3273064NK3F78C
F5KK9QY5P7QM | F5K308600J9K3F7AD
F5KKF0WPP7QM | F5K3115014NK3F71M
```

* macOS Tahoe recovery experiencing problem with GPU acceleration enabled, disable `WhateverGreen.kext` first to start fresh install of macOS Tahoe.

* There is way to get macOS Tahoe recovery image (if `fetch-macOS-v2.py` utility didnt provide), using macrecovery utility.

```
python macrecovery.py -b Mac-CFF7D910A743CAAF -m 00000000000000000 -os latest download
```

---

## LICENSE & CREDITS

This project is licensed under the [MIT License](https://opensource.org/license/mit).

This project includes or depends on these following projects with subject to their respective licenses:

* [AppleALC](https://github.com/acidanthera/AppleALC)
* [BsxM1](https://github.com/blackosx/BsxM1)
* [CpuTopologyRebuild](https://github.com/b00t0x/CpuTopologyRebuild)
* [IntelMausi](https://github.com/acidanthera/IntelMausi)
* [Lilu](https://github.com/acidanthera/Lilu)
* [NVMeFix](https://github.com/acidanthera/NVMeFix)
* [OcBinaryData](https://github.com/acidanthera/OcBinaryData)
* [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg)
* [rEFInd](https://sourceforge.net/p/refind)
* [RestrictEvents](https://github.com/acidanthera/RestrictEvents)
* [SMCRadeonSensors](https://github.com/ChefKissInc/SMCRadeonSensors)
* [VirtualSMC](https://github.com/acidanthera/VirtualSMC)
* [WhateverGreen](https://github.com/acidanthera/WhateverGreen)

----
