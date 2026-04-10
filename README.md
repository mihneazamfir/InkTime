# InkTime — Open Source E-Paper Smartwatch

InkTime este un smartwatch open-source, accesibil, construit în jurul microcontrolerului Nordic nRF52840 și al unui display e-paper, optimizat pentru consum redus de energie și autonomie ridicată.

---

## Overview

Sistemul este centrat pe nRF52840 și integrează multiple periferice prin SPI, I2C și GPIO:

- Display e-paper (SPI)
- Baterie LiPo + sistem de încărcare
- Accelerometru (detecție mișcare)
- Driver haptic (feedback vibrații)
- Fuel gauge (monitorizare baterie)
- Regulator buck-boost (alimentare stabilă)
- USB-C pentru încărcare și comunicație

---

## Main Components

- **nRF52840** — MCU principal (BLE 5.0, Cortex-M4)
- **BQ25180** — încărcător LiPo cu I2C
- **BMA423** — accelerometru + step counter
- **DRV2605** — driver haptic
- **MAX17048** — fuel gauge
- **RT6160** — regulator buck-boost 3.3V
- Antenă 2.4 GHz, USB-C, cristale, pasive

---

## Hardware Functionality

### Microcontroller

nRF52840 rulează la 64 MHz și include:
- Bluetooth 5.0
- Criptografie hardware
- USB 2.0 full-speed

Cristale utilizate:
- **32 MHz** (RF)
- **32.768 kHz** (low-power / RTC)

---

### E-Paper Display

- Conectare prin **SPI**
- Control suplimentar prin GPIO (DC, RST, BUSY)
- Alimentare controlată separat pentru eficiență energetică

---

### Power Management

- **BQ25180** gestionează încărcarea bateriei LiPo
- **RT6160** oferă tensiune stabilă de 3.3V
- **MAX17048** estimează nivelul bateriei fără rezistor de măsură

---

### Sensors & Feedback

- **BMA423** detectează mișcarea și poate genera interrupturi
- **DRV2605** controlează motorul de vibrații

---

### USB & Debug

- USB-C pentru alimentare și comunicație
- Protecție ESD pe liniile USB
- Debug prin interfață **SWD** (Tag-Connect / Test pad-uri)

---

### Buttons

- 3 butoane: **UP, ENTER, DOWN**
- Debounce hardware (RC)

---

### RF Section

- Antenă 2.4 GHz optimizată
- Fără trasee sau plan de masă sub antenă

---

## Pin Configuration

- **SPI** → display e-paper
- **I2C** → senzori și management baterie
- **GPIO** → butoane și control periferice

Selectarea pinilor a fost făcută pentru:
- Trasee scurte pe PCB
- Flexibilitate
- Compatibilitate hardware

---

## Power Consumption (Estimated)

| Mode | Consumption |
|------|-------------|
| Active (BLE) | ~15 mA |
| EPD refresh | ~33 mA |
| Haptic feedback | ~65 mA |
| Deep sleep | ~3 µA |

Autonomie estimată (180 mAh): **5–7 zile**

---

## Test Points

Placa include puncte de test pentru:

- `3.3V`, `VBAT`, `GND`
- `SDA`, `SCL` (I2C)
- `SWDIO`, `SWDCLK` (Debug)
- `RESET`
- Motor haptic

---

## Design Decisions

- PCB de **1 mm grosime**
- Componente doar pe stratul **TOP**
- Planuri de masă pe ambele straturi
- Fără cupru sub antenă
- Trasee optimizate (45°, fără unghiuri de 90°)
- Conexiune directă baterie (fără conector)

---

## Repository Structure

```text
InkTime/
├── Hardware/              # Schematică și layout PCB
│   ├── InkTime.sch
│   └── InkTime.brd
├── Manufacturing/         # Fișiere pentru producție
│   ├── Gerbers.zip
│   ├── InkTime_BOM.bom
│   └── InkTime_PnP.cpl
├── Mechanical/            # Modele 3D
│   ├── InkTime.f3z
│   └── InkTime_Exploded.f3z
├── Images/                # Randări și imagini
├── LICENSE
└── README.md
```

---

## Licență

Proiectul este distribuit sub **Apache License 2.0** — vezi fișierul [LICENSE](LICENSE).