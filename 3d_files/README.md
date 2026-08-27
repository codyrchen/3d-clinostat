# 3D print files

Print files for every printed part, as `.3mf`, copied unmodified from
[OpenClino](https://github.com/wahabk/Clinostat) — see [`../UPSTREAM.md`](../UPSTREAM.md) for the
exact upstream commit these came from.

## Parts

Quantities are from the upstream bill of materials.

| File | Part | Qty | Notes |
|---|---|---:|---|
| `x_body v9.3mf` | Outer (X) frame body | 1 | Bearings and hex nuts push-fit into the body |
| `x_pulley v7.3mf` | X axis pulley | 1 | May need the pins sanded to push-fit |
| `y_body v4.3mf` | Inner (Y) frame body | 1 | |
| `y_guide v2.3mf` | Y guide — L-shaped bracket holding the Y pulley | 1 | Bearings push-fit |
| `y_turn v2.3mf` | Y turn — bearings that bend the long Y belt | 1 | Washers between bolt head/nut and bearing |
| `y_turn_pulley v2.3mf` | Y turn pulley | 2 | |
| `m2y v5.3mf` | Motor-to-Y pulley — the one with 2 belts attached | 1 | **Needs supports.** Takes two push-fit bearings; keep the wider part toward the X body |
| `m_base v9.3mf` | Motor mount | 2 | One per motor. `m_base v7.3mf` is the superseded revision, kept for reference |
| `m_enclosure v2.3mf` | Motor enclosure | 2 | Bearings push-fit |

`m_base v7.3mf` is an older revision and is not part of the build — print `v9`.

## Print settings

Upstream's settings, on an Ender 3:

| Setting | Value |
|---|---|
| Material | PLA works; PETG preferred |
| Infill | 20% |
| Supports | `m2y` only |
| Brim | Preferred |

Expect to sand edges depending on how your printer strings and over/under-extrudes. If bolt heads
spin in their pockets instead of keying into the bodies, upstream suggests silicone tape on the bolt
head.

> **Note on the Y pulley:** since upstream version 0.4 the Y pulley is an off-the-shelf 6 mm GT2 30T
> pulley rather than a printed part, so the printed pulley in the older build-guide photos no longer
> applies.

<!-- Fill in once printed: the material and layer height you actually used, total print time, and
     any part you had to reprint. -->
