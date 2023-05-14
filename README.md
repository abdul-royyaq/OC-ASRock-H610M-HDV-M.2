# OpenCore EFI for ASRock H610M-HDV/M.2

Monterey and Ventura OpenCore EFI configuration for ASRock H610M-HDV/M.2

![](https://i.imgur.com/1N57Sr1.png)

---

### macOS Monterey

![](https://i.imgur.com/PNofAUz.png)

### macOS Ventura

![](https://i.imgur.com/F3W2uMO.png)

---

## System Configuration

* ASRock H610M-HDV/M.2
* Intel Core I3 12100F
* Sapphire Pulse RX 560 2G G5 14 CU (45W) / RX 560 896SP
* Team T-create Classic 2*8GB DDR4 3200Mhz
* Adata SU650 240GB SATA SSD (For Hackintosh installation)
* Team MP33 M.2 512GB PCIe SSD (For Linux installation, detected on macOS)
* Broadcom BCM43142 802.11 bgn Wi-Fi M.2 (From old HP Notebook, *Only for network lab on GNU/Linux)

## Confirmed Working

* Sleep and Wake
* Intel I219-V Ethernet
* Intel HD and Realtek AC-79 Audio
* All USB Port
* All SATA Port (AHCI mode)
* NVME SSD
* Intel and Radeon Sensors
* Intel CPU Power Management
* Broadcom BCM43142 (only) Bluetooth Works in Monterey with [BrcmPatchRAM3](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#broadcom) (AirDrop not supported by adapter)

## How To

---

### Create USB Installer

To create a USB installer please refer to [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer).

### Fetch and Place EFI File

* Download this [OpenCore EFI for ASRock H610M-HDV/M.2](https://github.com/abdul-royyaq/OC-ASRock-H610M-HDV-M.2/archive/refs/heads/main.zip).

* Extract archived file then place `EFI` folder into the EFI partition on the USB installer, for more information please refer to [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/opencore-efi.html).

### Installation

For the installation process please refer to [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html).

---

## OpenCore Recipe (Source and Credit)

* [OpenCore](https://github.com/acidanthera/OpenCorePkg)
* [BsxM1](https://github.com/blackosx/BsxM1)
* [AppleALC](https://github.com/acidanthera/AppleALC)
* [CpuTopologyRebuild](https://github.com/b00t0x/CpuTopologyRebuild)
* [IntelMausi](https://github.com/acidanthera/IntelMausi)
* [Lilu](https://github.com/acidanthera/Lilu)
* [NVMeFix](https://github.com/acidanthera/NVMeFix)
* [RadeonSensor](https://github.com/aluveitie/RadeonSensor)
* [RestrictEvents](https://github.com/acidanthera/RestrictEvents)
* [SMCRadeonGPU](https://github.com/aluveitie/RadeonSensor) (part of RadeonSensor)
* [SMCSuperIO](https://github.com/acidanthera/VirtualSMC) (part of VirtualSMC)
* [VirtualSMC](https://github.com/acidanthera/VirtualSMC)
* [WhateverGreen](https://github.com/acidanthera/WhateverGreen)

----
