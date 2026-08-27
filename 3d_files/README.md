# 3D print files

Print files for every printed part, as `.3mf`, copied unmodified from
[OpenClino](https://github.com/wahabk/Clinostat) — see [`../UPSTREAM.md`](../UPSTREAM.md) for the
exact upstream commit these came from.

Per the upstream build guide, parts can be printed in PLA, but PETG is preferred.

| File | Part | Notes |
|---|---|---|
| `x_body v9.3mf` | Outer (X) frame body | Bearings push-fit; hex nuts push-fit into the body |
| `y_body v4.3mf` | Inner (Y) frame body | |
| `y_guide v2.3mf` | Y guide | Bearings push-fit |
| `y_turn v2.3mf` | Y turn | Sub-assembly built first; washers between bolt head/nut and bearing |
| `y_turn_pulley v2.3mf` | Y turn pulley | |
| `x_pulley v7.3mf` | X axis pulley | May need the pins sanded to push-fit |
| `m2y v5.3mf` | Motor-to-Y pulley | Takes two push-fit bearings; keep the wider part toward the X body |
| `m_base v9.3mf` | Motor base / mount | One per motor. `m_base v7.3mf` is the older revision, kept for reference |
| `m_base v7.3mf` | Motor base / mount (older) | Superseded by v9 |
| `m_enclosure v2.3mf` | Motor enclosure | |

> **Note on the Y pulley:** since upstream version 0.4 the Y pulley is an off-the-shelf 6 mm GT2 30T
> pulley rather than a printed part, so the printed pulley in the older build-guide photos no longer
> applies.

<!-- TODO: record the print settings you actually used — material, layer height, infill, supports,
     and total print time — and note any part you reprinted or rescaled. -->
