# *Dual Linear PSU (9V/5V)* Module Board
**Module Board Status**: `[Prototyped]`

Dual-rail linear power supply module board featuring cascaded $9\text{V}$ and $5\text{V}$ regulated outputs.  
This MOB accepts wide-range AC or DC input voltages from $12\text{V}$ to $15\text{V}$.

![mob-built](mob-audio-psu-9v-5v_built.jpg)

This module provides clean, low-noise linear regulation suitable for audio circuits, microcontrollers, and hardware development cores. It features universal AC/DC input rectification, high-capacity capacitive smoothing, independent output toggle switches, and dedicated status LED indicators.


## Specifications
| Parameter | Min | Typical | Max | Unit | Notes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Supply Voltage** | 12.0 | 12.0 - 15.0 | 18.0 | V | AC RMS or DC polar/non-polar input |
| **Output Voltage 1** | 8.65 | 9.0 | 9.35 | V | DC regulated rail via `U1` (7809) |
| **Output Voltage 2** | 4.80 | 5.0 | 5.20 | V | DC regulated rail via `U2` (7805) |
| **Smoothing Capacitance** | — | 1000 | — | $\mu$F | Main electrolytic filter capacitor ($C1$) |
| **Quiescent Current** | — | 11.5 | — | mA | Idle consumption at $12\text{V}_{\text{DC}}$ (All switches ON, no load) |
| **Output Connectors** | — | 2 | — | Ports | Dual independent 2-pin headers (`J2` and `J3`) |


## Design

### Schematic
![mob-schematic](mob-audio-psu-9v-5v_sch.jpg)

### Circuit Description
The power supply architecture starts at the power input DC jack `J1`. An integrated diode bridge rectifier (`B1`) ensures universal compatibility with both AC and DC sources while rendering the DC input completely immune to reverse-polarity wiring faults. Main low-frequency ripple filtering is handled by a large $1000\,\mu\text{F}$ aluminum electrolytic capacitor (`C1`) paired with a high-frequency $100\text{nF}$ ceramic bypass capacitor (`C2`). A raw voltage status LED (`DL1`) with a $2.2\text{ k}\Omega$ limiting resistor (`R1`) monitors the pre-regulated rail.

Voltage regulation is executed via a cascaded topology:
* **$9\text{V}$ Rail**: The primary 7809 linear regulator (`U1`) stabilizes the smoothed input down to $+9\text{V}$. This rail is switchable via `SW1` and outputs to the 2-pin Molex connector `J2`. A green LED (`DL2`) with a $2.2\text{ k}\Omega$ resistor (`R2`) indicates active rail status.
* **$5\text{V}$ Rail**: The secondary 7805 linear regulator (`U2`) is chained directly to the regulated $+9\text{V}$ node rather than the raw input. This structure splits the thermal load across both ICs, significantly lowering the power dissipation of `U2`. This rail is switchable via `SW2` and outputs to the 2-pin Molex connector `J3`. A green LED (`DL3`) with a $1\text{ k}\Omega$ resistor (`R3`) signals active output status.

### PCB Layout
![mob-pcb](mob-audio-psu-9v-5v_pcb.jpg)


## Test Log
Todo.


## Bill of Materials
- [x] 1 x Prototyping paperboard 5x7cm
- [x] 1 x DC Power Jack barrel connector PCB mount (`J1`)
- [x] 2 x 2-pin power output connectors (Molex-KK, `J2` $+9\text{V}$, `J3` $+5\text{V}$)
- [x] 2 x SPST or SPDT miniature slide switches (`SW1`, `SW2`)
- [x] 1 x Diode Bridge Rectifier (e.g., DF04M / W04M or discrete 1N4007 array, `B1`)
- [x] 1 x Positive Linear Regulator $9\text{V}$ / 1A (TO-220, 7809, `U1`)
- [x] 1 x Positive Linear Regulator $5\text{V}$ / 1A (TO-220, 7805, `U2`)
- [x] 1 x Aluminum electrolytic capacitor $1000\,\mu\text{F}$ / 25V or higher (`C1`)
- [x] 4 x Ceramic decoupling capacitors $100\text{nF}$ / 50V (`C2`, `C3`, `C4`, `C5`)
- [x] 3 x Power indicator green LEDs 3mm (`DL1`, `DL2`, `DL3`)
- [x] 2 x Precision carbon resistors $2.2\text{ k}\Omega$ (`R1`, `R2`)
- [x] 1 x Precision carbon resistor $1\text{ k}\Omega$ (`R3`)