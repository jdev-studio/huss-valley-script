# Changelog

## 0.6.17 - 2026-10-05

- Remove Dagger, Ability, Gear, Ghost, Clone and Tackle cooldown controls and all associated attribute-writing code.
- Remove catcher alerts, distance/status controls and recurring catcher enumeration. Remove the now-empty Cooldowns tab and its Stop all button.
- Retain Movement, Dash and Settings with the same saved movement/dash values, theme and menu key. Old saved keys for removed features are ignored.
- Movement, dash/reload/config regressions and 120 next-frame relocation checks pass. This feature removal does not establish a fix for the separately reported Matcha process crash.

## 0.6.16 - 2026-10-05

- Retry temporary GC exceptions and invalid scan results without permanently disabling dash tuning or changing saved toggles. Both timer-only and release re-arm modes recover automatically; failed scans never write memory.
- Bound node-array verification during header discovery, header selection and storage relocation. Slow lookups resume from partial work, and a changed storage pointer discards that work before rebinding.
- Back off unchanged ambiguous headers instead of inspecting their full arrays every frame. A new dash count bypasses the backoff immediately. Deduplicate history seeds and ignore malformed GC entries while retaining valid controller data.
- Batch log file writes at 250 ms intervals while retaining console messages and flushing the final log on stop/reload.
- Download the tested GitHub JDUI 1.0.7 commit on every run, preserving Huss Valley branding with the updated sidebar. No local JDUI dependency and no gameplay controls removed.
- Regression proof: 120 distant relocations still recover on their first render step. A simulated slow-read 256-node refresh completes over four callbacks, each at most 6.080 ms. Partial pointer replacement, ambiguous headers, scan failures, the captured controller, portability, movement, cooldowns, alerts and saved configs all pass.
- The affected users' exact stop errors were unavailable, so live confirmation of those reports remains pending.

## 0.6.15 - 2026-10-04

- Track the verified MovementModel table header through its movement-history link. Moving timer storage now follows the header's current pointer before the old address-fault delay or a full scan.
- Learn shuffled header layouts at runtime and inspect only the active table's small node array. This avoids relying on undocumented owner IDs or readable string hashes for this path.
- Verify all five field identities, private dash count, history link and storage pointer before writes. Publication races retry, and ambiguous or invalid headers retain the fallback.
- Log direct lookup time when timer storage changes.
- The old release fails the new tracking regression. The new build recovers 120 distant relocations on the next render step across three simulated header layouts, with no additional GC scans. The captured controller, relocation, portability and GitHub JDUI/config suites also pass.
- Live verification: the same table/header and history link survived a node-storage move; lookup at dash 210 took 0.259 ms. The retained log records consecutive successful re-arms from dashes 182–211 with no fallback scan, and the user reported the pauses stopped.

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
