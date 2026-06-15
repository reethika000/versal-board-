# AMD VCK190 Versal Evaluation Board – Complete Beginner to Interview Revision Notes

## 1. What is VCK190?

The VCK190 is an AMD Versal Evaluation Board built around the Versal XCVC1902 Adaptive SoC.

Unlike traditional processors, a Versal device combines:

* ARM Processors
* Programmable Logic (FPGA)
* AI Engines
* High-Speed Interfaces
* Memory Controllers

in a single chip.

Think of it as:

```text
CPU + FPGA + AI Accelerator + Embedded System
```

all integrated into one device.

---

# 2. Main Components Present on VCK190

The board contains:

```text
VCK190 Board
│
├── Versal XCVC1902 Adaptive SoC
├── DDR4 Memory
├── LPDDR4 Memory
├── SD Card Slot
├── USB-C Port
├── FTDI Chip
├── Ethernet
├── PCIe Connector
├── FMC+ Connectors
├── System Controller
└── Clocking Circuits
```

---

# 3. Which Processor Does VCK190 Contain?

Interview Answer:

The VCK190 contains an AMD Versal XCVC1902 Adaptive SoC.

Inside the Versal device are:

* Dual-core ARM Cortex-A72 Application Processors
* Dual-core ARM Cortex-R5F Real-Time Processors
* AI Engines
* Programmable Logic (FPGA Fabric)

Do NOT say:

```text
Versal Processor
```

Correct answer:

```text
Dual ARM Cortex-A72
Dual ARM Cortex-R5F
inside the Versal XCVC1902 Adaptive SoC.
```

---

# 4. What is Programmable Logic (PL)?

Programmable Logic is the FPGA portion of the chip.

This is where custom hardware is implemented.

Examples:

* CNN Accelerators
* Image Processing
* DSP Systems
* Communication Systems
* Custom Peripherals

---

# 5. USB vs JTAG

This is one of the most important concepts.

## USB

USB is a communication interface.

Examples:

```text
Keyboard
Mouse
Pendrive
Webcam
```

all use USB.

---

## JTAG

JTAG stands for:

```text
Joint Test Action Group
```

JTAG is used for:

* FPGA Programming
* Hardware Debugging
* Reading Registers
* Signal Inspection

Think:

```text
USB = Communication

JTAG = Programming + Debugging
```

---

# 6. How Does Vivado Program the FPGA?

Many beginners think:

```text
Vivado
 ↓
FPGA
```

Actual path:

```text
Vivado
 ↓
USB Cable
 ↓
FTDI Chip
 ↓
JTAG Signals
 ↓
Versal Device
```

---

# 7. What is FTDI?

FTDI stands for:

```text
Future Technology Devices International
```

It is a company that manufactures USB interface chips.

The FT4232HL chip on the VCK190 converts:

```text
USB ↔ JTAG
USB ↔ UART
```

Therefore the laptop only needs a USB cable.

---

# 8. Why Do JTAG Cables Exist?

Older FPGA systems required:

```text
PC
 │
JTAG Cable
 │
FPGA
```

Modern boards include FTDI chips.

Therefore:

```text
PC
 │
USB
 │
FTDI
 │
JTAG
 │
FPGA
```

No external JTAG cable is normally required.

For VCK190:

```text
USB cable is sufficient.
```

---

# 9. UART

UART stands for:

```text
Universal Asynchronous Receiver Transmitter
```

Used for:

* Serial Communication
* Linux Console
* Debug Messages
* printf()

Path:

```text
Versal UART
      │
      ▼
FTDI
      │
      ▼
USB
      │
      ▼
Laptop Terminal
```

---

# 10. What is Linux on Versal?

Linux is an operating system.

Just like:

```text
Laptop
 └── Windows/Linux
```

Versal processors can run Linux.

Architecture:

```text
ARM Cortex-A72
        │
        ▼
Linux
```

---

# 11. What is SD Card?

The board contains a MicroSD slot.

The SD card is a storage device.

Examples:

```text
16GB
32GB
64GB
128GB
```

MicroSD cards.

---

# 12. What Files Are Stored in SD Card?

Typical contents:

```text
BOOT.BIN
image.ub
rootfs
```

---

## BOOT.BIN

Contains:

```text
Bootloader
Firmware
Bitstream
```

---

## image.ub

Contains:

```text
Linux Kernel
```

---

## rootfs

Contains:

```text
Linux Filesystem
Libraries
Applications
```

---

# 13. What is a Boot Image?

Image does NOT mean photograph.

Image means:

```text
Binary Software Package
```

Example:

```text
BOOT.BIN
```

is a boot image.

---

# 14. What is Booting?

When power is applied:

```text
Versal starts execution
```

and checks where software must be loaded from.

Possible sources:

```text
JTAG
SD Card
QSPI Flash
```

---

# 15. Boot Modes

Boot mode is selected using switches.

Examples:

```text
JTAG Boot
SD Boot
QSPI Boot
```

---

## JTAG Boot

```text
Power ON
 ↓
Vivado Programs FPGA
 ↓
Design Runs
```

No SD card required.

---

## SD Boot

```text
Power ON
 ↓
Read SD Card
 ↓
Load BOOT.BIN
 ↓
Load Linux
 ↓
System Starts
```

