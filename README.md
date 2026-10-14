# 3D-Clinostat — a desktop microgravity simulator

A 3D-printed, two-axis clinostat (random positioning machine) that simulates microgravity for small
biological samples by continuously rotating them so that the gravity vector averages toward zero over
time. Built from off-the-shelf parts and a 3D printer — no machining required.

<!-- TODO: replace with a real photo of your build. A hero image sells this repo more than any paragraph. -->
<p align="center">
  <img src="images/hero.jpg" alt="Assembled clinostat" width="600">
</p>

---

## Why a clinostat

Gravity is one of the few environmental variables you can't switch off in a normal lab. A clinostat
gets around this: by rotating a sample slowly about one or two axes, the *direction* of gravity
relative to the sample changes continuously, so the time-averaged gravity vector approaches zero. For
organisms whose gravity-sensing response is slower than the rotation period — plant roots, cell
cultures, small aquatic organisms — this is functionally similar to microgravity.

A two-axis clinostat rotating at incommensurate speeds (e.g. 3 and 4 RPM) avoids the sample tracing a
repeating path, which gives better averaging than a single axis.

## Specs

This is a stock OpenClino build, so these are the upstream design's figures.

| | |
|---|---|
| Axes | 2 (nested inner/outer frame) |
| Modes | Continuous clinorotation, or random positioning (RPM) via SD path following |
| Rotation range | Typically 2–4 RPM per axis; firmware caps moves at 10 RPM by default |
| Effective resolution | 3200 microsteps/rev × 3.125:1 (X) — see [`firmware/README.md`](firmware/README.md) |
| Controller | Arduino (any board — uses digital pins 2–8 plus hardware SPI) |
| Motors | 2× NEMA 17, 0.42 Nm, driven by A4988 or TMC2208 at 16× microstepping |
| Frame | 3D printed (PLA/PETG) + 20×20 mm aluminium extrusion + 12 skateboard bearings |
| Sample chamber | Not specified by the design — left to the builder |
| Payload capacity | Not characterised upstream |
| Power | Sized to your motors and drivers; not specified upstream |
| Build cost | ~£100 (upstream estimate) |
| Continuous runtime tested | 100+ hours upstream. Not yet run on this build |

## Repository layout

```
3d_files/         .3mf print files for all 10 printed parts
firmware/
  openclino/        Main Arduino sketch, plus partial-gravity path generators
  clinostat-ui/     Optional LVGL touchscreen UI
hardware/         Pinout and notes on the electronics
docs/             Bill of materials, assembly notes, build log
images/           Photos and video of the build and of it running
UPSTREAM.md       Exactly what was copied from upstream, and from which commit
LICENSE.upstream  Upstream OpenClino MIT notice
```

The contents of `firmware/` and `3d_files/` are copied unmodified from upstream — see
[`UPSTREAM.md`](UPSTREAM.md).

## Bill of materials

See [`docs/BOM.md`](docs/BOM.md).

## Printing the parts

Upstream's print settings, used unmodified (an Ender 3 in upstream's case):

| Setting | Value |
|---|---|
| Material | PLA works; PETG preferred |
| Infill | 20% |
| Supports | `m2y` only |
| Brim | Preferred |

Expect to sand edges depending on stringing and over-extrusion. Full part list with quantities is in
[`3d_files/README.md`](3d_files/README.md).

Files live in [`3d_files/`](3d_files/), copied unmodified from upstream — nothing was rescaled,
reinforced, or redesigned. Upstream suggests PLA works but prefers PETG.

## Assembly

Step-by-step notes are in [`docs/ASSEMBLY.md`](docs/ASSEMBLY.md). Wiring and pinout are in
[`hardware/`](hardware/).

## Firmware and running it

Open [`firmware/openclino/openclino.ino`](firmware/openclino/openclino.ino) in the Arduino IDE and
upload, or use `arduino-cli`:

```
arduino-cli compile --fqbn <your-fqbn> firmware/openclino
arduino-cli upload  --fqbn <your-fqbn> -p <your-port> firmware/openclino
```

The motors stay disabled until the button on pin 2 reads HIGH. Which routine that button runs is
chosen by uncommenting one call in `loop()` — `follow_path()` is active as shipped, so uncomment
`spin_continuous(...)` instead for plain clinorotation:

```cpp
spin_continuous(3, 4);   // X (outer) axis 3 RPM, Y (inner) axis 4 RPM
```

See [`firmware/README.md`](firmware/README.md) for the full command set.

## Known issues / next steps

Nothing found on this build yet — it hasn't been run. Known constraints inherited from the design:

- **Y calibration is per-build.** `yCorrection` depends on friction in your specific machine, so the
  shipped `1.5` will not be right until you re-run `calibrate_y_correction()`. See
  [`docs/ASSEMBLY.md`](docs/ASSEMBLY.md).
- **No defined sample chamber.** The design stops at the rotating frame; sample mounting is left to
  the builder.
- **Belt clearance is tight.** The short Y belt and the long `m2y` belt nearly touch — upstream calls
  this the tightest tolerance in the build.
- **Partial gravity needs a computer in the loop.** The Arduino can't compute the path at runtime, so
  paths are generated in Python and read from an SD card.

## License

MIT 
