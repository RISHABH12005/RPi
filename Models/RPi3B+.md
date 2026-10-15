# Raspberry Pi 3 Model B+

> Comprehensive, concise reference for the Raspberry Pi 3 Model B+ hardware, ports, and architecture.

---

## Overview

The Raspberry Pi 3 Model B+ is a compact single-board computer ideal for learning, prototyping, and embedded projects. It features a Broadcom BCM2837B0 SoC (quad-core ARM Cortex‑A53), integrated Wi‑Fi and Bluetooth, a 40‑pin GPIO header, and common I/O for displays, cameras, audio, networking, and USB peripherals.

---

## Quick Specs

* **SoC:** Broadcom BCM2837B0
  * CPU: Quad‑core ARM Cortex‑A53 (ARMv8‑A) @ **1.4 GHz**
  * GPU: Broadcom VideoCore IV
* **RAM:** 1 GB LPDDR2 (shared with GPU)
* **Storage:** microSD (boot + root filesystem)
* **Power:** 5 V via micro‑USB Type‑B (recommended **2.5 A**)
* **Networking:** Gigabit Ethernet (300 Mbps effective, via USB 2.0 bus), Dual‑band Wi‑Fi (2.4/5 GHz), Bluetooth 4.2
* **Ports:** HDMI (full‑size), DSI (15‑pin), CSI (15‑pin), 4 × USB 2.0, 3.5 mm TRRS (audio + composite), microSD slot
* **GPIO:** 40‑pin header (3.3 V logic)

---

## Ports & Interfaces (Detailed)

### HDMI

* **Type:** Full‑size HDMI 1.3a
* **Max:** 1920×1200 @ 60 Hz
* Carries audio and video. Supports HDMI‑CEC on compatible displays.

### Display (DSI)

* **Connector:** 15‑pin FFC (MIPI DSI)
* Used to connect official Raspberry Pi touchscreen displays. Lower latency than HDMI for attached DSI displays.

### Camera (CSI)

* **Connector:** 15‑pin FFC (MIPI CSI‑2)
* For Raspberry Pi Camera Modules; supports typical modules up to 1080p @ 30 fps (module dependent).

### Ethernet

* **Connector:** RJ45
* **Controller:** LAN7515 (USB hub + Ethernet bridge)
* **Throughput:** Limited by internal USB 2.0 bus — realistic throughput ≈ **300 Mbps**.
* **PoE:** Supported via a PoE HAT and 4‑pin PoE header (HAT required).

### USB

* **4 × USB 2.0 Type‑A** ports
* Shared USB 2.0 bandwidth; power draw shared across ports (ensure adequate PSU).

### Audio / Composite

* **3.5 mm TRRS** jack provides analog stereo audio and composite video output.
* Pinout: Tip = Left, Ring1 = Right, Ring2 = Ground, Sleeve = Composite Video.

### microSD Slot

* Primary boot medium. Partition layout: FAT32 boot partition + EXT4 root filesystem (typical).
* Use good quality, high‑endurance cards for reliability.

### Power Input (Micro USB B)

* **5 V** recommended, **2.5 A** supply to handle USB peripherals and HATs.
* Board includes polyfuse and basic protection.

### GPIO Header (40 pins)

* **Voltage logic:** 3.3 V (do not exceed)
* **Notable interfaces:**

  * I²C: SDA (GPIO2), SCL (GPIO3)
  * SPI: MOSI, MISO, SCLK, CE0, CE1
  * UART: TXD0 (GPIO14), RXD0 (GPIO15)
  * PWM: available on certain GPIOs
  * Power: 5 V (pins 2, 4), 3.3 V (pins 1, 17), multiple GND pins
* Compatible with HATs that follow the EEPROM HAT spec.

---

## Internal Architecture

* The SoC integrates CPU, GPU, and memory controller. The GPU (VideoCore IV) handles multimedia acceleration (H.264 decode, OpenGL ES 2.0).
* USB 2.0 controller and Ethernet are connected through the LAN7515 chip; they share the USB 2.0 bus which caps throughput.
* The CPU is 64‑bit capable but many distributions run 32‑bit userland by default (Raspberry Pi OS legacy images). Use 64‑bit OS images to enable full ARMv8 features.

---

## Power & Thermal Considerations

* Use a quality 5 V / 2.5 A supply. Voltage drop can cause instability (undervoltage warnings logged). Avoid powering high‑draw USB devices without external powered hub.
* The BCM2837B0 can run warm under sustained load; passive heat sinks or a small fan are recommended for heavy CPU/GPU tasks.
