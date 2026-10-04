# Changelog

## 0.6.14 - 2026-10-04

- Fix dash identification when Matcha returns numeric GC entries without a common `tbl` owner. The fallback verifies actual hash-table field names, numeric types, live dash count and timers instead of relying on owner metadata.
- Spread fallback lookup across frames, reuse verified addresses and prevent duplicate cached matches.
- Report unsupported memory access or node formats in Dash's Write status.
- Remove all comments from the distributed script. Saved settings and unrelated controls keep their existing behavior.
- Regression checks pass for three simulated PC layouts with 120 repeated dashes, relocation recovery, the captured movement controller and the GitHub JDUI/config suite. Other-PC live verification is still required.

## 0.6.13 - 2026-10-04

- Initial GitHub release of Huss Valley for Matcha.
- Movement speed tuning, dash controls and independent cooldown caps.
- Dash recovery checks cached timer blocks and verified nearby nodes before a full scan, with work spread across render frames.
- Brief publication and identity read races retry without discarding a valid binding.
- JDUI loads directly from GitHub; toggles, sliders, theme and menu key persist across reloads.
