# *LED Matrix (4x4)* Module Board
**Module Board Status**: `[Prototyped]`

Four-by-four LED indicator matrix output module board.  
This MOB operates across a logic supply voltage range from $3.3\text{V}$ to $5.0\text{V}$.

![mob-built](mob-io-matrix-led-4x4_built.jpg)

This module provides 16 green indicator LEDs arranged in a $4\times4$ multiplexed matrix.


## Specifications
| Parameter | Min | Typical | Max | Unit | Notes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Supply Voltage** | 3.3 | 5.0 | 5.0 | V | Main power bus ($V_{CC}$) |
| **Bulk Capacitance** | — | 10 | — | $\mu$F | Tantalum capacitor ($C$) |
| **Quiescent Current ($I_Q$)** | 1.5 | 3.2 | 3.2 | mA | Idle state (power LED `DL` only) at $3.3\text{V} / 5.0\text{V}$ |
| **Matrix Interface** | — | $4 \times 4$ | — | Lines | 4 Row source inputs (`JR`), 4 Column sink inputs (`JC`) |
| **Row Current Limiters** | — | 1 | — | k$\Omega$ | Integrated per-row series resistor ($R1$–$R4$) |
| **Matrix LED Active Current** | 1.4 | 3.1 | 3.1 | mA | Per active junction ($I_{LED} = (V_{\text{Row}} - V_{\text{Col}} - V_F) / 1\text{k}\Omega$) at $3.3\text{V} / 5.0\text{V}$ |


## Design

### Schematic
![mob-schematic](mob-io-matrix-led-4x4_sch.jpg)

### Circuit Description
The module implements a $4\times4$ multiplexed LED display matrix containing 16 indicator LEDs ($D_{11}$–$D_{44}$). The array is wired in a common-cathode column configuration. The four row lines (`JR`, `rows`) act as current sources and include $1\text{k}\Omega$ series current limiting resistors ($R1$–$R4$). The four column lines (`JC`, `/cols`) act as current sinks. Activating a specific indicator requires multiplexing logic to drive the target row HIGH ($V_{CC}$) while pulling the target column LOW ($GND$). Main power rail decoupling is handled locally by a $10\,\mu\text{F}$ tantalum capacitor (`C`), and board power status is shown by a dedicated green LED (`DL`) with a $1\text{k}\Omega$ resistor (`R`).

### PCB Layout
![mob-pcb](mob-io-matrix-led-4x4_pcb.jpg)


## Bill of Materials
- [x] 1 x Prototyping paperboard 5x7cm
- [x] 1 x 2-pin power connector (Molex-KK)
- [x] 2 x 4-pin data headers (Molex-KK, `JR` Rows, `JC` Columns)
- [x] 1 x Tantalum bulk capacitor $10\,\mu\text{F}$ / 16V ($C$)
- [x] 1 x Power LED limiting resistor $1\text{k}\Omega$ (`R`)
- [x] 1 x Power indicator green LED 3mm (`DL`)
- [x] 4 x Matrix row current limiters $1\text{k}\Omega$ ($R1$–$R4$)
- [x] 16 x Matrix green indicator LEDs 3mm ($D_{11}$–$D_{44}$)