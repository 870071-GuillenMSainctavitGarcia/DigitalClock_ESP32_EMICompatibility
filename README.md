# DigitalClock_ESP32_EMICompatibility

A 2-layer custom hardware board designed in **KiCad 9.0** featuring dual isolated ground planes (`GND` and `GND1`), input noise filtering, an onboard 12V-to-5V buck regulator, and Wi-Fi capabilities for acquiring UTC time via NTP.

---

##  Features

- **ESP32 Microcontroller:** Integrated module layout with a dedicated antenna exclusion zone to maximize Wi-Fi & Bluetooth RF performance.
- **Dual Isolated Ground Planes:** Independent `GND` and `GND1` domains to prevent noise coupling across high-voltage input and digital control sections.
- **Power Management:**
  - **Input Filtering:** Common Mode Choke & Pi Filter ($C-L-C$) for supply line noise suppression.
  - **Buck Regulator:** High-efficiency $12\text{V} \to 5\text{V}$ DC-DC step-down switching converter (TSOT-23-8 footprint).
- **Peripherals & Debugging:**
  - Onboard I2C sensor interface with pull-up resistors (`SDA` / `SCL`).
  - Strategic Test Points (`12V_TP`, `5V_TP`, `3V3_TP`, `SDA_TP`, `SCL_TP`, `GND_TP`).
- **DFA / DFM Compliant:** 2-layer stackup optimized for JLCPCB manufacturing rules (0.15 mm minimum clearance).

---

##  Hardware Specifications

| Parameter | Value |
| :--- | :--- |
| **Input Voltage** | 12V DC |
| **Regulated Voltages** | 5V DC (Buck Converter Output), 3.3V DC (ESP32 LDO) |
| **PCB Stackup** | 2 Layers (`F.Cu` signal routing & components, `B.Cu` ground plane) |
| **EDA Software** | KiCad 9.0 |
| **Minimum Clearance** | 0.15 mm (6 mil) |
| **Drill Format** | Excellon Merged (PTH + NPTH) |
| **Gerber Format** | Extended Gerber RS-274X (Protel File Extensions) |

---

# PCB and Layout

- **Layer Architecture:**
  - **Top Layer (`F.Cu`):** Primary routing layer for SMD components, power distribution traces, and signal lines.
  - **Bottom Layer (`B.Cu`):** Dedicated low-impedance continuous ground plane for optimal return paths and EMI reduction.
- **Isolated Ground Planes (`GND` vs `GND1`):**
  - **`GND1` Domain:** Isolated ground fill surrounding the $12\text{V}$ power input, protection diode, and Pi filter stage to contain input switching noise.
  - **`GND` Domain:** Main system ground covering the buck regulator output stage, ESP32 module, and digital peripherals.
- **RF Antenna Keepout Zone:**
  - Full copper clearance on all layers directly underneath the ESP32 PCB antenna region to prevent RF attenuation and maintain maximum Wi-Fi/Bluetooth range.
- **Power Routing & Via Placement:**
  - Expanded track widths ($0.8\text{ mm} - 1.2\text{ mm}$) for $12\text{V}$ input, switching nodes, and $5\text{V}$ power rails.
  - Low-inductance ground vias placed in immediate proximity to SMD ground pads for direct bottom-layer stitching.
- **Design Rules (DRC):**
  - Optimized $0.15\text{ mm}$ ($6\text{ mil}$) trace clearance to accommodate high-density TSOT-23-8 IC footprints without manufacturing rule violations.
---

<img width="770" height="792" alt="Captura de pantalla 2026-11-06 234343" src="https://github.com/user-attachments/assets/049a851a-451e-4e19-b8ce-4c590a26c6e1" />

---

# Schematic

The schematic is divided into distinct functional blocks optimized for power integrity, noise isolation, and ease of debugging:

### 1. Power Input & Isolated Domain (`GND1`)
- **Input Terminal:** $12\text{V}$ DC main supply connection (`J2`).
- **Protection Stage:** Schottky diodes (`D1`, `D3`) providing reverse-polarity protection and transient voltage suppression.
- **Noise Filtering:** Dual-stage EMI filtering using a Common Mode Choke (`FL1`) and a Pi Filter ($C-L-C$) to prevent external noise from entering the board.

### 2. Step-Down Buck Converter ($12\text{V} \to 5\text{V}$)
- **Regulator Core:** High-efficiency DC-DC switching regulator (`U1`, TSOT-23-8 footprint).
- **LC Output Filter:** High-current power inductor (`L1`) paired with low-ESR ceramic capacitor banks (`C1`–`C16`) for low output voltage ripple under dynamic loads.

### 3. ESP32 Microcontroller Core (`U2`)
- **Main Processing Unit:** ESP32 module powered from the main $5\text{V}$ rail (converted to $3.3\text{V}$ via internal LDO).
- **Wireless Connectivity:** Optimized for Wi-Fi synchronization to fetch real-time UTC timestamps via NTP servers.

### 4. Sensor & Peripheral Interface
- **I2C Bus:** Dedicated MSOP-8 sensor interface (`U3`) and expansion header (`J3`) with integrated pull-up resistors (`RPullUp-SCL1`, `RPullUp-SDA1`).

### 5. Diagnostic Test Points
- Strategic test pads placed across key nets for oscilloscope and multimeter probing:
  - **Power Rails:** `12V_TP1`, `12VE_TP2`, `5V_TP5`, `3V3_TP7`
  - **Signals:** `SCL_TP9`, `SDA_TP8`
  - **Ground References:** `GND_TP3`, `GND_TP4`, `GND1_TP10`
---

<img width="1253" height="828" alt="Captura de pantalla 2026-11-06 234321" src="https://github.com/user-attachments/assets/0e25b663-9cdf-4afc-aaeb-fc756fe4061c" />

