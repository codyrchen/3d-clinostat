# Hardware

Wiring, pinout, and electronics notes.

## Pinout

Taken from `firmware/openclino/openclino.cpp`. `X` is the outer frame, `Y` is the inner frame.

| Signal | MCU pin | Goes to |
|---|---:|---|
| Button | 2 | Momentary start button (reads HIGH to run) |
| Enable X | 3 | X stepper driver `EN` |
| Step X | 4 | X stepper driver `STEP` |
| Dir X | 5 | X stepper driver `DIR` |
| Enable Y | 6 | Y stepper driver `EN` |
| Step Y | 7 | Y stepper driver `STEP` |
| Dir Y | 8 | Y stepper driver `DIR` |
| SD chip select | 10 | SD card reader `CS` (only needed for `follow_path()`) |
| Status LED | `LED_BUILTIN` | On-board LED, lit while the motors are enabled |

The SD reader is on hardware SPI, so it also uses the board's MOSI/MISO/SCK pins alongside CS.

Drivers must be set to **16× microstepping** to match `subStep = 16` in the firmware. If you change
the microstepping jumpers, change that constant to match or every rotation will be off by the same
factor.

## Wiring diagram

Upstream publishes circuit diagrams — one plain, one including the microSD reader — in
[OpenClino's `docs/images/`](https://github.com/wahabk/Clinostat/tree/main/docs/images). They aren't
copied here to keep this repo small; the circuit description is in
[upstream `docs/1_documentation.md`](https://github.com/wahabk/Clinostat/blob/main/docs/1_documentation.md).

<!-- TODO: add a photo of your own wiring as wiring.jpg once it's built. -->

## Power

<!-- TODO: record your supply voltage/current, the driver Vref you set, and whether anything ran hot.
     Vref depends on your specific motors and driver boards, so it has to be measured on your build. -->

## Safety

Upstream reports testing the machine for a minimum of 100 hours of continuous operation.

<!-- TODO: note your own findings on unattended running — belt tension drift, motor/driver
     temperature, and whether you fused or timer-limited the supply. -->
