# Advanced Versal Architecture Notes (Important Interview Topics)

---

# 1. What is APU?

APU stands for:

Application Processing Unit

In Versal, the APU contains:

```text
Dual ARM Cortex-A72
```

Purpose:

- Run Linux
- Run User Applications
- Networking
- TCP/IP Stack
- Python Applications
- C/C++ Applications
- High-Level Software

Think:

```text
APU = PC-like processor section inside Versal
```

Example:

```text
Linux
Python Program
OpenCV Application
Web Server
```

All these execute on the Cortex-A72 processors inside the APU.

---

# 2. What is RPU?

RPU stands for:

Real-Time Processing Unit

Contains:

```text
Dual ARM Cortex-R5F
```

Purpose:

- Motor Control
- Industrial Automation
- Safety Applications
- Deterministic Tasks
- Timing-Critical Systems

Think:

```text
APU = Performance

RPU = Deterministic Timing
```

Example:

Suppose a motor control loop must execute every:

```text
100 microseconds
```

Linux running on A72 cannot guarantee this.

Therefore R5F is used.

---

# 3. Cortex-A72 vs Cortex-R5F

| Feature | Cortex-A72 | Cortex-R5F |
|----------|----------|----------|
| Type | Application Processor | Real-Time Processor |
| Unit | APU | RPU |
| OS | Linux | RTOS / Bare Metal |
| Goal | Maximum Performance | Deterministic Timing |
| Execution | Not Predictable | Predictable |
| Cache | Larger | Smaller |
| Throughput | Higher | Lower |
| Used For | Linux, Applications | Motor Control |

Interview Answer:

Cortex-A72 is optimized for performance and runs Linux.

Cortex-R5F is optimized for deterministic execution and real-time control applications.

---

# 4. Why Does Versal Have Both A72 and R5F?

Because modern systems require both:

Example:

```text
Autonomous Robot

Cortex-A72:
    Linux
    AI Algorithms
    Networking

Cortex-R5F:
    Motor Control
    Safety Monitoring
    Sensor Timing
```

One processor type alone cannot efficiently perform both tasks.

---

# 5. What is BootROM?

BootROM means:

Boot Read Only Memory

It is a small ROM permanently built into the silicon by AMD.

Important:

```text
BootROM is inside the Versal chip.
```

Not in:

- SD Card
- DDR4
- QSPI Flash

Think:

```text
BootROM
=
Factory Programmed Startup Code
```

---

# 6. Why is BootROM Needed?

When power is first applied:

```text
Power ON
```

Nothing is running.

Not Linux.

Not PLM.

Not FPGA Design.

Question:

```text
Who starts the system?
```

Answer:

```text
BootROM
```

---

# 7. Responsibilities of BootROM

Immediately after power-on:

BootROM performs:

### Step 1

Read Boot Mode

Examples:

```text
JTAG Boot
SD Boot
QSPI Boot
```

### Step 2

Identify boot device

Example:

```text
SD Card
```

### Step 3

Locate PLM

### Step 4

Load PLM

### Step 5

Transfer execution control

---

# 8. BootROM in Zynq vs Versal

Zynq:

```text
Power ON
 ↓
BootROM
 ↓
FSBL
 ↓
Linux
```

Versal:

```text
Power ON
 ↓
BootROM
 ↓
PMC
 ↓
PLM
 ↓
Linux
```

---

# 9. What is FSBL?

FSBL stands for:

First Stage Boot Loader

Used in:

```text
Zynq-7000
Zynq UltraScale+
```

Boot Flow:

```text
Power ON
 ↓
BootROM
 ↓
FSBL
 ↓
Linux
```

---

# 10. Responsibilities of FSBL

FSBL performs:

```text
DDR Initialization
Clock Initialization
Peripheral Initialization
Bitstream Loading
Linux Loading
```

Think:

```text
FSBL
=
System Startup Software
```

---

# 11. Why Did AMD Replace FSBL?

Versal contains:

```text
A72
R5F
AI Engines
NoC
PMC
PSM
PL
```

