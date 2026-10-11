# RP2040 Dev Board


<img width="1269" height="846" alt="Screenshot 2026-10-11 at 2 26 41 PM" src="https://github.com/user-attachments/assets/33a702c3-0835-4636-8525-38b520564317" />
<img width="326" height="785" alt="Screenshot 2026-10-11 at 2 27 03 PM" src="https://github.com/user-attachments/assets/2645560e-9a99-4b38-8ff8-fcd9dfed3a3f" />

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

## Bill of Materials

Per board. 33 parts total (16 line items). Full data incl. manufacturer/MPN in [bom.csv](bom.csv).

| Designators | Qty | Value | Footprint | MPN | LCSC | Assembled by JLCPCB |
|---|--:|---|---|---|---|---|
| C1,C10 | 2 | 1uF | C_0402_1005Metric | CL05A105KA5NQNC | [C52923](https://www.lcsc.com/product-detail/C52923.html) | Yes |
| C2,C3,C4,C5,C6,C7,C8,C9,C11,C12,C17 | 11 | 0.1uF | C_0402_1005Metric | CL05B104KO5NNNC | [C1525](https://www.lcsc.com/product-detail/C1525.html) | Yes |
| C13,C14 | 2 | 10uF | C_0603_1608Metric | CL10A106KP8NNNC | [C19702](https://www.lcsc.com/product-detail/C19702.html) | Yes |
| C15,C16 | 2 | 33pF | C_0402_1005Metric | 0402CG330J500NT | [C1562](https://www.lcsc.com/product-detail/C1562.html) | Yes |
| J1 | 1 | USB_C_Receptacle_USB2.0_14P | USB_C_Receptacle_HRO_TYPE-C-31-M-12 | TYPE-C-31-M-12 | [C165948](https://www.lcsc.com/product-detail/C165948.html) | Yes |
| J2,J3 | 2 | Conn_01x20 | PinHeader_1x20_P2.54mm_Vertical | 2.54-1*20P直针 | [C50981](https://www.lcsc.com/product-detail/C50981.html) | No (hand-solder) |
| J4 | 1 | Conn_01x03 | PinHeader_1x03_P2.54mm_Vertical | 1.27-1*3P针 | [C24980](https://www.lcsc.com/product-detail/C24980.html) | No (hand-solder) |
| R1,R2 | 2 | 5.1k | R_0402_1005Metric | 0402WGF5101TCE | [C25905](https://www.lcsc.com/product-detail/C25905.html) | Yes |
| R3,R4 | 2 | 27 | R_0402_1005Metric | 0402WGF270JTCE | [C25100](https://www.lcsc.com/product-detail/C25100.html) | Yes |
| R5,R7 | 2 | 1k | R_0402_1005Metric | 0402WGF1001TCE | [C11702](https://www.lcsc.com/product-detail/C11702.html) | Yes |
| R6 | 1 | 10k | R_0402_1005Metric | 0402WGF1002TCE | [C25744](https://www.lcsc.com/product-detail/C25744.html) | Yes |
| SW1 | 1 | SW_Push | SW_Push_SPST_NO_Alps_SKRK | TS-1088-AR02016 | [C720477](https://www.lcsc.com/product-detail/C720477.html) | Yes |
| U1 | 1 | RP2040 | QFN-56-1EP_7x7mm_P0.4mm_EP3.2x3.2mm | RP2040 | [C2040](https://www.lcsc.com/product-detail/C2040.html) | Yes |
| U2 | 1 | MCP1700x-330xxTT | SOT-23 | MCP1700T-3302E/TT | [C39051](https://www.lcsc.com/product-detail/C39051.html) | Yes |
| U3 | 1 | W25Q16JVZPIQTR | Winbond_USON-8-1EP_3x2mm_P0.5mm_EP0.2x1.6mm | W25Q16JVUXIQ | [C2843335](https://www.lcsc.com/product-detail/C2843335.html) | Yes |
| Y1 | 1 | 12MHz | Crystal_SMD_3225-4Pin_3.2x2.5mm | X322512MSB4SI | [C9002](https://www.lcsc.com/product-detail/C9002.html) | Yes |
