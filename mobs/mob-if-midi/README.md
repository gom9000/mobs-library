# *MIDI Interface (IN/OUT/THRU)* Module Board
**Module Board Status**: `[Validated]`

Optoisolated MIDI input, output, and thru hardware interface module board.  
This MOB interfaces dual-voltage host logic ($3.3\text{V} / 5.0\text{V}$) with standard $5.0\text{V}$ MIDI current loops.

![mob-built](mob-if-midi_built.jpg)

This module provides complete, compliant MIDI connectivity featuring full galvanic isolation on the input channel via a high-speed optocoupler, active Schmitt-trigger buffering for THRU/OUT signaling, independent data activity LEDs, and selectable logic level translation.


## Specifications
| Parameter | Min | Typical | Max | Unit | Notes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Supply Voltage** | — | 5.0 | 5.0 | V | Fixed power supply for ICs (`PWR1` or `PWR2`) |
| **Logic Interface Voltage** | 3.3 | — | 5.0 | V | Host I/O level reference selected via `J1` |
| **Bulk Capacitance** | — | 20 | — | $\mu$F | Dual $10\,\mu\text{F}$ tantalum capacitors ($C_{5\text{V}}, C_{3\text{V}}$) |
| **Quiescent Current** | 3.0 | 6.5 | 7.0 | mA | Idle state (no MIDI data, power LEDs active) at $3.3\text{V} / 5.0\text{V}$ |


## Design

### Schematic
![mob-schematic](mob-if-midi_sch.jpg)

### Circuit Description
The circuit handles bidirectional MIDI communication. The **MIDI IN** line is fully isolated through a 6N138 optocoupler ($U1$). The output collector of $U1$ uses a split pull-up configuration selectable via jumper `J1`: a $680\,\Omega$ resistor ($R2b$) shifts the line output to $3.3\text{V}$ logic, while a $1\text{ k}\Omega$ resistor ($R2a$) targets $5.0\text{V}$ devices. A 74LS14 Hex Schmitt-Trigger Inverter ($U2$) conditions and buffers the signals. Two series inverters regenerate the isolated input signal to drive the current-loop **MIDI THRU** port using standard $220\,\Omega$ resistors ($R4, R5$). The **MIDI OUT** hardware uses two cascaded inverters to re-shape the incoming `Tx` serial data before sending it out through $220\,\Omega$ resistors ($R7, R8$). Dedicated inverters drive three 3mm data activity LEDs (`DL1`–`DL3`) to monitor the status of all three channels without loading down the signal lines.

### PCB Layout
![mob-pcb](mob-if-midi_pcb.jpg)


## Bill of Materials
- [x] 1 x Prototyping paperboard 5x7cm
- [x] 1 x 2-pin power connector (Molex-KK, `PWR1`)
- [x] 1 x 3-pin dual-rail power connector (Molex-KK, `PWR2`)
- [x] 1 x 3-pin data connector (Molex-KK, `SERIAL` Rx/Tx/GND)
- [x] 3 x DIN5 female PCB-mount sockets (MIDI IN, OUT, THRU)
- [x] 1 x 3-pin male header with shorthand jumper block (`J1`)
- [x] 2 x Tantalum bulk capacitors $10\,\mu\text{F}$ ($C_{5\text{V}}, C_{3\text{V}}$)
- [x] 2 x Ceramic decoupling capacitors $100\text{nF}$ ($C1, C2$)
- [x] 2 x Power indicator green LEDs 3mm (`DL5V`, `DL3V`)
- [x] 2 x Power LED limiting resistors $1\text{ k}\Omega$ (`R5V`, `R3V`)
- [x] 3 x Data status green LEDs 3mm (`DL1`–`DL3`)
- [x] 3 x Data LED limiting resistors $1\text{ k}\Omega$ ($R3, R6, R9$)
- [x] 5 x Precision carbon resistors $220\,\Omega$ ($R1, R4, R5, R7, R8$)
- [x] 1 x Precision carbon resistor $680\,\Omega$ ($R2b$)
- [x] 1 x Precision carbon resistor $1\text{ k}\Omega$ ($R2a$)
- [x] 1 x High-speed optocoupler IC (6N138) with DIP-8 IC socket
- [x] 1 x Hex Schmitt-Trigger Inverter IC (74LS14) with DIP-14 IC socket
- [x] 1 x Small-signal fast switching diode (1N4148, $D1$)