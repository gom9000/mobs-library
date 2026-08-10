# *Switch Array (8x)* Module Board
**Module Board Status**: `[Validated]`

Eight channel active-low switch/button input array module board.  
This MOB operates across a logic supply voltage range from $3.3\text{V}$ to $5.0\text{V}$.

![mob-built](mob-io-array-switch-8x_built.jpg)

This module provides eight user-input SPST tactile switches connected to dedicated active-low data lines with integrated pull-up resistors.


## Specifications
| Parameter | Min | Typical | Max | Unit | Notes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Supply Voltage** | 3.3 | 5.0 | 5.0 | V | Main power bus  ($V_{CC}$) |
| **Bulk Capacitance** | — | 10 | — | $\mu$F | Tantalum capacitor ($C$) |
| **Quiescent Current** | 1.5 | 3.2 | 3.2 | mA | Idle state (all switches open) at 3.3V / 5.0V |
| **Input Channels** | — | 8 | — | Lines | Active-low logic outputs (`JA` pins 1–4, `JB` pins 1–4) |
| **Pull-up Resistance** | — | 10 | — | k$\Omega$ | Integrated per-channel pull-up ($R1$–$R8$) |
| **Logic HIGH Output Level** | — | $V_{CC}$ | — | V | Switches open (idle) |
| **Logic LOW Output Level** | — | 0 | — | V | ($GND$) |
| **Switch Active Current** | 0.33 | 0.50 | 0.50 | mA | Per pressed switch ($I_{SW} = V_{CC} / 10\text{k}\Omega$) at 3.3V / 5.0V |


## Design

### Schematic
![mob-schematic](mob-io-array-switch-8x_sch.jpg)

### Circuit Description
The circuit provides an 8-bit digital input array interfacing user tactile switches ($SW1$–$SW8$) with active-low logic, to drive microcontrollers or digital buses. Integrated $10\text{k}\Omega$ pull-up resistors ($R1$–$R8$) ensure stable HIGH signals when switches are open. Data lines are routed through two 4-pin Molex-KK headers (`JA` and `JB`). Power status is indicated by a green LED (`DL`) with a $1\text{k}\Omega$ limiting resistor (`R`), while a $10\,\mu\text{F}$ tantalum capacitor (`C`) provides localized supply decoupling.

### PCB Layout
![mob-pcb](mob-io-array-switch-8x_pcb.jpg)


## Test Log
The board was tested using a GVDA 30V/10A switching laboratory power supply and a GD128 digital multimeter.

**Quiescent & Active Current Verification**:
| Supply Voltage | Expected Idle | Idle $I_Q$ (All Open) | Single Switch Pressed | All 8 Switches Pressed |
| :---: | :---: | :---: | :---: | :---: |
| **3.3V** | $1.50\text{mA}$ | $1.44\text{mA}$ | $1.77\text{mA}$ | $4.05\text{mA}$ |
| **5.0V** | $3.20\text{mA}$ | $3.09\text{mA}$ | $3.58\text{mA}$ | $7.04\text{mA}$ |

*\*Note: Expected idle values assume nominal LED $V_F = 1.8\text{V}$, while measured diode drop was $1.9\text{V}$.*

<br/>

**Logic Level Verification**:
| State | Calculated Voltage | Measured Voltage | Logic Level |
| :---: | :---: | :---: | :---: |
| **Idle (Switch Open)** | $V_{CC}$ | $V_{CC}$ ($3.30\text{V} / 5.00\text{V}$) | **HIGH** |
| **Pressed (Switch Closed)** | $0.000\text{V}$ | below measurement resolution | **LOW** |


## Bill of Materials
- [x] 1 x Prototyping paperboard 5x7cm
- [x] 1 x 2-pin power connector (Molex-KK)
- [x] 2 x 4-pin data output connectors (Molex-KK, `JA`, `JB`)
- [x] 1 x Tantalum bulk capacitor $10\,\mu\text{F}$ / 16V ($C$)
- [x] 1 x Current limiting resistor $1\text{k}\Omega$ (for LED)
- [x] 1 x Green power activity LED (3mm, `DL`)
- [x] 8 x Pull-up resistors $10\text{k}\Omega$ ($R1$–$R8$)
- [x] 8 x SPST NO tactile pushbuttons ($SW1$–$SW8$)