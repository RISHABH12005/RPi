# Raspberry Pi 4 Model B

> Comprehensive reference for the Raspberry Pi 4 Model B hardware, ports, architecture.

---

## Overview

The Raspberry Pi 4 Model B is a powerful single-board computer suitable for learning, prototyping, and embedded projects. It features a Broadcom BCM2711 SoC (quad-core ARM Cortex-A72), up to 8 GB RAM, USB 3.0 support, dual-display output, and improved networking.

---

## Quick Specs

* **SoC:** Broadcom BCM2711

  * CPU: Quad-core ARM Cortex-A72 (ARMv8-A) @ **1.5 GHz**
  * GPU: Broadcom VideoCore VI
* **RAM:** 2 GB / 4 GB / 8 GB LPDDR4
* **Storage:** microSD (boot + root filesystem), USB boot support
* **Power:** 5 V via USB-C (3.0 A recommended)
* **Networking:** Gigabit Ethernet, Dual-band Wi-Fi 802.11 b/g/n/ac (2.4/5 GHz), Bluetooth 5.0 + BLE
* **Ports:** 2 × micro-HDMI, DSI (15-pin), CSI (15-pin), 2 × USB 3.0, 2 × USB 2.0, 3.5 mm audio jack, microSD slot
* **GPIO:** 40-pin header (3.3 V logic)

---

## Ports & Interfaces (Detailed)

### HDMI

* **Type:** 2 × micro-HDMI
* **Max:** 4Kp60 (1 × 4Kp60 or dual 4Kp30)
* Carries digital audio and video. Supports CEC and HDMI DDC.

### Display (DSI)

* **Connector:** 15-pin FFC (MIPI DSI)
* For official Raspberry Pi touchscreen; low-latency direct connection.

### Camera (CSI)

* **Connector:** 15-pin FFC (MIPI CSI-2)
* Supports Raspberry Pi Camera Modules up to 1080p @ 30 fps.

### Ethernet

* **Connector:** RJ45
* **Controller:** Broadcom BCM54213PE Gigabit Ethernet PHY
* **Throughput:** Full Gigabit via dedicated bus (not shared with USB)
* **PoE:** Supported with PoE HAT via 4-pin PoE header

### USB

* **2 × USB 3.0 Type-A, 2 × USB 2.0 Type-A**
* USB 3.0 provides up to 5 Gbps; USB 2.0 remains 480 Mbps.
* Power draw across ports; use quality PSU for high-current peripherals.

### Audio / Composite

* **3.5 mm TRRS** jack provides analog stereo audio and composite video output.
* Pinout: Tip = Left, Ring1 = Right, Ring2 = Ground, Sleeve = Composite Video.

### microSD Slot

* Primary boot medium; supports high-capacity UHS-I cards.
* Can also boot from USB devices with appropriate firmware.

### Power Input (USB-C)

* **5 V** recommended, **3.0 A** supply
* Proper USB-C cable required; insufficient power can cause instability.

### GPIO Header (40 pins)

* **Voltage logic:** 3.3 V
* Interfaces: I²C, SPI, UART, PWM, digital GPIO, 5V/3.3V power pins, GND pins
* Compatible with standard HATs with EEPROM.

---

## Internal Architecture Notes

* SoC integrates CPU, GPU, and memory controller; supports hardware acceleration for video and graphics.
* USB 3.0 ports connect via dedicated PCIe lanes, avoiding USB 2.0 bottlenecks.
* Gigabit Ethernet has full bandwidth, independent of USB bus.
* CPU is 64-bit capable; many distributions support 64-bit userland (Raspberry Pi OS 64-bit recommended for full performance).

---

## Common Use Cases

* Desktop replacement (Raspberry Pi OS, Ubuntu, etc.)
* Media center with 4K dual displays
* Home server, network-attached storage (NAS)
* Robotics, IoT, and sensor integration via GPIO/HATs
* High-speed data acquisition and AI/ML prototyping

---

## Quick Start

1. Download Raspberry Pi OS or compatible image (64-bit recommended) and flash to high-quality microSD card.
2. Insert microSD, connect HDMI displays (or DSI touchscreen), USB keyboard/mouse, Ethernet or Wi-Fi, and power via USB-C.
3. First boot: complete setup wizard (locale, Wi-Fi, password), enable interfaces in `raspi-config` if needed.
4. Secure Pi: change default password, enable SSH key auth or firewall if remote access is needed.

---

## Power & Thermal Considerations

* Use a quality 5 V / 3 A USB-C PSU. Voltage drop or underpowered cables can cause instability.
* BCM2711 runs hotter under heavy load; heat sinks or fan recommended for sustained 4K video or CPU-intensive tasks.
