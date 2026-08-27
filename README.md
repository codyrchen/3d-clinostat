# 3D-Clinostat — a desktop microgravity simulator

A 3D-printed, two-axis clinostat (random positioning machine) that simulates microgravity for small
biological samples by continuously rotating them so that the gravity vector averages toward zero over
time. Built from off-the-shelf parts and a 3D printer — no machining required.

> **Credit where it's due.** This build is based on the open-source
> [**OpenClino**](https://github.com/wahabk/Clinostat) project by [wahabk](https://github.com/wahabk),
> which is itself derived from European Space Agency clinostat research. The mechanical design and
> firmware originate there and are used under the MIT license. This repository documents *my build* —
> the parts I sourced, the problems I hit, the changes I made, and how it performed.
> If you want the canonical design files, go to the upstream project first.

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

<!-- TODO: fill these in from your actual build. Delete rows that don't apply. -->

| | |
|---|---|
| Axes | 2 (nested inner/outer frame) |
| Rotation range | *TODO — e.g. 0.5–10 RPM per axis* |
| Sample chamber | *TODO — e.g. 50 mL falcon tube / 35 mm petri dish* |
| Payload capacity | *TODO* |
| Controller | *TODO — e.g. Arduino Uno + CNC shield* |
| Motors | *TODO — e.g. 2× NEMA 17 steppers* |
| Power | *TODO — e.g. 12 V 2 A* |
| Frame | 3D printed (PLA/PETG) + skateboard bearings |
| Continuous runtime tested | *TODO — how long did you actually run it?* |
| Build cost | *TODO* |

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

<!-- TODO -->
Print settings used:

| Setting | Value |
|---|---|
| Material | *TODO* |
| Layer height | *TODO* |
| Infill | *TODO* |
| Supports | *TODO* |
| Total print time | *TODO* |

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

## Results

<!-- TODO: this is the section that makes the repo worth showing off. -->
*What did you actually run on it? Include: how long it ran unattended, RPM stability, anything that
failed, and — if you ran a biological sample — what you observed versus a static control. Photos and
plots go a long way here.*

## What I changed from the upstream design

Nothing — this is a stock build. The firmware and print files here are byte-for-byte copies of
upstream at the commit recorded in [`UPSTREAM.md`](UPSTREAM.md), and no part was substituted or
redesigned.

## Known issues / next steps

<!-- TODO -->

## Attribution

- **Upstream design:** [OpenClino](https://github.com/wahabk/Clinostat) by wahabk — MIT licensed.
  Cite the Zenodo release for research use: https://doi.org/10.5281/zenodo.18448825
- The upstream project derives from published ESA clinostat research; see its README and CHANGELOG
  for the primary references, including the time-averaged simulated partial gravity work.

## License

MIT — see [LICENSE](LICENSE). The upstream OpenClino copyright is retained alongside mine, since this
build derives from that project.
