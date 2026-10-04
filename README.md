# huss-valley-script

Huss Valley movement and dash controls for Matcha. The menu is [JDUI](https://github.com/jdev-studio/jdui), downloaded directly from GitHub on every run.

## Running it

```lua
loadstring(game:HttpGet("https://raw.githubusercontent.com/jdev-studio/huss-valley-script/refs/heads/main/Valley"))()
```

Written against Matcha, with its Drawing API, keyboard/focus functions and memory/GC APIs. Settings require `readfile` and `writefile`. Dash tuning requires Matcha's unsafe Lua execution option to enable the memory APIs.

## What's in it

- **Movement**: speed tuning and adjustable travel speed.
- **Dash**: adjustable maximum cooldown and re-arm on Space release.
- **Cooldowns**: independent Dagger, Ability, Gear, Ghost, Clone and Tackle caps, plus catcher alerts.
- **Settings**: theme, menu key and saved configuration.

## Dash

Set **Dash max cooldown** to `0`, enable **Tune Dash**, and enable **Re-arm dash on Space release**. Release Space after each dash, then change direction and press it again. The game's turn and grounding requirements still apply. Holding Space preserves the current dash motion.

The script identifies the private dash timers and learns the MovementModel table header through its movement-history link. The header layout is verified on each PC. Once tracking is enabled, it checks the table's current storage pointer each frame. A change reads only that table's small node array, verifies all field names and the live dash count, then resumes tuning without a full GC scan or the old stale-address waiting period.

Look for `Dash table tracking enabled` in the console. Relocation recovery logs `Followed dash table` with its lookup time. Initial identification still uses GC. Unsupported or ambiguous headers, lost controller objects and character replacement retain the cached/nearby/full-scan fallback, so those cases can still cause a pause.

If Dash reports a memory access/version error, confirm unsafe Lua execution is enabled in Matcha. Tracking requires `memory_read` and `memory_write` and verifiable table/node metadata. Check the console for `Loaded Huss Valley v0.6.15` to confirm the updated loader result.

## Controls

| Key | Action |
| --- | --- |
| Right Shift | Show / hide menu |

The menu key can be changed in Settings. Close the menu with X and confirm to stop the script.

## Saved settings

Toggles, sliders, theme and menu key are saved to `huss_valley_config.json` in Matcha's workspace and restored on the next run. Enabled features also restore. Memory addresses are identified again each run and are never saved.

## Version

Current version: **0.6.15**. See [CHANGELOG.md](CHANGELOG.md).
