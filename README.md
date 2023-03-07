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
* Team T-create Clasic 2*8GB DDR4 3200Mhz
* Broadcom BCM43142 802.11 bgn Wi-Fi M.2 (From Old HP Notebook, *Only for network lab on GNU/Linux)

## Confirmed Working

* Sleep and Wake
* Intel I219-V Ethernet
* Intel HD and Realtek AC-79 Audio
* All USB Port
* Intel and Radeon Sensors
* Intel CPU Power Management
* Broadcom BCM43142 (only) Bluetooth Works in Monterey with [BrcmPatchRAM3](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#broadcom) (AirDrop not supported by adapter)

---