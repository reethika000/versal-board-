

# 2. Evolution of AMD FPGA SoCs

## Zynq-7000 (PYNQ-Z2, ZYBO)

Contains:

- Dual ARM Cortex-A9
- Programmable Logic (FPGA)

Architecture:

PS + PL

---

## Versal (VCK190)

Contains:

- Dual Cortex-A72
- Dual Cortex-R5F
- AI Engines
- Programmable Logic
- NoC
- PMC
- PSM

Architecture:

APU + RPU + AI Engine + PL + NoC

---

# 3. What is VCK190?

VCK190 is an AMD Versal Evaluation Board built around the Versal XCVC1902 Adaptive SoC.

Applications:

- AI Acceleration
- DSP
- Image Processing
- Networking
- Datacenter Acceleration
- Embedded Linux

---

# 4. Major Components on VCK190

- Versal XCVC1902 Adaptive SoC
- DDR4 Memory
- LPDDR4 Memory
- QSPI Flash
- SD Card Slot
- FMC+ Connectors
- PCIe Interface
- Ethernet
- FTDI Interface
- System Controller

---

# 5. Which Processor Does VCK190 Contain?

Interview Answer:

The VCK190 contains a Versal XCVC1902 Adaptive SoC.

Inside it:

- Dual ARM Cortex-A72
- Dual ARM Cortex-R5F
- AI Engines
- Programmable Logic

Do NOT say:

"Versal Processor"

Correct Answer:

"Versal XCVC1902 containing dual Cortex-A72 and dual Cortex-R5F processors."

---

# 6. Cortex-A72

Used for:

- Linux
- User Applications
- Networking
- High-Level Software

Characteristics:

- 64-bit
- High Performance
- Application Processor

---

# 7. Cortex-R5F

Used for:

- Real-Time Control
- Deterministic Tasks
- Industrial Applications
- Safety Applications

Characteristics:

- Real-Time Processor
- Low Latency
- Predictable Execution

---

# 8. AI Engines

AI Engines are specialized vector processors.

Used for:

- DSP
- Machine Learning
- FFT
- Beamforming
- Matrix Operations

Benefits:

- High Throughput
- Low Power
- Better than implementing everything in PL

---

# 9. Programmable Logic (PL)

The FPGA portion of Versal.

Used for:

- Accelerators
- CNNs
- DSP Blocks
- Image Processing
- Custom Hardware

---

# 10. NoC (Network on Chip)

NoC = Network on Chip

Purpose:

Connects:

- Processors
- AI Engines
- DDR
- PL

Think of it as:

Internal High-Speed Highway

Not present in Zynq-7000.

---

# 11. USB

USB is used for:

- Programming
- Debugging
- Serial Communication

USB itself cannot directly talk to FPGA JTAG.

Hence FTDI is used.

---

# 12. FTDI

FTDI = Future Technology Devices International

VCK190 contains FT4232HL.

Functions:

USB ↔ JTAG

USB ↔ UART

---

# 13. JTAG

JTAG = Joint Test Action Group

Used for:

- FPGA Programming
- Hardware Debugging
- Boundary Scan

Programming Path:

Vivado
↓
USB
↓
FTDI
↓
JTAG
↓
Versal

---

# 14. UART

UART = Universal Asynchronous Receiver Transmitter

Used for:

- Linux Console
- Debug Messages
- Serial Communication

Path:

Versal UART
↓
FTDI
↓
USB
↓
Laptop Terminal

---

# 15. SD Card

Stores:

- BOOT.BIN
- image.ub
- rootfs

SD card is removable storage.

---

# 16. BOOT.BIN

Boot image.

May contain:

- PLM
- FPGA Bitstream
- Boot Components

---

# 17. image.ub

Contains Linux Kernel.

---

# 18. rootfs

Contains:

- Libraries
- Applications
- Linux Filesystem

---

# 19. DDR4

Runtime memory.

Linux executes from DDR4.

Characteristics:

- Volatile
- High Speed

---

# 20. LPDDR4

Low Power DDR4.

Used for:

- Additional Memory
- High Bandwidth Applications

---

# 21. Difference Between SD Card and DDR4

SD Card:

- Non-Volatile
- Stores Linux

DDR4:

- Volatile
- Runs Linux

Process:

SD Card
↓
DDR4
↓
Execution

---

# 22. Linux on Versal

Linux runs on Cortex-A72 processors.

Boot Process:

SD/QSPI
↓
Load Linux
↓
Copy to DDR4
↓
Execute on A72

---

# 23. Flash Memory

Non-Volatile Memory.

Examples:

- SSD
- Pendrive
- Memory Card

Data remains after power off.

---

# 24. QSPI Flash

QSPI = Quad SPI Flash

Permanent storage on board.

Stores:

- BOOT.BIN
- Linux
- Applications

Unlike SD card:

- Cannot be removed

---

# 25. Boot Modes

VCK190 supports:

- JTAG Boot
- SD Boot
- QSPI Boot

Boot mode selected using switches.

---

# 26. JTAG Boot

Power ON
↓
Vivado Programs FPGA
↓
Run

