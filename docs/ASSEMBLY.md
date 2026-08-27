# Assembly

This build is stock, so the canonical instructions are the
[upstream build guide](https://github.com/wahabk/Clinostat/blob/main/docs/3_build_guide.md), which has
a photo at every step. This page is a condensed walkthrough plus space for notes on *this* build.

Upstream puts the build at **1–2 hours**. Tools and parts are listed in [`BOM.md`](BOM.md).

**Naming:** X is the outer body, Y is the inner body. Motor pulleys attach to the motors; X/Y pulleys
attach to the bodies. `m2y` is the pulley with two belts on it. `y_turn` is the bearing assembly that
bends the long Y belt. `y_guide` is the L-shaped bracket holding the Y pulley.

> The guiding principle throughout: **nothing should be tight.** Over-tightening introduces friction
> that the motors have to fight, and can crack the printed mounts. Everything should spin freely by
> hand before you power it.

## 1. Print the parts

See [`../3d_files/README.md`](../3d_files/README.md) — 20% infill, supports on `m2y` only, brim
preferred. Sand the edges where stringing or over-extrusion interferes with a fit.

## 2. Build the y_turn

Place washers between the bolt head/nut and the bearing. Don't tighten the nuts — that adds
unwanted friction.

## 3. Combine the X and Y bodies

1. Push-fit bearings into the `y_guide` and the `x_body`.
2. Run bolts through the X and Y bodies, with a **washer on each side of every bearing**.
3. Install the Y pulley and `y_guide` with washers between them. **Add the Y belt before the nut** —
   it can't go on afterwards. Hex nuts push-fit into the X body. Tighten the Y pulley grub screws so
   it rotates with the Y body.
4. Install the `y_turn` into the X body; its hex nuts also push-fit.
5. Check everything rotates smoothly. Nylock nuts only need to be tight enough to stop shake.

## 4. x_pulley and m2y pulley

1. **x_pulley:** push-fit into the body and add washers. You may need to sand the pins.
2. **m2y pulley:** push-fit two bearings and add washers.

> The long belt must not scrape the motor. Keep the wider part of the `m2y` close to the X body and
> put 2–3 washers between the X body and the `m2y` pulley.

## 5. Build the base

1. Install the motor pulleys, aligning the notch in the motor shaft with one of the grub screws.
   **Leave the motors loose** — you tension the belts later. Both sides.
2. Bolt each motor to its motor mount with 4 hex screws. Both sides.
3. Push-fit bearings into the motor mounts and motor enclosures.
4. Attach the enclosures and motor mounts to the aluminium rails. Keep every screw loose — aligning
   this takes a lot of wiggling.

## 6. Final assembly

You now have two assemblies: the base, and the X+Y bodies.

1. Add the short belts to the `x_pulley` and `m2y` pulley.
2. Mount the X body assembly to the base, with a washer between the pulleys and the motor mount
   bearings.
3. Tighten the long bolts — but not hard, or you'll break the mounts and enclosures.
4. Hook the short belts onto the motor pulleys: lift the motors to get the belt on, tension it, then
   tighten the motor screws.
5. **Check the short Y belt and the long m2y belt don't interfere.** This is the tightest tolerance
   in the machine.
6. Only once both axes rotate smoothly, tighten the base.

If there's friction anywhere, loosen bolts or sand back the interference before powering up.

## 7. Electronics

Wire per [`../hardware/README.md`](../hardware/README.md) — button on pin 2, X on 3/4/5, Y on 6/7/8,
SD chip select on 10. Set the drivers to **16× microstepping** to match `subStep = 16` in the
firmware, and set the driver current limit (Vref) for your specific motors.

## 8. Calibrate before first real run

The Y axis needs calibrating because the outer body's effect on the inner one depends on friction,
which varies between builds. From [upstream's procedure](https://github.com/wahabk/Clinostat/blob/main/docs/1_documentation.md):

1. Flash `firmware/openclino/openclino.ino` with `calibrate_y_correction()` uncommented in `loop()`.
2. Open the Serial Monitor.
3. Centre the frames so they overlap.
4. Press the button — the Y motor rotates 360°.
5. Measure how far Y *actually* rotated and enter that in the Serial Monitor.
6. Update `yCorrection` in `firmware/openclino/openclino.cpp` with the value it prints.

Expect to repeat this a couple of times to converge. The shipped value is `1.5`, which is upstream's
build, not yours.

## 9. First power-on

Before leaving it unattended: confirm both axes turn freely by hand, that no belt scrapes, that the
drivers aren't overheating, and that the calibration holds over a few minutes of rotation.

## Gotchas

Upstream's, worth knowing before you hit them:

- The Y belt has to go on **before** the nut in step 3.
- Y belt vs. m2y belt clearance is the tightest tolerance in the build.
- Over-tightening cracks the printed mounts and enclosures.
- The `m2y` pulley needs supports when printing; nothing else does.
- Calibration usually needs more than one pass.

<!-- Fill in as you build: the things that actually cost you an evening on this build. This ends up
     being the most useful section for anyone rebuilding it. -->
