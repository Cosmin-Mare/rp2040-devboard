# RP2040 Dev Board

A small, Pico-style development board built around the **RP2040**, designed in **KiCad 10**. USB-C, 3.3 V LDO, 2 MB QSPI flash, a BOOTSEL button, SWD header, and every GPIO broken out to two 20-pin 2.54 mm headers. 


|          |                                                                            |
| -------- | -------------------------------------------------------------------------- |
| MCU      | Raspberry Pi RP2040 (QFN-56), 12 MHz crystal                               |
| Flash    | Winbond W25Q16JV, 16 Mbit (2 MB) QSPI                                      |
| Power    | USB-C (5 V) → MCP1700-3.3 LDO (250 mA)                                     |
| I/O      | 26 GPIO (incl. 4 ADC), RUN, VBUS, 3V3, GND on headers; 3-pin SWD (1.27 mm) |
| Controls | BOOTSEL button (no reset button – RUN is on a header pin)                  |
| Board    | 21 × 51 mm, 2-layer, 1.6 mm, headers 17.78 mm (700 mil) apart              |
| Assembly | All SMD on the top side (JLCPCB), pin headers hand-soldered                |




## Repository layout

```
hardware/kicad/        KiCad 10 project (schematic + PCB) – the source of truth
fabrication/gerbers/   Gerbers, drill files, .gbrjob exported from KiCad
fabrication/jlcpcb/    Ready-to-upload files: gerbers zip, bom.csv, cpl.csv
fabrication/extras/    IPC-D-356 netlist, ODB++, IPC-2581 XML, KiCad board report (.rpt)
bom/bom.csv            Full BOM with MPN + LCSC numbers
bom/BOM.md             Readable BOM
bom/jlcpcb-bom-match-*.xlsx   JLCPCB's BOM-tool match result (stock/prices at the time)
docs/ORDERING.md       Step-by-step JLCPCB order
docs/ASSEMBLY.md       What JLCPCB places vs. what you solder, plus hand-assembly notes
docs/BRINGUP.md       First power-up, flashing, and test checklist
docs/PINOUT.md         Header pinout
```



## Quick start

1. **Order** – follow [docs/ORDERING.md](docs/ORDERING.md). Upload `fabrication/jlcpcb/devboard-gerbers.zip`, then `bom.csv` and `cpl.csv`.
2. **Solder** the two 20-pin headers (and optionally the SWD header) – see [docs/ASSEMBLY.md](docs/ASSEMBLY.md).
3. **Bring up** – hold BOOTSEL, plug in USB-C, copy a `.uf2` onto the `RPI-RP2` drive. See [docs/BRINGUP.md](docs/BRINGUP.md).



## Editing the design

Open `hardware/kicad/devboard.kicad_pro` in KiCad 10. After changes, re-export Gerbers/drill (`File → Fabrication Outputs`), and the position file (`Fabrication Outputs → Component Placement`, CSV, SMD only, millimetres), then refresh `fabrication/` and `bom/`.