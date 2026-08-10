# Electronics Module Boards Library
A collection of modular electronics boards (MOBs) and CAD resources for rapid prototyping and interfacing.

![overview](images/overview.jpg)

These MOdule Boards (MOBs) are useful for:
* doing experiences
* testing specific components functions
* prototyping complex projects by modular approach
* interfacing and expanding hardware sub-systems
* having fun building simple circuits


## The MOBs Library
**MOdule Boards Status Legend**
- **`[Designed]` Development**: Layout and schematics completed. Ready for physical build.
- **`[Prototyped]` Built**: Physical board assembled. Ready for bench testing.
- **`[Validated]` Tested**: Verified on the bench and circuit documentation is finalized.

### MOBs for PSU eXPeriences
| Module | Description | Voltage Range | Status |
| :--- | :--- | :---: | :---: |
| [mob-psu-5v](mobs/mob-psu-5v/) | Linear 5V ($V_{CC}$) PSU | 5.0V | `[Designed]` |
| *[mob-psu-cbank-26.4mF](mobs/mob-psu-cbank-26.4mF/)* | *26.4 mF Capacitor bank* | *3.3–5.0V* | *`[Prototyped]`* |
| [mob-psu-distribution](mobs/mob-psu-distribution/) | Eight-lines power bus expansion | 3.3–9.0V | `[Validated]` |
| [mob-psu-vdivider-pot-2x](mobs/mob-psu-vdivider-pot-2x/) | Dual potentiometers voltage-divider | 3.3–9.0V | `[Validated]` |
| [mob-psu-vdivider-buf](mobs/mob-psu-vdivider-buf/) | Dual buffered voltage divider ($V_{CC}/2$ and $V_{CC}/4$ references) | 3.3–9.0V | `[Designed]` |

### MOBs for Digital eXPeriences
| Module | Description | Voltage Range | Status |
| :--- | :--- | :---: | :---: |
| [mob-io-array-led-8x](mobs/mob-io-array-led-8x/) | Eight LED output array | 3.3–5.0V (logic) | `[Validated]` |
| [mob-io-array-switch-8x](mobs/mob-io-array-switch-8x/) | Eight switch input array | 3.3–5.0V (logic) | `[Validated]` |
| *[mob-io-array-switch-and-led-4x](mobs/mob-io-array-switch-and-led-4x/)* | *Quad switch input array and quad LED output array* | *3.3–5.0V (logic)* | *`[Prototyped]`* |
| [mob-io-matrix-led-4x4](mobs/mob-io-matrix-led-4x4/) | 4x4 output led matrix | 3.3–5.0V (logic) | `[Designed]` |
| [mob-io-matrix-switch-4x4](mobs/mob-io-matrix-switch-4x4/) | 4x4 input switch matrix | 3.3–5.0V (logic) | `[Prototyped]` |
| [mob-if-midi](mobs/mob-if-midi/) | MIDI IN/OUT/THRU interface | 3.3–5.0V (logic) | `[Validated]` |
| [mob-if-rs232](mobs/mob-if-rs232/) | RS-232 interface | 5.0V (logic) | `[Designed]` |
| [mob-mcu-pic16f6x8](mobs/mob-mcu-pic16f6x8/) | Microchip PIC16F6x8 microcontroller board | 5.0V (logic) | `[Prototyped]` |

### MOBs for Audio eXPeriences
| Module | Description | Voltage Range | Status |
| :--- | :--- | :---: | :---: |
| [mob-audio-psu-9v-5v](mobs/mob-audio-psu-9v-5v/) | Dual linear 9V ($V_{CC}$) and 5V ($V_{DD}$ or $V_{REF}$) PSU | 5.0–9.0V | `[Prototyped]` |
| [mob-audio-jack](mobs/mob-audio-jack/) | Audio TRS jack 1/4" to pin-header adapter | — | `[Validated]` |
| [mob-audio-io-stage](mobs/mob-audio-io-stage/) | Audio input and output buffered stages | 5.0–9.0V | `[Prototyped]` |


