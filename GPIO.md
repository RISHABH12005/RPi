# RPi Interfaces & Signals

```text
Raspberry Pi 40-pin Header
├── Power Supply
│   ├── 5 V Power
│   │   ├── Direct from USB power input
│   │   ├── Powers motors, sensors, displays (with regulator)
│   │   └── Cannot be switched by software
│   ├── 3.3 V Power
│   │   ├── Generated on-board from 5 V
│   │   ├── Powers GPIO logic, ICs, sensors
│   │   └── Cannot be switched by software
│   └── Ground (GND)
│       ├── Common reference for all voltages
│       ├── Used to complete electrical circuits
│       └── Essential for stable measurements
│
├── General Purpose Input/Output (GPIO)
│   ├── Digital Input Mode
│   │   ├── Read button presses
│   │   ├── Sense HIGH/LOW voltages
│   │   └── Detect events/edges (interrupts)
│   ├── Digital Output Mode
│   │   ├── Drive LEDs, relays, MOSFET gates
│   │   └── Generate logic-level control signals
│   ├── Alternate Functions (shared with GPIO)
│   │   ├── I²C, SPI, UART, PCM, PWM etc.
│   │   └── Selected by configuring pin’s alt-function in software
│   └── Voltage Characteristics
│       ├── 3.3 V logic level
│       ├── 16 mA max per pin recommended
│       └── Use level shifters for 5 V devices
│
├── I²C (Inter-Integrated Circuit)
│   ├── Bus Lines
│   │   ├── SDA (Serial Data)
│   │   └── SCL (Serial Clock)
│   ├── Electrical
│   │   ├── Open-drain lines with pull-ups
│   │   └── Multiple devices share same two wires
│   ├── Software
│   │   ├── Kernel driver /dev/i2c-X
│   │   └── Addressed by 7-bit or 10-bit address
│   └── Typical Devices
│       ├── Sensors (Temp, Pressure, IMU)
│       ├── EEPROM for HAT identification
│       ├── GPIO expanders
│       └── Real Time Clock modules
│
├── SPI (Serial Peripheral Interface)
│   ├── Bus Lines
│   │   ├── MOSI (Master Out Slave In)
│   │   ├── MISO (Master In Slave Out)
│   │   ├── SCLK (Clock)
│   │   ├── CE0_N (Chip Select 0)
│   │   └── CE1_N (Chip Select 1)
│   ├── Electrical
│   │   ├── Full-duplex, synchronous
│   │   ├── Separate chip select per slave
│   │   └── High speed (MHz range)
│   ├── Software
│   │   ├── Appears as /dev/spidevX.Y
│   │   └── Configurable mode, clock speed, bits/word
│   └── Typical Devices
│       ├── TFT / OLED Displays
│       ├── High-speed ADC/DAC chips
│       ├── Flash memory chips
│       └── RFID / NFC modules
│
├── UART (Universal Asynchronous Receiver/Transmitter)
│   ├── Lines
│   │   ├── TXD (Transmit)
│   │   └── RXD (Receive)
│   ├── Electrical
│   │   ├── 3.3 V logic level
│   │   └── Only point-to-point (no bus)
│   ├── Software
│   │   ├── /dev/serial0, /dev/serial1
│   │   └── Configurable baud, parity, stop bits
│   └── Typical Uses
│       ├── Serial console to Pi
│       ├── GPS receivers
│       ├── Bluetooth or GSM modules
│       └── Debugging microcontrollers
│
├── PWM (Pulse Width Modulation)
│   ├── Hardware PWM Pins
│   │   ├── GPIO12, GPIO13 (PWM0 channels)
│   │   ├── GPIO18, GPIO19 (PWM1 channels)
│   │   └── High-resolution duty cycle
│   ├── Software PWM
│   │   ├── Any GPIO with timing loops
│   │   └── Lower frequency/resolution
│   └── Uses
│       ├── Motor speed control
│       ├── LED dimming
│       └── Servo angle control
│
├── PCM / I²S (Digital Audio)
│   ├── PCM_CLK (Bit Clock)
│   ├── PCM_FS (Frame Sync)
│   ├── PCM_DIN (Data In)
│   ├── PCM_DOUT (Data Out)
│   ├── Supports
│   │   ├── Stereo digital audio streams
│   │   ├── Low jitter clocking
│   │   └── External DAC/ADC boards
│   └── Typical Uses
│       ├── Hi-Fi DAC hats
│       ├── Digital microphones
│       └── Multi-channel audio output
│
├── EEPROM / HAT ID Interface
│   ├── ID_SD (Data)
│   ├── ID_SC (Clock)
│   ├── Dedicated I²C bus for HATs
│   └── Stores
│       ├── Board name, version
│       ├── GPIO usage metadata
│       └── Configuration scripts
│
├── Special Pins (RUN, ID)
│   ├── RUN header (reset)
│   ├── ACT LED control
│   └── Utility test pads (varies by model)
│
└── Mechanical/Physical Layer
    ├── 2×20 pin header
    ├── 2.54 mm pitch
    ├── Pin 1 marker
    └── Orientation matters (keying)
```
# RPi Interfaces & Signals Define

