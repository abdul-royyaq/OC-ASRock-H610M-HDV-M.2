# OpenCore EFI for ASRock H610M-HDV/M.2

Monterey and Ventura OpenCore EFI configuration for ASRock H610M-HDV/M.2

![](https://i.imgur.com/7e2sFKK.png)

---

## System Configuration

* ASRock H610M-HDV/M.2
* Intel Core i3-12100F
* Sapphire Pulse RX 560 2G G5 14 CU (45W)
* Team T-create Classic 2*8GB DDR4 3200Mhz
* Adata SU650 SATA 240GB (Hackintosh)
* Team MP33 M.2 NVMe 512GB (ArchLinux)

## Confirmed Working

* Sleep and Wake
* Intel I219-V Ethernet
* Intel HDA & Realtek ALC897 Audio
* USB
* SATA
* NVMe/NGFF SSD & WiFi ([Specific WiFi Card](https://dortania.github.io/Wireless-Buyers-Guide))
* Intel & Radeon Power Management & Sensors

## How To

---

### Create USB Installer (Linux, EZ way)

* Fetch some tools

```bash
mkdir fetch-macOS &&
cd fetch-macOS &&
wget https://raw.githubusercontent.com/kholia/OSX-KVM/master/fetch-macOS-v2.py &&
wget https://github.com/foxlet/macOS-Simple-KVM/raw/master/tools/dmg2img &&
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
sudo dd if=BaseSystem.img of=/dev/sdX status=progress
```

`*Remember sdX is your USB flashdrive device, don't make a mistake or it will destroy your data, use 'sudo fdisk -l' to see all list of storage devices`

To create a USB installer on Windows or other OS please refer to [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer).

### Fetch and Place EFI File

* Fetch EFI

```bash
git clone https://github.com/abdul-royyaq/OC-ASRock-H610M-HDV-M.2 --depth 1 
```

* Mount EFI and copy to EFI Partition

```bash
sudo mount /dev/sdX /mnt
cp -r OC-ASRock-H610M-HDV-M.2/EFI /mnt
```

`*Remember sdX is your EFI partion of USB installer, use 'sudo fdisk -l' to see all list of storage devices`

Or/If in other OS

* Manually download this [OpenCore EFI for ASRock H610M-HDV/M.2](https://github.com/abdul-royyaq/OC-ASRock-H610M-HDV-M.2/archive/refs/heads/main.zip).

* Extract archived file then place `EFI` folder into the EFI partition on the USB installer.

For more information please refer to [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/opencore-efi.html).

### Installation

For the installation process please refer to [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html).

`*Take a note, please create a EFI partition at lease 200M at partitioning stage.`

### Post-Installation

After installation, don't forget to copy `EFI` folder from USB installer to the EFI partition on the HDD/SSD where the macOS is installed.

* Mount EFI partition

Open Terminal and run

```bash
sudo diskutil mount diskXsY
```

`*Remember diskXsY is your EFI disk partiton, use 'sudo diskutil list' to see all list of storage devices`

* Copy EFI folder EFI Partition

Manually copy EFI folder from USB installer to EFI partition.

Have problem(s) after installation?, please refer to [Dortania OpenCore Post-install](https://dortania.github.io/OpenCore-Post-Install)

---

## OpenCore Recipe (Sources and Credits)

* [OpenCore](https://github.com/acidanthera/OpenCorePkg)
* [BsxM1](https://github.com/blackosx/BsxM1)
* [OcBinaryData](https://github.com/acidanthera/OcBinaryData)
* [btrfs_x64.efi](https://sourceforge.net/p/refind) (rEFInd)
* [AppleALC](https://github.com/acidanthera/AppleALC)
* [CpuTopologyRebuild](https://github.com/b00t0x/CpuTopologyRebuild)
* [IntelMausi](https://github.com/acidanthera/IntelMausi)
* [Lilu](https://github.com/acidanthera/Lilu)
* [NVMeFix](https://github.com/acidanthera/NVMeFix)
* [RadeonSensor](https://github.com/aluveitie/RadeonSensor)
* [RestrictEvents](https://github.com/acidanthera/RestrictEvents)
* [SMCProcessor](https://github.com/acidanthera/VirtualSMC) (VirtualSMC)
* [SMCRadeonGPU](https://github.com/aluveitie/RadeonSensor) (RadeonSensor)
* [SMCSuperIO](https://github.com/acidanthera/VirtualSMC) (VirtualSMC)
* [VirtualSMC](https://github.com/acidanthera/VirtualSMC)
* [WhateverGreen](https://github.com/acidanthera/WhateverGreen)

----
