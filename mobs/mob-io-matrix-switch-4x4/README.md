# *Switch Matrix (4x4)* Module Board
**Module Board Status**: `[Prototyped]`

Four-by-four active-low key matrix input module board with anti-ghosting diodes.  
This MOB operates across a logic supply voltage range from $3.3\text{V}$ to $5.0\text{V}$.

![mob-built](mob-io-matrix-switch-4x4_built.jpg)

This module provides 16 tactile switches arranged in a $4\times4$ scanned matrix. Integrated row pull-ups and series anti-ghosting diodes allow reliable multi-key sensing using only 8 I/O lines.


## Specifications
| Parameter | Min | Typical | Max | Unit | Notes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Supply Voltage** | 3.3 | 5.0 | 5.0 | V | Main power bus ($V_{CC}$) |
| **Bulk Capacitance** | — | 10 | — | $\mu$F | Tantalum capacitor ($C$) |
| **Quiescent Current ($I_Q$)** | 1.5 | 3.2 | 3.2 | mA | Idle state (no keys pressed, power LED `DL` only) at $3.3\text{V} / 5.0\text{V}$ |
| **Matrix Interface** | — | $4 \times 4$ | — | Lines | 4 Row outputs (`JR`), 4 Column inputs/strobe (`JC`) |
| **Row Pull-up Resistance** | — | 10 | — | k$\Omega$ | Integrated per-row pull-up ($R1$–$R4$) |
| **Diode Forward Voltage Drop ($V_F$)** | — | 0.7 | — | V | Anti-ghosting signal diodes ($D_{11}$–$D_{44}$) |
| **Active Scan Current** | 0.26 | 0.43 | 0.43 | mA | Per pressed key during active column LOW scan step |


## Design

### Schematic
![mob-schematic](mob-io-matrix-switch-4x4_sch.jpg)

### Circuit Description
The module implements a $4\times4$ multiplexed matrix for 16 SPST tactile switches ($SW_{11}$–$SW_{44}$). The four row lines (`JR`) are tied HIGH to $V_{CC}$ via integrated $10\text{k}\Omega$ pull-up resistors ($R1$–$R4$). The four column lines (`JC`, `/cols`) are sequentially driven LOW by a microcontroller scan routine. When a switch is pressed, grounding the corresponding column pulls the associated row line LOW (minus the $V_F$ drop of the series diode). Signal diodes ($D_{11}$–$D_{44}$) prevent back-feeding and ghost key reads during simultaneous multi-key presses. Local power filtering is provided by tantalum capacitor `C` ($10\,\mu\text{F}$), with power status indicated by green LED `DL` and resistor `R` ($1\text{k}\Omega$).

### PCB Layout
![mob-pcb](mob-io-matrix-switch-4x4_pcb.jpg)


## Test Log
The board was tested using a GVDA 30V/10A switching laboratory power supply and a GD128 digital multimeter.

**Quiescent Current Verification**:
| Supply Voltage | Expected Idle | Idle (No Keys Pressed) |
| :---: | :---: | :---: |
| **3.3V** | $1.50\text{mA}$ | $1.44\text{mA}$ |
| **5.0V** | $3.20\text{mA}$ | $3.08\text{mA}$ |

*\*Note: Expected idle values assume nominal LED $V_F = 1.8\text{V}$, while measured diode drop was $1.95\text{V}$.*

<br/>

**Active Scan Current Verification**:
| Supply Voltage | Measured Row Voltage ($V_F$) | Measured Current ($I_{KEY}$) |
| :---: | :---: | :---: |
| **3.3V** | $0.56\text{V}$ | $0.28\text{mA}$ |
| **5.0V** | $0.60\text{V}$ | $0.45\text{mA}$ |

<br/>

**Matrix Scan Logic Verification**:
| Column State (`JC`) | Switch State | Row Reading (`JR`) | Logical Output |
| :---: | :---: | :---: | :---: |
| **Strobe LOW ($0.0\text{V}$)** | **Open** | $V_{CC}$ ($3.3\text{V} / 5.0\text{V}$) | **Key OFF (HIGH)** |
| **Strobe LOW ($0.0\text{V}$)** | **Pressed** |$V_{F}$ | **Key ON (LOW)** |
| **Idle / Hi-Z / HIGH** | **Pressed / Open** | $V_{CC}$ ($3.3\text{V} / 5.0\text{V}$) | **Key OFF (HIGH)** |

*\*Note: Current during active LOW scan step is $I_{KEY} = (V_{CC} - V_F) / 10\text{k}\Omega \approx 0.43\text{mA}$ @ 5V.*


## Bill of Materials
- [x] 1 x Prototyping paperboard 5x7cm
- [x] 1 x 2-pin power connector (Molex-KK)
- [x] 2 x 4-pin data headers (Molex-KK, `JR` Rows, `JC` Columns)
- [x] 1 x Tantalum bulk capacitor $10\,\mu\text{F}$ / 16V ($C$)
- [x] 1 x Power LED limiting resistor $1\text{k}\Omega$ (`R`)
- [x] 1 x Power indicator green LED 3mm (`DL`)
- [x] 4 x Row pull-up resistors $10\text{k}\Omega$ ($R1$–$R4$)
- [x] 16 x Signal anti-ghosting diodes (1N4148 or equivalent, $D_{11}$–$D_{44}$)
- [x] 16 x SPST NO tactile pushbuttons ($SW_{11}$–$SW_{44}$)