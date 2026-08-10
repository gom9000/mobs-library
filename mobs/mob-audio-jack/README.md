# *Audio Jack (Dual 1/4" TRS)* Module Board
**Module Board Status**: `[Validated]`

Dual-channel $1/4"$ ($6.35\text{mm}$) TRS audio jack interface and routing module board.  
This passive MOB handles standard analog line-level or instrument-level audio signals.

![mob-built](mob-audio-jack_built.jpg)

This module breaks out two independent $1/4"$ TRS (Tip, Ring, Sleeve) phone jacks into internal system headers. Each channel features localized DC blocking/filter capacitors, dedicated stereo (3-pin) and mono (2-pin) outputs, and a manual routing jumper to select the mono source channel.


## Specifications
| Parameter | Min | Typical | Max | Unit | Notes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Channels** | — | 2 | — | Qty | Fully independent isolated audio structures |
| **Connector Type** | — | 1/4" TRS | — | Inch | Standard $6.35\text{mm}$ stereo chassis jack |
| **Coupling Capacitance**| — | 4.7 | — | $\mu$F | Electrolytic filtering per signal line ($C1$–$C4$) |
| **Stereo Output** | — | 3 | — | Pins | Molex-KK port (`JTRS1`, `JTRS2`) |
| **Mono Output** | — | 2 | — | Pins | Molex-KK port (`JTS1`, `JTS2`) |
| **Signal Configuration**| — | Mono/Stereo| — | — | Jumper selectable routing layout |


## Design

### Schematic
![mob-schematic](mob-audio-jack_sch.jpg)

### Circuit Description
The board houses two separate audio channels built around switched $1/4"$ TRS jacks (`TRS1`, `TRS2`). The Sleeve (S) connection provides a common ground chassis tie across the design. The Tip (T) and Ring (R) lines pass through $4.7\,\mu\text{F}$ polarized capacitors ($C1$–$C4$) to filter the baseline analog signals. 

Each block features two distinct output routing footprints:
1. **`JTRSx` (Stereo Out)**: Directly taps the Tip, Ring, and Sleeve lines for standard multi-channel downstream operations.
2. **`JTSx` (Mono Out)**: Connects via a 3-pin selector header (`JSW1`, `JSW2`). Moving the jumper shunt changes the input source fed to the 2-pin mono connector. Positioning the shunt on pins 1-2 bridges the active **Ring** line, while positioning it on pins 2-3 (square pad indicator) bridges the active **Tip** line, enabling custom Left/Right manual routing onto mono sub-buses.

### PCB Layout
![mob-pcb](mob-audio-jack_pcb.jpg)


## Bill of Materials
- [x] 1 x Prototyping paperboard 5x7cm
- [x] 2 x 1/4" ($6.35\text{mm}$) TRS PCB-mount stereo phone jacks (`TRS1`, `TRS2`)
- [x] 2 x 3-pin stereo audio output headers (Molex-KK, `JTRS1`, `JTRS2`)
- [x] 2 x 2-pin mono audio output headers (Molex-KK, `JTS1`, `JTS2`)
- [x] 2 x 3-pin male selector headers with shorting shunts (`JSW1`, `JSW2`)
- [x] 4 x Aluminum electrolytic capacitors $4.7\,\mu\text{F}$ / 25V or higher ($C1$–$C4$)