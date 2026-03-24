# B302

B302 is an **8-channel high-voltage AC input module** designed to convert **220 VAC class input signals into isolated 3.3 V TTL-compatible sense outputs**. The board is built in a Mini PCI Express style form factor and is intended to be used as a host-pluggable input card for embedded and industrial control systems.

This repository is an **Altium Designer hardware design repository**. It contains the project files, schematics, PCB layout and generated manufacturing/output artifacts used to review, manufacture or extend the board.

## What This Board Does

From the schematic set, B302 is a **220 V to TTL input module** with **8 isolated sensing channels**. Each channel accepts a high-voltage AC input and produces a logic-level sense output for the host side.

At a high level, the board provides:

- **8 independent AC input channels**
- **galvanic signal isolation** per channel
- **3.3 V TTL-compatible sense outputs**
- a **Mini PCIe style host connector**
- a compact interface card approach for systems that need multiple high-voltage presence/status inputs

## Main Design Approach

The design is organized as a repeated per-channel isolation structure. Each input channel uses a resistor network sized for mains-class voltage sensing and an isolation stage that converts the input presence into a host-side logic signal.

The schematics indicate:

- nominal input assumption around **230 VAC**
- worst-case design check up to **400 VAC**
- resistor chain sizing repeated per channel
- logic-side outputs labeled as **SENSE_1 ... SENSE_8**
- outputs described as **active low** on the 3.3 V side

This makes the board suitable for monitoring the presence of AC signals in applications where the host controller must remain at logic-level voltage while field wiring stays on the high-voltage side.

## Functional Blocks

### 1. High-Voltage Input Connector
A dedicated input connector exposes the 8 field inputs:

- `INPUT_1` to `INPUT_8`

This is the high-voltage side of the design and should be treated accordingly during integration, PCB review and assembly.

### 2. Eight Repeated Isolation Channels
The core of the board is a repeated signal isolation channel for each AC input.

Each channel includes:

- a high-value resistor network for voltage/current limiting
- an isolation stage
- a logic-side sense output

The schematics also include explicit power dissipation and worst-case calculations, which is a good sign that the sensing network was dimensioned deliberately rather than heuristically.

### 3. Host Interface
The board exposes its low-voltage logic signals through a Mini PCIe style edge connector. From the schematic, the host side includes:

- 3.3 V supply feeds
- GND
- `SENSE_1` to `SENSE_8`
- connector-side enable/control style lines inherited from the connector standard footprint

This means the board behaves as an interface/input card rather than a standalone product.

## Intended Use Cases

B302 is well suited to applications where a controller must detect the presence of AC mains-class signals while keeping the host electronics at low voltage. Example use cases include:

- industrial monitoring systems
- machine status detection
- contactor / relay state sensing
- mains presence detection
- panel and field I/O expansion
- agricultural or utility automation systems

## Safety and Design Notes

This board interfaces with **high voltage**. The schematic pages explicitly mention PCB copper clearance considerations and channel resistor power calculations.

Important practical notes:

- treat the input side as hazardous voltage during review, bring-up and use
- verify creepage/clearance rules against the target standard and enclosure conditions
- verify resistor voltage rating, package stress and production tolerances for the intended installation class
- validate isolation behavior and input assumptions in the final use environment

This repository shares the hardware design sources, but safe integration remains the responsibility of the integrator.

## Repository Structure

| Path | Purpose |
|---|---|
| `B302.PrjPcb` | Main Altium project file |
| `B302.PcbDoc` | PCB layout document |
| `Schematics/` | Schematic source files |
| `B302.BomDoc` | Bill of materials document |
| `Output/` | Generated outputs such as schematic prints, fabrication and review artifacts |
| `Job File.OutJob` | Output generation settings |

## Schematic Overview

The published schematic set is structured around:

- a block diagram
- the host/card edge connector
- eight separate signal isolation pages
- the high-voltage input connector

This is a clean and reviewable structure for a repeated multi-channel input board.

## Tooling Requirements

To inspect and modify the project properly, the recommended tooling is:

- **Altium Designer** for native project editing
- PDF tools for schematic review
- CAM/Gerber viewers for manufacturing output inspection

## Notes for Reviewers

The current repository already contains the essential hardware design files, but it can be strengthened further with:

- board photos or renders
- a short mechanical/connector note
- explicit licensing
- a quick integration example showing how the host interprets the sense outputs

## License

A repository-level license file is not currently visible. If this project is intended for broader open reuse, adding an explicit `LICENSE` file is recommended.
