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
---

<img width="770" height="792" alt="Captura de pantalla 2026-11-06 234343" src="https://github.com/user-attachments/assets/049a851a-451e-4e19-b8ce-4c590a26c6e1" />

---

# Schematic

---

<img width="1253" height="828" alt="Captura de pantalla 2026-11-06 234321" src="https://github.com/user-attachments/assets/0e25b663-9cdf-4afc-aaeb-fc756fe4061c" />