---

## QSPI Boot

```text
Power ON
 ↓
Read Flash Memory
 ↓
Load Software
 ↓
Run Application
```

No SD card required.

---

# 16. What is Flash Memory?

Flash memory is non-volatile memory.

Example:

```text
SSD
Pendrive
Memory Card
```

Power OFF:

```text
Data remains stored
```

---

# 17. What is QSPI Flash?

QSPI stands for:

```text
Quad Serial Peripheral Interface
```

QSPI Flash is a flash memory chip permanently soldered on the board.

```text
Board
│
├── Versal
└── QSPI Flash
```

It can store:

```text
BOOT.BIN
Linux
Applications
```

permanently.

---

# 18. SD Card vs QSPI Flash

## SD Card

```text
Removable
```

Can be inserted or removed.

---

## QSPI Flash

```text
Fixed
```

Permanently soldered.

Cannot be removed.

---

# 19. DDR4 Memory

DDR4 is RAM.

Used while software is running.

Characteristics:

```text
Fast
Temporary
Volatile
```

Power OFF:

```text
Data lost
```

---

# 20. LPDDR4 Memory

Low-Power DDR4 memory.

Used for:

* High Bandwidth
* Embedded Applications
* AI Workloads
* Video Processing

---

# 21. Relationship Between SD Card and DDR4

Very important interview concept.

Linux is STORED in:

```text
SD Card
```

but RUNS in:

```text
DDR4
```

Process:

```text
SD Card
 ↓
Load Linux
 ↓
Copy to DDR4
 ↓
Execute from DDR4
```

Same concept as:

```text
SSD → RAM → CPU
```

in a PC.

---

# 22. Linux Console

After boot:

```text
Linux executes from DDR4
```

Console output:

```text
Linux
 ↓
UART
 ↓
FTDI
 ↓
USB
 ↓
Laptop Terminal
```

---

# 23. What is PCIe?

PCIe stands for:

```text
Peripheral Component Interconnect Express
```

It is a very high-speed communication interface.

---

## Why Not Use USB?

USB is mainly used for:

```text
Programming
Debugging
Console Access
```

---

PCIe is used for:

```text
Massive Data Transfer
```

Examples:

```text
GPU
Network Card
FPGA Accelerator
```

---

# 24. PCIe Example

```text
CPU
 │
PCIe
 │
FPGA
```

Data can move at multiple GB/s.

Used for:

* AI Acceleration
* CNN Accelerators
* Video Processing
* Datacenter Applications

---

# 25. What is FMC?

FMC stands for:

```text
FPGA Mezzanine Card
```

Think:

```text
USB Port for FPGA Expansion
```

but much faster.

---

# 26. What is FMC+?

Enhanced FMC standard.

Provides:

* More Signals
* Higher Speed
* More Bandwidth

Used by VCK190.

---

# 27. How FMC Works

Not a cable.

It is a slot.

Example:

```text
Motherboard
     │
 RAM Slot
     │
 RAM Module
```

Similarly:

```text
VCK190
     │
 FMC+ Connector
     │
 FMC Card
```

---

# 28. What is an ADC Card?

ADC = Analog to Digital Converter

Purpose:

```text
Analog Signal
      │
      ▼
Digital Samples
```

Examples:

```text
Microphone
Sensor
Radar
RF Signal
```

---

# 29. What is on an ADC Card?

ADC card is an entire PCB.

Contains:

```text
ADC Chip
Clock Circuit
Power Circuit
FMC Connector
```

It physically plugs into FMC+.

---

# 30. Is ADC Built into VCK190?

For user applications:

```text
NO
```

External ADC cards are connected through FMC+.

---

# 31. Is DAC Built into VCK190?

For user applications:

```text
NO
```

External DAC cards are connected through FMC+.

---

# 32. What is a Camera FMC Card?

Example:

```text
Camera
 │
Camera FMC Board
 │
FMC+
 │
Versal
```

Allows direct transfer of image data to FPGA.

---

# 33. Why Use FMC Instead of USB for Cameras?

FMC provides:

```text
Lower Latency
Higher Speed
Direct FPGA Access
Raw Data Transfer
```

USB introduces protocol overhead.

---

# 34. System Controller

VCK190 contains a separate controller device.

Responsibilities:

```text
Voltage Monitoring
Temperature Monitoring
Clock Control
Board Management
Power Sequencing
```

Think:

```text
Board Manager
```

---

# 35. Complete Board Architecture

```text
                    VCK190

              ┌──────────────┐
              │   Versal     │
              │  XCVC1902    │
              └──────┬───────┘
                     │

      ┌──────────────┼──────────────┐
      │              │              │

      ▼              ▼              ▼

    DDR4         LPDDR4          FMC+

                                     │
                                     ▼

                           ADC / DAC / Camera

                     ▲
                     │

             Linux Runs Here
                  DDR4

                     ▲
                     │

             Loaded From

                     ▼

           SD Card or QSPI Flash

                     ▲
                     │

                Boot Source

                     ▲
                     │

                  JTAG

                     ▲
                     │

                   FTDI

                     ▲
                     │

                 USB-C

                     ▲
                     │

                  Laptop
```

---