## 1. I²C (Inter-Integrated Circuit) Bus

**Definition:**  
I²C is a **synchronous, multi-master, multi-slave, two-wire serial communication protocol**. It allows multiple peripheral devices to communicate over the same pair of wires using unique addresses. The Pi can act as master or slave depending on configuration. Widely used for low-speed sensors, EEPROMs, RTCs, and configuration devices.

### Types

**a) Standard I²C Bus**  
- **Definition:** General-purpose I²C bus for connecting peripherals.  
- **Features:**  
  - Uses SDA (data) and SCL (clock) lines  
  - Multi-device support via addresses  
  - Open-drain configuration; requires pull-up resistors  
  - Speeds: Standard 100 kHz, Fast 400 kHz, High-speed 1 MHz  
- **Signals:**  
  - **SDA1 (GPIO2, Pin 3)**: Data line; bidirectional; transmits/receives bytes between Pi and peripherals.  
  - **SCL1 (GPIO3, Pin 5)**: Clock line; synchronizes data transmission; master-controlled.

**b) Dedicated HAT EEPROM Bus**  
- **Definition:** Separate I²C bus for reading HAT EEPROM metadata.  
- **Features:**  
  - Independent from standard I²C bus  
  - Stores HAT board name, version, and GPIO configuration  
  - Read automatically at boot to configure device tree overlays  
- **Signals:**  
  - **ID_SD (Pin 27)**: Serial data line for EEPROM.  
  - **ID_SC (Pin 28)**: Clock line for EEPROM synchronization.

---

## 2. SPI (Serial Peripheral Interface)

**Definition:**  
SPI is a **synchronous, full-duplex, high-speed serial communication bus** that allows a master device (Pi) to communicate with one or more slave devices using separate chip select lines.

**Features:**  
- Full-duplex, simultaneous transmit/receive  
- High-speed (up to tens of MHz)  
- Each slave device has a unique chip-select line  
- Excellent for displays, flash memory, ADCs/DACs

**Signals:**  
- **MOSI (GPIO10, Pin 19)** — Master Out Slave In; master sends data to slave.  
- **MISO (GPIO9, Pin 21)** — Master In Slave Out; slave sends data to master.  
- **SCLK (GPIO11, Pin 23)** — Serial Clock; controls timing for data transfer.  
- **CE0_N (GPIO8, Pin 24)** — Chip Enable 0; active-low selection for slave 0.  
- **CE1_N (GPIO7, Pin 26)** — Chip Enable 1; active-low selection for slave 1.

---

## 3. UART (Universal Asynchronous Receiver/Transmitter)

**Definition:**  
UART is a **point-to-point asynchronous serial interface** used to exchange data between two devices. It does not require a clock line because both ends agree on a common baud rate.

**Features:**  
- Configurable baud rate, parity, stop bits  
- Simple two-wire interface (TX/RX)  
- Often used for console, GPS, GSM, or debugging

**Signals:**  
- **TXD (GPIO14, Pin 8)** — Transmit data; sends bytes from Pi.  
- **RXD (GPIO15, Pin 10)** — Receive data; receives bytes into Pi.

---

## 4. PWM (Pulse Width Modulation)

**Definition:**  
PWM generates a **variable duty-cycle square wave** to control the effective voltage or energy supplied to devices like motors, LEDs, and servos.

**Features:**  
- Hardware PWM gives precise, high-frequency signals  
- Software PWM is flexible but less accurate  
- Duty cycle controls speed, brightness, or position

**Hardware PWM Signals:**  
- **GPIO12 (Pin 32), GPIO13 (Pin 33), GPIO18 (Pin 12), GPIO19 (Pin 35)**  

**Software PWM Signals:**  
- Any GPIO pin can be used; implemented via software loops.

---

## 5. PCM / I²S (Digital Audio Interface)

**Definition:**  
PCM / I²S is a **synchronous digital audio bus** for transferring raw audio samples between processors and DAC/ADC chips.

**Features:**  
- High-quality stereo audio  
- Separate clock (PCM_CLK) and frame sync (PCM_FS) lines  
- Allows precise timing for audio sample transmission

**Signals:**  
- **PCM_CLK (GPIO18, Pin 12)** — Bit clock; controls rate of audio bits.  
- **PCM_FS (GPIO19, Pin 35)** — Frame sync / LRCLK; indicates left/right channel frame.  
- **PCM_DIN (GPIO20, Pin 38)** — Audio data input; Pi receives digital audio.  
- **PCM_DOUT (GPIO21, Pin 40)** — Audio data output; Pi transmits digital audio.

---

## 6. Power Pins

**Definition:**  
Supply voltage to Pi and connected peripherals. Not software-controllable.

**Types:**  
- **5V Power (Pin 2, Pin 4)** — Direct USB input; high-voltage devices.  
- **3.3V Power (Pin 1, Pin 17)** — Regulated; for logic circuits and sensors.  
- **GND (Pins 6, 9, 14, 20, 25, 30, 34, 39)** — Common 0 V reference; completes circuits.
