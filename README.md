# OpenCore EFI for ASRock H610M-HDV/M.2

Monterey, Ventura and Sonoma OpenCore EFI configuration for ASRock H610M-HDV/M.2

![](https://i.imgur.com/jHFOiBt.png)

---

## System Configuration

* ASRock H610M-HDV/M.2 **Tested on BIOS ver. 4.02 (Factory BIOS), 9.01 - 16.02*
* Intel Core i3-12100F
* Sapphire Pulse RX 560 2G G5 14 CU (45W)
* Team T-create Classic 2*8GB DDR4 3200Mhz
* Adata XPG SX8200 Pro M.2 NVMe 512GB

## Confirmed Working

* AppleID
* Sleep & Wake
* Intel I219-V Ethernet
* Realtek ALC897 Audio **Includes front panel audio*
* All USB Port **Includes front panel USB 2.0 & 3.0*
* All SATA Port
* M.2/NGFF NVMe SSD & WiFi/BT **Need [Specific WiFi Card](https://dortania.github.io/Wireless-Buyers-Guide) & [Specific kext](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#wifi-and-bluetooth)*
* Intel VT, Power Management & Sensors
* Radeon Graphics Acceleration, Power Management & Sensors **Will just work on [Native Radeon GPU](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html#native-amd-gpus)*

## How To

---

### Easy Way to Create a USB Installer on Linux (Can use Live USB)

* Fetch some tools

```bash
mkdir fetch-macOS
cd fetch-macOS
wget https://raw.githubusercontent.com/kholia/OSX-KVM/master/fetch-macOS-v2.py
wget https://github.com/foxlet/macOS-Simple-KVM/raw/master/tools/dmg2img
chmod +x *
```

* Fetch macOS recovery image

```bash
./fetch-macOS-v2.py
```

* Convert dmg to raw img

```bash
./dmg2img BaseSystem.dmg BaseSystem.img
```

* Write to USB

```bash
sudo dd if=BaseSystem.img of=/dev/sdX bs=100M conv=fsync status=progress
```

**Remember sdX is your USB flashdrive device, don't make a mistake or it will destroy your data, use `sudo fdisk -l` to see all list of storage devices*

To create a USB installer on Windows or other OS please refer to [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer).

### Fetch and Place EFI File

* Fetch EFI

```bash
git clone https://github.com/abdul-royyaq/OC-ASRock-H610M-HDV-M.2 --depth 1 
```

* Make EFI partiton

**In some case, EFI partition isn't available.*

```bash
sudo parted /dev/sdX mkpart efi 0% 100%
```

**Remember sdX is your USB flashdrive device, don't make a mistake or it will destroy your data, use `sudo fdisk -l` to see all list of storage devices.*

```bash
sudo mkfs.fat -F 32 /dev/sdXY -n EFI-USB
```

**Remember sdXY is your EFI partion of USB installer, use `sudo fdisk -l` to see all list of storage devices.*

* Mount EFI and copy to EFI Partition

```bash
sudo mount /dev/sdXY /mnt
sudo cp -r OC-ASRock-H610M-HDV-M.2/EFI /mnt
```

**Remember sdXY is your EFI partion of USB installer, use `sudo fdisk -l` to see all list of storage devices.*

For more information please refer to [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/opencore-efi.html).

### Installation

For the installation process please refer to [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html).

**Take a note, please create a EFI partition at lease 200M at partitioning stage.*

### Post-Installation

Install EFI on macOS HDD/SSD.

* Mount EFI partition

Open macOS Terminal and run

```bash
sudo mkdir /Volumes/EFI
sudo mount -t msdos /dev/diskXsY /Volumes/EFI
```

**Remember diskXsY is your EFI disk partiton, use `sudo diskutil list` to see all list of storage devices*

* Copy EFI folder to EFI Partition

```bash
sudo cp -rv /Volumes/EFI-USB/EFI /Volumes/EFI
sudo umount /Volumes/EFI
sudo rm -r /Volumes/EFI
```

Have problems after installation?, please refer to [Dortania OpenCore Post-install](https://dortania.github.io/OpenCore-Post-Install).

## Important Notes

* This EFI comes with a memory mapping template for ASRock H610M-HDV/M.2, [you can change](https://dortania.github.io/OpenCore-Post-Install/universal/memory.html) according to your memory module configuration e.g `Manufacture`, `PartNumber`, `SerialNumber`, `Size`, and `Speed`.

* `CpuTopologyRebuild.kext` is disabled by default, you don't need this if you are using a P-Core only CPU e.g i3-12100/F, this also makes the type 2 hypervisor e.g VirtualBox detect that there are only 2 CPU cores.

* Don't change `MinKernel` variable to 21.x or later, this will make your macOS unable to wake up from sleep.

* Please [generate new SN and MLB](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#using-macserial) if getting trouble with iServices.

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
