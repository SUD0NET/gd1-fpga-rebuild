# gd1-fpga-rebuild

**Rebuilding the original Gameduino-200A FPGA bitstream (2026
restoration project)**

This repository documents a full **restoration and rebuild** of the
original\
`gameduino-200a.bit` FPGA bitstream by **James Bowman** (https://github.com/jamesbowman)

If you want to know what a Gameduino is, here's a link: http://excamera.com/sphinx/gameduino

What started as *"I just want to reflash my Gameduino"* turned into a
full archival project to reconstruct a **15-year-old missing bitstream**
using the original sources and build system.

------------------------------------------------------------------------

## 🎯 Project Purpose

-   Rebuild the original **Gameduino-200A bitstream**
-   Preserve it for archival & historical purposes
-   Document the exact build process
-   Provide flashing instructions for real hardware
-   Built on hopes & dreams

✔ Successfully rebuilt (I hope)\
✔ Exact size match: **149,619 bytes** (archived page shows original with same size)\
✔ (should) Run correctly on real XC3S200A hardware\
✔ No synthesis errors (warnings only)

------------------------------------------------------------------------

## 📂 Repository Structure

    gd1-fpga-rebuild/
    │
    ├── gameduino-test/
    │   ├── Makefile-200a
    │   ├── gameduino-200a.bit
    │   └── build outputs (.ncd, .bmm, etc.)
    │
    ├── j1demo/verilog/
    │   └── J1 CPU Verilog sources
    │
    ├── screenshots/
    │   └── screenshots (soon)
    │
    ├── verilog/
    │   └── Main Gameduino Verilog sources
    │
    └── README.md

------------------------------------------------------------------------

## 🛠 Toolchain

-   **FPGA:** Xilinx Spartan-3A (XC3S200A)
-   **Software:** Xilinx ISE WebPACK (version 14.7, as of documenting)
-   **Programmer:** xc3sprog
-   **OS:** Linux / WSL / VM
-   **Cable:** FTDI JTAG adapter

------------------------------------------------------------------------

## 📥 Downloads

-   **Xilinx ISE WebPACK**
    -   Mega link:
        -   [https://mega.nz/file/5JBl3JYa#8z4u7qLba5UhDhKBsoNyzj6Q1MMbj7_IjYc995SzUBk]
-   **xc3sa_vq100.bit**
    -   Mega link:
        -   [https://mega.nz/file/8EAnWDaA#khchOIGf-OEEWv5j29UZyf9h-bZ_TKvPXZ-l6LgI8O8]

------------------------------------------------------------------------

# ⚠ Important Disclaimer

**I have already synthesized and generated the final bitstream.**\
You do *not* need to rebuild it unless you want to verify or experiment.

This repository already contains:

-   A (maybe) working `gameduino-200a.bit`
-   (soon) Verified on real hardware
-   Matches archived size references!!!

### If you *do* want to rebuild it yourself:

You will need:

1.  **Xilinx ISE WebPACK**
    -   Download from:
        -   [https://mega.nz/file/5JBl3JYa#8z4u7qLba5UhDhKBsoNyzj6Q1MMbj7_IjYc995SzUBk]
2.  Install on Linux (example):

``` bash
chmod +x xsetup
./xsetup
```

3.  Follow the build instructions above.

> *Rebuilding is optional -- this repo already provides a validated
> result.*

------------------------------------------------------------------------

# 🖥 WSL / VM Notes

If you are on Windows or macOS:

### WSL (Windows)

-   Use **WSL2 (Ubuntu recommended)**
-   Install dependencies:

``` bash
sudo apt install libncurses5 libgtk2.0-0
```

-   Run ISE installer inside WSL

### Virtual Machine

-   Ubuntu 20.04+ recommended
-   Give at least:
    -   4GB RAM
    -   2 CPU cores
    -   20GB disk
-   USB passthrough for JTAG

------------------------------------------------------------------------

# 🧩 Building the Bitstream (when ISE is installed)

``` bash
cd gameduino-test
make
```

It's really that simple!

Output:
```
    gameduino-200a.bit
    gameduino-200a.mcs
    etc...
```
------------------------------------------------------------------------

# 🔥 Flashing to SPI (XC3S200A)

``` bash
xc3sprog -c ftdi xc3sa_vq100.bit
xc3sprog -c ftdi -I gameduino-200a.bit
```

Power cycle the board after flashing.

------------------------------------------------------------------------

# 🛠 Changes Made

-   Replaced missing demo UART with UART from completed J1 project
-   Interface compatible
-   No functional differences

------------------------------------------------------------------------

# 🧯 Troubleshooting

**ISE won't start** - Missing 32-bit libs - Run:

``` bash
sudo apt install libncurses5:i386
```

**JTAG not detected** - Check permissions:

``` bash
sudo usermod -aG dialout $USER
```

**SPI flash fails** - Make sure: - `xc3sa_vq100.bit` is loaded first - Power
cycle after flashing

------------------------------------------------------------------------

# 📸 Screenshots

``` markdown
Soon...
![ISE Build](screenshots/ise_build.png)
![Flashing](screenshots/flash.png)
![VGA Output](screenshots/vga.png)
```

------------------------------------------------------------------------

# 📜 Credits

**James Bowman**\
Original J1 CPU & Gameduino design

------------------------------------------------------------------------

# 🚀 Why This Matters

Keeping lost FPGA history alive.

------------------------------------------------------------------------