## Specifications
Schematics and PCB layouts are designed with ExpressPCB free CAD software.

### MOBs naming convention
* `mob` (module board base)
* `mob-psu` (power supply & power conditioning units)
* `mob-io` (digital & analog input/output units)
* `mob-if` (communication & interface units)
* `mob-fn` (specialized function controller units)
* `mob-mcu` (microcontroller host units)
* `mob-audio` (audio signal chain units)

### Standard Hardware Rules
* **Paperboard Grid Sizes**: $2\times8\text{cm}$, $4\times6\text{cm}$, $5\times7\text{cm}$, $7\times10\text{cm}$
* **Power Connection**: Standard power connector (`PWR`) with positive pin on the left, bulk capacitor ($C$), and power-on indicator LED (`DL`).
* **Activity Indicator LEDs**:
  * 3mm Green LED: Power status
  * 3/5mm Green LED: Normal activity
  * 3/5mm Yellow LED: Warning status
  * 3/5mm Red LED: Error / fault status
  * 3/5mm Blue LED: Manual intervention required

### Design Rationale
To maintain consistency and simplify assembly across all MOBs, the following baseline rules were adopted:

* **LED Current Limiters ($1\text{k}\Omega$ @ 3V3 and 5V, $2.2\text{k}\Omega$ @ 9V)**: 
  Calculated for standard 3mm/5mm LEDs to target $I_F \approx 3\text{mA} - 4\text{mA}$. This provides clear visual indication while minimizing total power consumption on the supply rails.
* **Digital Line Pull-Ups ($10\text{k}\Omega$)**: 
  Standard trade-off value offering noise immunity for low-frequency/static digital lines while keeping active-LOW state power waste below $0.5\text{mA}$ (@ 5V). 
  For high-impedance CMOS logic inputs, the voltage drop across the resistor is negligible ($V_{IH} \approx V_{CC}$). For TTL inputs (where input leakage current $I_{IH}$ causes a small voltage drop $V_{drop} = I_{IH} \cdot R$), a single $10\text{k}\Omega$ pull-up maintains $V_{IH}$ well above the TTL logic HIGH threshold ($2.0\text{V}$).
* **IC Decoupling ($100\text{nF}$ Ceramic)**: 
  Placed as close as possible to IC power supply pins to suppress high-frequency switching transients and localized noise.
* **Board Bulk Capacitance ($10\mu\text{F}$ Tantalum/Electrolytic)**: 
  Acts as a local energy reservoir to smooth out low-frequency power supply ripple and step-load variations across board interconnects.

### ExpressPCB Custom Component Library
Layouts and schematics are designed using ExpressPCB (free CAD software) and the custom library stored in [`expresspcb/`](expresspcb):
* Custom components follow the format `_MOB_<name>_<size>`
* Board templates follow the format `_MOB__Paperboard_<size>`
* ExpressPCB size units are $1/10$ of an inch ($0.1"$)
* Standard trace width: **$0.05"$ ($50\text{ mil}$)**, pad diameter: $0.065"$
  * *Note*: A $50\text{ mil}$ trace on 1 oz copper provides up to $\approx 900\text{mA}$ continuous current capability under worst-case thermal and loading constraints ($50^\circ\text{C}$ ambient, $J = 20\,\text{A/mm}^2$ conservative density), while bounding ohmic drop below $20\text{mV}$ on standard board runs (ref. [xp-hardware#](https://github.com/gom9000/xp-hardware/tree/master/hardware-notes/conductors-and-wiring)).


## Changes
See file [CHANGES](CHANGES.md) for the project resources change log.


## Future Plans for the MOBs Library
* Add more MOBs!


## About & License
**Author**: Alessandro Fraschetti (gom9000).  
**Technical Notes**: The hardware design was supported by **ExpressPCB** and the custom **[expresspcb-goslib](https://github.com/gom9000/expresspcb-goslib)** libraries.  
**License**: This project is licensed under the [MIT License](LICENSE).
