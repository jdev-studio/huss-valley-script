# Changelog

## 0.6.21 - 2026-10-06

- Speed tuning no longer switches itself off when the game corrects your position. Corrections are ignored and the speed stays where you set it.
- Travel speed is capped at 45 studs/s (was 80). Saved values above 45 load as 45.
- Speed ramps up over about a quarter second instead of jumping to full speed in one frame.
- A few unreadable or rejected velocity frames no longer turn speed off; it only stops if they keep failing for about a second. One bad frame no longer stops the whole script.
- Infinite dash is now one toggle, **Infinite dash (no cooldown)**, replacing Tune Dash, Dash max cooldown and Re-arm dash on Space release. Turn it on once after updating; the old dash settings don't carry over.
- Speed and dash are on the same Movement tab. The Dash tab is gone.

## 0.6.20 - 2026-10-05

- Stop speed tuning before its next velocity write when the game's MovementReset counter increases. Previously the script only logged the correction and kept forcing the same speed, allowing repeated corrections.
- Clear pending velocity confirmation and notify the user to lower Travel speed before enabling again. Preserve the speed slider, dash controls and saved settings.
- Regression reproduces the previous post-correction writes and verifies that they stop, the slider remains unchanged and manual re-enabling still works. This cannot prevent the game's initial correction or establish the cause of an unobserved position jump.

## 0.6.19 - 2026-10-05

- Fix the startup nil `RunService` / `RenderStepped` error. Retry scheduler discovery for up to 100 yielded attempts, accepting an available global service and Heartbeat when RenderStepped is absent.
- Share the selected frame signal with GitHub JDUI and the gameplay loop so the fallback supports the full menu and dash functionality.
- If Matcha exposes no usable frame scheduler, exit before loading JDUI with an attach-and-rerun message instead of a nil-index error. No settings or controls are removed.
- Reproduce the original nil-service failure and verify late-service recovery, missing-service exit, Heartbeat gameplay/config regression, delayed-player startup and dash table tracking in simulation. Affected-PC behavior remains unverified.

## 0.6.18 - 2026-10-05

- Wait for a ready Roblox player, mouse and camera before loading JDUI. Re-running while waiting replaces the pending startup callback instead of creating duplicate menus.
- Retry an unsuccessful GitHub download once; reject empty/HTML responses before executing library code. JDUI still downloads exclusively from the tested GitHub revision.
- Support missing `task.spawn` and font tables through local JDUI compatibility adapters. Text keeps its native default font when optional font constants are unavailable.
- Validate downloaded avatar PNG signatures, chunk boundaries, dimensions and size before forwarding data to Matcha's native Drawing image decoder. Invalid responses use JDUI's existing initial badge; valid avatars remain supported.
- Regression cases reproduce the previous delayed-player, missing scheduler/fonts, empty download and invalid-image forwarding failures. Those cases now pass, along with valid avatars, network exceptions, HTML download retries, dash tracking and saved settings.
- This hardens known startup and native-input failure paths. Without an affected PC or crash report, the exact reported Matcha process crash remains unconfirmed.

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
