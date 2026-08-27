# Bill of materials

Everything here is off-the-shelf or 3D printed — no machining. This build is stock, so the list
matches [upstream's BOM](https://github.com/wahabk/Clinostat/blob/main/docs/2_BOM.md); upstream puts
the total at **around £100**.

## Electronics

| Qty | Part | Specification | Notes |
|----:|------|---------------|-------|
| 1 | Arduino | Your choice of board | The sketch uses only digital pins 2–8 plus hardware SPI |
| 2 | Stepper motor | NEMA 17, 0.42 Nm | 200 steps/rev (1.8°/step) |
| 2 | Stepper driver | A4988 (cheap) or TMC2208 | TMC2208 runs quieter with less vibration. Must be set to 16× microstepping |
| 1 | Power supply | Sized to your motors and drivers | |
| 1 | MicroSD card reader | 5 V, 6-pin SPI | **Optional** — only needed for partial-gravity path following |
| — | Hookup wire, connectors | | |

## Mechanical

| Qty | Part | Specification | Notes |
|----:|------|---------------|-------|
| 12 | Skateboard bearings | 8 mm ID, 22 mm OD | Standard 608-size |
| 2 | GT2 belt | 200 mm, 6 mm wide | The two short belts |
| 1 | GT2 belt | 500 mm, 6 mm wide | The long `m2y` belt |
| 2 | Stepper timing pulley | 16 tooth | Motor pulleys |
| 1 | GT2 pulley (`y_pulley`) | 30 tooth, 8 mm bore, 6 mm wide | Off-the-shelf since upstream v0.4 — no longer a printed part |
| 1 | Aluminium extrusion | 1 m × 20 mm × 20 mm | Cut in half for the base rails |
| 1 | Filament | 1 kg, your choice | PLA works; PETG preferred |

## Bolts and washers

| Qty | Part | Specification |
|----:|------|---------------|
| 4 | Hex bolts | M8 × 60 mm |
| 2 | Hex bolts | M8 × 100 mm |
| 8 | Allen bolts | M3 × 12 mm |
| 12 | Allen bolts | M5 × 16 mm |
| 13 | Washers | M8 (8 mm ID, 16 mm OD) |

## Printed parts

See [`../3d_files/README.md`](../3d_files/README.md) for the full list with quantities and print
settings.

## Tools

| Tool | Size | Used for |
|---|---|---|
| Spanner/wrench | 13 mm | M8 nuts (same as a skateboard tool) |
| Allen key | 3 mm | Base |
| Allen key | 2 mm | Motors and bodies |
| Allen key | 1.5 mm | Motor pulley grub screws |

## Sample handling

The upstream design does **not** specify a sample chamber — the BOM has no vessel or holder, and
mounting is left to the builder. Whatever you use has to be fixed inside the Y body so it can't shift
during rotation.

<!-- Fill in once decided: the vessel used (falcon tube, petri dish, etc.), how it's secured, and
     the payload mass. -->

## Sourcing notes

<!-- Fill in as you buy: what was hard to find, what arrived wrong, what you'd substitute, and what
     you actually paid against the ~£100 upstream estimate. -->
