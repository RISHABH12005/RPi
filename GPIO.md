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
