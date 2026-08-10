# *Audio I/O Stage* Module Board
**Module Board Status**: `[Prototyped]`

Dual-stage active analog audio input/output interface module board.  
This MOB operates from a single positive power rail ($V_{CC} \ge 9\text{V}$) and utilizes a virtual ground reference ($V_R$).

![mob-built](mob-audio-io-stage_built.jpg)

This module conditions analog line-level audio signals for downstream modular systems. It features a high-impedance input buffer stage, an independent output driver stage with jumper-selectable gain ($1\times$ or $2\times$ relative amplitude shift), and flexible internal/external virtual ground reference routing.


## Specifications
Todo.


## Design

### Schematic
![mob-schematic](mob-audio-io-stage_sch.jpg)

### Circuit Description
Todo.

### PCB Layout
![mob-pcb](mob-audio-io-stage_pcb.jpg)


## Bill of Materials
- [x] 1 x Prototyping paperboard 5x7cm
- [x] 1 x 2-pin power input connector (Molex-KK, `JVCC`)
- [x] 1 x 2-pin external reference voltage input connector (Molex-KK, `JVR`)
- [x] 4 x 2-pin audio I/O inline headers (Molex-KK, `JIN`, `JA`, `JB`, `JOUT`)
- [x] 2 x 3-pin male selection headers with shorting shunts (`JSW1`, `JSW2`)
- [x] 1 x Low-noise dual operational amplifier (NE5532, `U1`)
- [x] 1 x machined DIP-8 IC socket
- [x] 2 x Tantalum bulk capacitors $10\,\mu\text{F}$ / 25V (`C1`, `C2`)
- [x] 1 x Aluminum electrolytic smoothing capacitor $47\,\mu\text{F}$ / 25V (`C3`)
- [x] 3 x Aluminum electrolytic audio coupling capacitors $1\,\mu\text{F}$ / 50V (`C4`, `C6`, `C7`)
- [x] 2 x Aluminum electrolytic audio coupling capacitors $10\,\mu\text{F}$ / 25V (`C9`, `C10`)
- [x] 1 x Ceramic decoupling capacitor $100\text{nF}$ / 50V (`C5`, labeled `.1u`)
- [x] 1 x Ceramic NPO/COG feedback filter capacitor $4.7\text{nF}$ (`C8`, labeled `4n7`)
- [x] 1 x Metal film pull-down resistor $1\text{ M}\Omega$ (`R5`)
- [x] 2 x Metal film bias resistors $470\text{ k}\Omega$ (`R6`, `R7`)
- [x] 1 x Metal film gain resistor $100\text{ k}\Omega$ (`R10`)
- [x] 4 x Metal film matching network resistors $47\text{ k}\Omega$ (`R3`, `R4`, `R8`, `R9`)
- [x] 1 x Metal film output isolation resistor $100\,\Omega$ (`R11`)
- [x] 1 x LED current limiting resistor $2.2\text{ k}\Omega$ (`R1`)
- [x] 1 x LED current limiting resistor $1\text{ k}\Omega$ (`R2`)
- [x] 2 x Power status indicator green LEDs 3mm (`DL1`, `DL2`)