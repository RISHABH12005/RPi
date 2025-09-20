# Raspberry Pi 3 Model B 

> Comprehensive, concise reference for the Raspberry Pi 3 Model B hardware, ports, architecture.

---

## Overview

The Raspberry Pi 3 Model B is a compact single board computer ideal for learning, prototyping, mbedded projects. It features a Broadcom BCM2837 SoC (quad-core ARM Cortex‑A53), integrated Wi‑Fi and Bluetooth, a 40‑pin GPIO header, and common I/O for displays, cameras, audio, networking, and USB peripherals.

---

## Quick Specs

* **SoC:** Broadcom BCM2837

  * CPU: Quad‑core ARM Cortex‑A53 (ARMv8‑A) @ **1.2 GHz**
  * GPU: Broadcom VideoCore IV
* **RAM:** 1 GB LPDDR2 (shared with GPU)
* **Storage:** microSD (boot + root filesystem)
* **Power:** 5 V via micro‑USB Type‑B (recommended **2.5 A**)
* **Networking:** 10/100 Ethernet, 2.4 GHz 802.11 b/g/n Wi‑Fi, Bluetooth 4.1 + BLE
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
* **Controller:** SMSC LAN9514 (USB hub + Ethernet controller)
* **Throughput:** 10/100 Mbps Fast Ethernet (shared USB 2.0 bandwidth)

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

## Internal Architecture Notes

* The SoC integrates CPU, GPU, and memory controller. The GPU (VideoCore IV) handles multimedia acceleration (H.264 decode, OpenGL ES 2.0).
* USB 2.0 controller and Ethernet share the LAN9514 chip; they share the USB 2.0 bus which caps throughput.
* The CPU is 64‑bit capable but many distributions run 32‑bit userland by default (Raspberry Pi OS legacy images). Use 64‑bit OS images to enable full ARMv8 features.

---

## Quick Start

1. Download a Raspberry Pi OS image (32‑bit or 64‑bit) and flash it to a high‑quality microSD card (use Raspberry Pi Imager or balenaEtcher).
2. Insert microSD, connect HDMI monitor (or DSI display), USB keyboard/mouse, Ethernet or Wi‑Fi, and power via micro‑USB.
3. First boot: complete setup wizard (locale, Wi‑Fi, password). Enable interfaces (Camera, I2C, SPI, Serial) in `raspi-config` if needed.
4. Secure the Pi: change default password, enable firewall or SSH key auth if remote access is required.

---

## Power & Thermal Considerations

* Use a quality 5 V / 2.5 A supply. Voltage drop can cause instability (undervoltage warnings logged). Avoid powering high‑draw USB devices without external powered hub.
* The BCM2837 can run warm under sustained load; passive heat sinks or a small fan are recommended for heavy CPU/GPU tasks.
