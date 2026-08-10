# *LED Array (8x)* Module Board
**Module Board Status**: `[Validated]`

Eight channel active-high LED output array module board.  
This MOB operates across a logic supply voltage range from $3.3\text{V}$ to $5.0\text{V}$.

![mob-built](mob-io-array-led-8x_built.jpg)

This module provides eight dedicated active-high visual indicator LEDs connected to signal input lines via integrated current limiting resistors.


## Specifications
| Parameter | Min | Typical | Max | Unit | Notes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Supply Voltage** | 3.3 | 5.0 | 5.0 | V | Main power bus  ($V_{CC}$) |
| **Bulk Capacitance** | — | 10 | — | $\mu$F | Tantalum capacitor ($C$) |
| **Quiescent Current ($I_Q$)** | 1.5 | 3.2 | 3.2 | mA | Idle state (power LED `DL` only) at $3.3\text{V} / 5.0\text{V}$ |
| **Input Channels** | — | 8 | — | Lines | Active-high logic inputs (`JA` pins 1–4, `JB` pins 1–4) |
| **Current Limiter Resistance** | — | 1 | — | k$\Omega$ | Integrated per-channel series resistor ($R1$–$R8$) |
| **Logic HIGH Input Threshold** | 2.0 | — | $V_{CC}$ | V | Minimum voltage to light LED ($V_{IH}$) |
| **Channel Active Current** | 1.4 | 3.1 | 3.1 | mA | Per active HIGH line ($I_{CH} = (V_{IN} - V_F) / 1\text{k}\Omega$) at $3.3\text{V} / 5.0\text{V}$ |


## Design

### Schematic
![mob-schematic](mob-io-array-led-8x_sch.jpg)

### Circuit Description
The circuit provides an 8-bit digital output indicator array interfacing digital buses or microcontroller outputs with active-high visual logic status. Data inputs are routed through two 4-pin Molex-KK headers (`JA` and `JB`). Each input line drives a 3mm green indicator LED (`DL1`–`DL8`) in series with a $1\text{k}\Omega$ current limiting resistor ($R1$–$R8$). Power status is indicated by a green LED (`DL`) with a $1\text{k}\Omega$ limiting resistor (`R`), while a $10\,\mu\text{F}$ tantalum capacitor (`C`) provides localized supply decoupling.

### PCB Layout
![mob-pcb](mob-io-array-led-8x_pcb.jpg)


## Test Log
The board was tested using a GVDA 30V/10A switching laboratory power supply and a GD128 digital multimeter.

**Quiescent Current Verification**:
| Supply Voltage | Expected Idle | Idle |
| :---: | :---: | :---: |
| **3.3V** | $1.50\text{mA}$ | $1.40\text{mA}$ |
| **5.0V** | $3.20\text{mA}$ | $3.09\text{mA}$ |

*\*Note: Expected idle values assume nominal LED $V_F = 1.8\text{V}$, while measured diode drop was $1.95\text{V}$.* 

<br/>

**Channel Current Verification**:
| Input Signal Line | Single LED Active | All 8 LEDs Active |
| :---: | :---: | :---: |
| **3.3V** | $1.40\text{mA}$ | $11.5\text{mA}$ |
| **5.0V** | $3.09\text{mA}$ | $24.6\text{mA}$ |

*\*Note: Active channel current is sourced directly from the input signal line, not the main $V_{CC}$ power header.*

<br/>

**Logic Level Response**:
| Signal State | Applied Voltage | Channel LED Status | Logic Level |
| :---: | :---: | :---: | :---: |
| **Input LOW** | $0.0\text{V}$ | **OFF** | **LOW** |
| **Input HIGH** | $V_{CC}$ ($3.30\text{V} / 5.00\text{V}$) | **ON** | **HIGH** |


## Bill of Materials
- [x] 1 x Prototyping paperboard 5x7cm
- [x] 1 x 2-pin power connector (Molex-KK)
- [x] 2 x 4-pin data input connectors (Molex-KK, `JA`, `JB`)
- [x] 1 x Tantalum bulk capacitor $10\,\mu\text{F}$ / 16V ($C$)
- [x] 1 x Power LED limiting resistor $1\text{k}\Omega$ (`R`)
- [x] 1 x Power indicator green LED 3mm (`DL`)
- [x] 8 x Channel LED current limiters $1\text{k}\Omega$ ($R1$–$R8$)
- [x] 8 x Data activity green LEDs 3mm (`DL1`–`DL8`)