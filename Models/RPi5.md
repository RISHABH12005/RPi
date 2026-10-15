# Raspberry Pi 5

> Comprehensive reference for the Raspberry Pi 5 hardware, ports, and architecture.

---

## Overview

The Raspberry Pi 5 is the latest single-board computer in the Raspberry Pi lineup, offering significant performance improvements, better connectivity, and advanced I/O options. It is suitable for desktop use, AI/ML prototyping, and high-performance embedded projects.

---

## Quick Specs

* **SoC:** Broadcom BCM2712
  * CPU: Quad-core ARM Cortex-A76 (ARMv8.2-A) @ **2.4 GHz**
  * GPU: Broadcom VideoCore VII
* **RAM:** 4 GB / 8 GB LPDDR5 / 16GB LPDDR5
* **Storage:** microSD (boot + root filesystem), USB boot, NVMe support via PCIe 2.0 (via compute module or adapter)
* **Power:** 5 V via USB-C (5.0 A recommended for full load)
* **Networking:** Gigabit Ethernet, Wi-Fi 6 (802.11ax), Bluetooth 5.2 + BLE
* **Ports:** 2 × micro-HDMI 2.0, DSI (15-pin), CSI (15-pin), 2 × USB 3.0, 2 × USB 2.0, 3.5 mm audio jack, microSD slot
* **GPIO:** 40-pin header (3.3 V logic)

---

## Ports & Interfaces (Detailed)

### HDMI

* **Type:** 2 × micro-HDMI 2.0
* **Max:** Dual 4Kp60 displays
* Supports digital audio and video, CEC, HDR, and HDCP 2.3.

### Display (DSI)

* **Connector:** 15-pin FFC (MIPI DSI)
* Compatible with official Raspberry Pi touchscreens and low-latency DSI displays.

### Camera (CSI)

* **Connector:** 15-pin FFC (MIPI CSI-2)
* Supports Raspberry Pi Camera Modules up to 8K video (module dependent).

### Ethernet

* **Connector:** RJ45
* **Controller:** Dedicated Gigabit Ethernet PHY, full bandwidth independent of USB.
* **PoE:** Supported via PoE HAT and 4-pin header.

### USB

* **2 × USB 3.0 Type-A, 2 × USB 2.0 Type-A**
* USB 3.0 ports provide high-speed data transfer (up to 5 Gbps). Power draw depends on PSU and connected peripherals.

### Audio / Composite

* **3.5 mm TRRS** jack provides analog stereo audio and composite video output.
* Pinout: Tip = Left, Ring1 = Right, Ring2 = Ground, Sleeve = Composite Video.

### microSD Slot

* Primary boot medium; supports high-speed UHS-I cards. USB boot also supported.

### Power Input (USB-C)

* **5 V** recommended, up to **5.0 A** for heavy workloads.
* Requires proper USB-C cable to avoid undervoltage or instability.

### GPIO Header (40 pins)

* **Voltage logic:** 3.3 V
* Interfaces: I²C, SPI, UART, PWM, digital GPIO, 5V/3.3V power pins, GND pins
* Compatible with HATs using standard EEPROM spec.

---

## Internal Architecture Notes

* The BCM2712 integrates high-performance CPU cores (Cortex-A76), GPU, and memory controller supporting LPDDR5.
* USB 3.0 and Gigabit Ethernet run on separate high-speed buses for maximum throughput.
* GPU supports advanced graphics, video decoding (8K H.265/VP9), and OpenGL ES 3.x.
* CPU is 64-bit and fully supported by modern OS images (Raspberry Pi OS 64-bit, Ubuntu, etc.).

---

## Power & Thermal Considerations

* Use a quality 5 V / 5 A USB-C PSU. High-performance workloads require sufficient power and proper cable.
* High-speed CPU/GPU can run hot; heatsinks or active cooling recommended for heavy compute or 8K video tasks.

---
