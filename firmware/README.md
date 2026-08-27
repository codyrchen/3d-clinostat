# Firmware

Code that drives the two rotation axes.

> The upstream [OpenClino](https://github.com/wahabk/Clinostat) firmware lives in its `src/`
> directory. Drop your version here — either a copy with your modifications, or a thin wrapper —
> and note below exactly what you changed.

## Flashing

<!-- TODO -->
```
TODO: e.g. arduino-cli compile --fqbn arduino:avr:uno . && arduino-cli upload -p /dev/ttyACM0 ...
```

## Commands

<!-- TODO: document the actual API you're using. -->

| Call | Effect |
|---|---|
| `spin_continuous(outer_rpm, inner_rpm)` | Rotate both axes continuously at the given speeds. Use incommensurate values (3 and 4) so the sample path doesn't repeat. |
| *TODO* | |

## Configuration

*TODO — steps/revolution, microstepping, gear ratio, driver current limit.*

## Changes from upstream

*TODO — list them, however small. If it's unmodified, say "unmodified from upstream vX.Y.Z".*