This architecture is significantly more complex than Zynq.

Therefore AMD introduced:

```text
PLM
```

---

# 12. What is PMC?

PMC stands for:

Platform Management Controller

Location:

```text
Inside Versal Chip
```

Think:

```text
PMC = Startup Boss
```

---

# 13. Responsibilities of PMC

PMC handles:

```text
Boot Management
Device Configuration
Security
Image Authentication
Initialization Control
Power-Up Coordination
```

Interview Answer:

PMC is responsible for startup, configuration and security management of the Versal device.

---

# 14. What is PLM?

PLM stands for:

Platform Loader and Manager

Used only in:

```text
Versal
```

Think:

```text
FSBL = Old Manager

PLM = New Manager
```

---

# 15. Responsibilities of PLM

PLM performs:

```text
Load Images
Initialize Device
Configure FPGA
Manage Boot Process
System Bring-Up
Error Handling
```

---

# 16. What Replaced FSBL?

Interview Answer:

```text
Zynq
 ↓
FSBL

Versal
 ↓
PLM
```

---

# 17. What is PSM?

PSM stands for:

Platform System Manager

Location:

```text
Inside Versal
```

Think:

```text
PMC = Startup Manager

PSM = Power Manager
```

---

# 18. Responsibilities of PSM

PSM manages:

```text
Power Domains
Sleep Modes
Wakeup Events
Reset Management
Power Saving
```

Example:

If AI Engines are not used:

```text
PSM can power them down.
```

---

# 19. Relationship Between BootROM, PMC, PLM and PSM

Most Important Diagram

```text
Power ON
   │
   ▼
BootROM
   │
   ▼
PMC
   │
   ▼
PLM
   │
   ▼
Initialize Device
   │
   ▼
Load Linux
   │
   ▼
Run Application
```

Meanwhile:

```text
PSM
```

continuously manages:

```text
Power
Reset
Sleep
Wakeup
```

---

# 20. Complete Versal Boot Flow

Interview Diagram

```text
Power ON
   │
   ▼
BootROM
   │
   ▼
Read Boot Mode
   │
   ▼
PMC Active
   │
   ▼
Load PLM
   │
   ▼
Initialize DDR
   │
   ▼
Initialize Clocks
   │
   ▼
Configure FPGA
   │
   ▼
Load Linux
   │
   ▼
Linux Runs on Cortex-A72
```

---

# 21. System Controller vs PMC

Very Common Interview Question

PMC:

```text
Inside Versal Chip
```

Responsibilities:

```text
Boot
Configuration
Security
Initialization
```

---

System Controller:

```text
Separate Device on VCK190 Board
```

Responsibilities:

```text
Voltage Monitoring
Temperature Monitoring
Fan Control
Clock Management
Board Management
```

Think:

```text
PMC
=
Versal Startup Manager

System Controller
=
Board Manager
```

---

# 22. FMC Comparison

PYNQ-Z2:

```text
No FMC
```

Provides:

```text
Pmod
Arduino Header
```

---

ZYBO Z7:

```text
FMC-LPC Available
```

Provides:

```text
Low Pin Count FMC
```

---

VCK190:

```text
Two FMC+ Connectors
```

Provides:

```text
Higher Bandwidth
More Signals
High-Speed Expansion
```

---

# 23. Interview Question

Why was FSBL replaced by PLM?

Answer:

Versal architecture contains AI Engines, NoC, PMC, PSM, multiple processor domains and advanced security features. FSBL was insufficient to manage this complexity. Therefore AMD introduced PLM, which provides a more scalable and flexible boot architecture.

---

# Quick Revision

BootROM
=
Factory programmed startup code

FSBL
=
Zynq startup software

PLM
=
Versal startup software

PMC
=
Startup and configuration manager

PSM
=
Power manager

APU
=
Dual Cortex-A72

RPU
=
Dual Cortex-R5F

A72
=
Linux + Applications

R5F
=
Real-Time Control

PYNQ-Z2
=
No FMC

ZYBO
=
FMC-LPC

VCK190
=
FMC+