Used during development.

---

# 27. SD Boot

Power ON
↓
Read SD Card
↓
Load BOOT.BIN
↓
Load Linux
↓
Run

---

# 28. QSPI Boot

Power ON
↓
Read Flash
↓
Load Software
↓
Run

Used in final products.

---

# 29. BootROM

First code executed after power-up.

Responsibilities:

- Read Boot Mode
- Start Boot Process

---

# 30. PMC

PMC = Platform Management Controller

Responsibilities:

- Device Initialization
- Configuration
- Boot Management
- Security

Think:

Startup Manager

---

# 31. PSM

PSM = Platform System Manager

Responsibilities:

- Power Management
- Reset Management
- Sleep/Wakeup

Think:

Power Manager

---

# 32. PLM

PLM = Platform Loader and Manager

Responsible for:

- Loading Images
- Device Bring-up
- System Initialization

Important:

Zynq → FSBL

Versal → PLM

---

# 33. Complete Versal Boot Flow

Power ON
↓
BootROM
↓
Read Boot Mode
↓
Load PLM
↓
Initialize Device
↓
Configure FPGA
↓
Load Linux
↓
Run Application

---

# 34. PCIe

PCIe = Peripheral Component Interconnect Express

Used for:

- High-Speed Data Transfer

Examples:

- GPU
- FPGA Accelerator
- Network Cards

---

# 35. Why PCIe When USB Exists?

USB:

- Programming
- Debugging

PCIe:

- Massive Data Transfer

Applications:

- AI Acceleration
- Video Processing
- Datacenter Systems

---

# 36. FMC+

FMC+ = FPGA Mezzanine Card Plus

Expansion Interface.

Used for attaching:

- ADC Cards
- DAC Cards
- RF Cards
- Camera Cards

---

# 37. ADC Card

ADC = Analog to Digital Converter

Converts:

Analog Signal
↓
Digital Samples

Connected through FMC+.

---

# 38. DAC Card

DAC = Digital to Analog Converter

Converts:

Digital Data
↓
Analog Signal

Connected through FMC+.

---

# 39. Camera FMC Card

Provides direct image data to FPGA.

Camera
↓
FMC+
↓
Versal

Much faster than USB cameras.

---

# 40. System Controller

Separate controller on VCK190 board.

Responsibilities:

- Voltage Monitoring
- Temperature Monitoring
- Clock Management
- Fan Control
- Board Management

Important:

System Controller ≠ PMC

PMC is inside Versal.

System Controller is a separate device on the board.

---

# 41. Difference Between PYNQ-Z2, ZYBO and VCK190

| Feature | PYNQ-Z2 | ZYBO | VCK190 |
|----------|----------|----------|----------|
| Family | Zynq-7000 | Zynq-7000 | Versal |
| CPU | Cortex-A9 | Cortex-A9 | Cortex-A72 + R5F |
| AI Engine | No | No | Yes |
| NoC | No | No | Yes |
| FMC+ | Limited | Limited | Yes |
| Performance | Low | Medium | Very High |
| Target | Education | Education | Industrial/Research |

---

# 42. Most Important Interview Questions

Q. What processor is inside VCK190?

Ans:
Dual Cortex-A72 and Dual Cortex-R5F inside Versal XCVC1902.

---

Q. Difference between Zynq and Versal?

Ans:

Zynq:
PS + PL

Versal:
A72 + R5F + AI Engine + PL + NoC + PMC + PSM

---

Q. What replaced FSBL in Versal?

Ans:

PLM

---

Q. What is NoC?

Ans:

Internal communication network connecting processors, memory, AI Engines and PL.

---

Q. What is PMC?

Ans:

Platform Management Controller responsible for initialization and boot management.

---

Q. What is PSM?

Ans:

Platform System Manager responsible for power and reset management.

---

Q. Difference between PMC and System Controller?

Ans:

PMC:
Inside Versal chip.

System Controller:
Separate device on VCK190 board.

---

Q. Why use PCIe instead of USB?

Ans:

USB for programming/debug.

PCIe for high-speed data transfer.

---

Q. Why use FMC+?

Ans:

To connect ADC, DAC, RF and Camera cards.

---

Q. What are AI Engines?

Ans:

Dedicated vector processors optimized for DSP and Machine Learning workloads.

---

Q. What is the complete Versal boot flow?

Ans:

Power ON
↓
BootROM
↓
PLM
↓
Initialization
↓
Bitstream Configuration
↓
Linux
↓
Application

---

# Quick 5-Minute Revision

Versal XCVC1902

Contains:

- Cortex-A72
- Cortex-R5F
- AI Engines
- Programmable Logic
- NoC

Boot Flow:

BootROM
→ PLM
→ FPGA Configuration
→ Linux

Storage:

SD Card / QSPI

Runtime:

DDR4 / LPDDR4

Programming:

USB
→ FTDI
→ JTAG

Console:

UART
→ FTDI
→ USB

Expansion:

FMC+

High-Speed Transfer:

PCIe

Board Management:

System Controller

Versal Startup:

PMC

Versal Power:

PSM
