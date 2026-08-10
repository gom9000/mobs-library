# *PSU Distribution* Module Board
**Module Board Status**: `[Validated]`

8-channel power bus expansion module board.  
This MOB operates across a supply voltage range from $3.3\text{V}$ to $9.0\text{V}$.

![mob-built](mob-psu-distribution_built.jpg)

Multiple MOBs often need to share a single power supply rail. This module provides a centralized power distribution hub, expanding 1 main input line into eight parallel output channels.


## Specifications
| Parameter | Min | Typical | Max | Unit | Notes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Supply Voltage** | 3.3 | 5.0 | 9.0 | V | Main power bus ($V_{CC}$) |
| **Bulk Capacitance** | — | 20 | — | $\mu$F | $2 \times 10\,\mu\text{F}$ Tantalum capacitors |
| **Quiescent Current** | 1.5 | 3.2 | 7.2 | mA | At $V_{CC} = 3.3\text{V}$ / $5.0\text{V}$ / $9.0\text{V}$ ($V_F = 1.8\text{V}$ LED) |
| **Distribution Channels** | — | 8 | — | Channels | Parallel output connectors (`PWR1` to `PWR8`) |
| **Output Voltage Drop** | — | — | — | mV |  No measurable drop at $V_{CC}=9.0\text{V}$, $R_{load}=148\Omega$ |


## Design

### Schematic
![mob-schematic](mob-psu-distribution_sch.jpg)

### Circuit Description
The circuit acts as a common power distribution node. The input power rail (`PWR`) is routed directly in parallel across eight output connectors (`PWR1`–`PWR8`).  

### PCB Layout
![mob-pcb](mob-psu-distribution_pcb.jpg)

## Test Log
The board was tested using a GVDA 30V/10A switching laboratory power supply and a GD128 digital multimeter.

**Quiescent Current**: 
| Supply Voltage | Expected | Measured |
| :---: | :---: | :---: |
| **3.3V** | $1.50\text{mA}$ | $1.43\text{mA}$ |
| **5.0V** | $3.20\text{mA}$ | $3.06\text{mA}$ |
| **9.0V** | $7.20\text{mA}$ | $6.94\text{mA}$ |

*Note: Expected values assume a nominal LED forward voltage $V_F = 1.8\text{V}$, while the actual measured diode drop was $1.9\text{V}$. This difference in $V_F$, together with component tolerances and measurement conditions, accounts for the observed discrepancy.*

<br/>

**Power Distribution & Line Resistance Verification** *(at $V_{CC} = 9.002\text{V}$ and $R_{load} = 148\Omega$)*  
Test performed on PWR4 and PWR8, the physically most distant output channels from the main power input.
| Output | Measured Unloaded $V_0$ | Measured Loaded $V_L$ | Load Current $I$ | Voltage Drop $\Delta V$ | Equivalent Line Resistance $R_{eq}$ |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **PWR4** | $9.002\text{V}$ | $9.002\text{V}$ | $\approx 60.8\text{mA}$ | below measurement resolution | below measurement resolution |
| **PWR8** | $9.002\text{V}$ | $9.002\text{V}$ | $\approx 60.8\text{mA}$ | below measurement resolution | below measurement resolution |

*\*Note: $I = V_L/R_{load}$, $\Delta V = V_0 - V_L$, and $R_{eq} = \Delta V/I$.*


## Bill of Materials
- [x] 1 x Prototyping paperboard 2x8cm
- [x] 9 x 2-pin power connectors (Molex-KK)
- [x] 2 x Tantalum bulk capacitors $10\,\mu\text{F}$ / 16V
- [x] 1 x Current limiting resistor $1\text{k}\Omega$ (for LED)
- [x] 1 x Green power activity LED (3mm)