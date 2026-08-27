# Firmware

Arduino code that drives the two rotation axes. Copied **unmodified** from
[OpenClino](https://github.com/wahabk/Clinostat)'s `src/` — see [`../UPSTREAM.md`](../UPSTREAM.md)
for the exact upstream commit.

```
openclino/         Main sketch — the clinostat controller
  openclino.ino      setup()/loop()
  openclino.h        Pin, gear-ratio, and function declarations
  openclino.cpp      Motor control implementation
  partial_gravity/   Python generators for partial-gravity path files
  test_path/         Standalone path-following test sketch
  test_sd/           Standalone SD card test sketch
clinostat-ui/      Optional LVGL touchscreen UI (separate sketch)
```

`X` is the outer frame, `Y` is the inner frame — that convention runs through the whole codebase.

## Dependencies

The main sketch includes `SPI.h` and `SD.h` (both bundled with the Arduino IDE). The SD card is only
needed for `follow_path()`; continuous clinorotation runs without it.

## Flashing

Open `openclino/openclino.ino` in the Arduino IDE and upload to your board, or with `arduino-cli`:

```
arduino-cli compile --fqbn <your-fqbn> firmware/openclino
arduino-cli upload  --fqbn <your-fqbn> -p <your-port> firmware/openclino
```

Upstream leaves the board choice open — the sketch only needs digital pins 2–8 plus hardware
SPI, so most Arduinos work.

<!-- Fill in once flashed: the exact --fqbn and port used, so this is copy-pasteable. -->

## Commands

| Call | Effect |
|---|---|
| `enable(bool enableX, bool enableY)` | Enable/disable each motor. |
| `spin_continuous(speedX = 10, speedY = 10, buttonDelay = 1000)` | Rotate both axes continuously at the given RPM until the button is pressed. Use incommensurate speeds (e.g. 3 and 4) so the sample path doesn't repeat. |
| `spin_degs(Q1_target, Q2_target, maxRPM = 10)` | Rotate each axis by a number of degrees, capped at `maxRPM`. |
| `follow_path()` | Read `path.txt` from the SD card and run `spin_degs()` for each line. Errors if the card or file can't be read. |
| `calibrate_y_correction()` | Rotate Y and measure actual rotation to derive `yCorrection`. |
| `test_pulley_ratios()` | Rotate both axes 360° and back. |
| `test_spin_degs_multi()` | Exercise `spin_degs()` over multiple rotations. |

`loop()` keeps the motors disabled until the button on `buttonPin` reads HIGH. Which routine runs on
that press is selected by uncommenting one call inside `loop()` — as shipped, `follow_path()` is the
active one, so **uncomment `spin_continuous(...)` instead if you want plain clinorotation.**

## Configuration

Set in `openclino.cpp`:

| Constant | Value | Meaning |
|---|---:|---|
| `motorSteps` | 200 | Full steps per motor revolution (1.8°/step) |
| `subStep` | 16 | Driver microstepping |
| `stepsPerRevolution` | 3200 | `motorSteps × subStep` |
| `xMotTeeth` / `xPulleyTeeth` | 16 / 50 | X drive pulley teeth |
| `yMotTeeth` / `yTurnTeeth` / `yPulleyTeeth` | 16 / 50 / 20 | Y drive pulley teeth |
| `yCorrection` | 1.5 | Empirical Y correction from `calibrate_y_correction()` |
| `PATH_FILENAME` | `path.txt` | Path file read from the SD card |

`yCorrection` is a calibration result, not a constant of the design — re-run
`calibrate_y_correction()` on your own build and update it if Y doesn't track.

## Partial gravity

`partial_gravity/` generates the `path.txt` consumed by `follow_path()`. Upstream implements time
averaged Simulated Partial Gravity (taSPG) following Kim et al. 2026, *Scientific Reports*
(https://doi.org/10.1038/s41598-026-40665-6).

```
pip install numpy matplotlib
python3 firmware/openclino/partial_gravity/generate_taspg_path.py
```

There is no command-line interface — the target gravity is set by editing `target_g` in the script's
`__main__` block (shipped as `0.38` for Mars; the Moon is `0.17`). The script prints the achieved
taSPG, opens a plot of the path, and writes the space-separated `dtheta dphi` step file.

A pre-generated 1000-step `partial_gravity/path.txt` is included. Copy it to the root of a
FAT-formatted SD card as `path.txt` to use it.

> `wc` and `wmin` in the generator are hardware constants — upstream notes you should measure `wmin`
> on your own motors rather than trusting the defaults.

## Changes from upstream

None — unmodified.
