# Upstream provenance

The firmware in [`firmware/`](firmware/) and the print files in [`3d_files/`](3d_files/) are copied
**verbatim and unmodified** from the OpenClino project. This file records exactly what was taken and
from where, so the copy can be diffed or refreshed later.

| | |
|---|---|
| Project | [OpenClino](https://github.com/wahabk/Clinostat) |
| Author | Abdelwahab Kawafi ([@wahabk](https://github.com/wahabk)) |
| License | MIT — see [`LICENSE.upstream`](LICENSE.upstream) |
| Commit copied | `2a7ea91be041df0864d875af1febfc499bbcbbea` |
| Commit date | 2026-04-11 |
| Citation | Wahab Kawafi. (2026). wahabk/Clinostat. Zenodo. https://doi.org/10.5281/zenodo.18448825 |

## What was copied

| Upstream path | Path here | Notes |
|---|---|---|
| `src/openclino/` | `firmware/openclino/` | Main sketch, headers, partial-gravity generators, test sketches |
| `src/clinostat-ui/` | `firmware/clinostat-ui/` | Optional LVGL touchscreen UI |
| `3d_files/*.3mf` | `3d_files/` | All 10 print files, original filenames preserved |
| `LICENSE` | `LICENSE.upstream` | Upstream MIT notice, retained as required |

Only the directory names changed (`src/` → `firmware/`, to match this repo's layout). No file
contents were altered.

## What was not copied

- `docs/images/` — roughly 34 MB, mostly two large animated GIFs. Linked to rather than duplicated.
- Upstream's markdown docs (`docs/1_documentation.md`, `2_BOM.md`, `3_build_guide.md`,
  `4_code_documentation.md`). The build guide and circuit diagram there remain the canonical
  reference; the docs in this repo cover *this* build.

## Refreshing against upstream

```
git clone https://github.com/wahabk/Clinostat.git /tmp/clinostat
diff -r /tmp/clinostat/src/openclino  firmware/openclino
diff -r /tmp/clinostat/src/clinostat-ui firmware/clinostat-ui
diff -r /tmp/clinostat/3d_files 3d_files
```

Upstream tracks changes in its
[CHANGELOG.md](https://github.com/wahabk/Clinostat/blob/main/CHANGELOG.md).
