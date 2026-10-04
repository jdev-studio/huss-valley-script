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

The script identifies the private dash timers and reuses verified addresses. Missing or inconsistent GC owner metadata now falls back to live hash-table lookup, checking all four numeric fields and the private dash count before binding. Addresses are discovered on each PC. When they change, it checks cached blocks and a bounded nearby region before falling back to a full scan. Field identities and write readback are checked. Full scans can still cause a pause, and game or server changes can limit client tuning.

If Dash reports a memory access/version error, confirm unsafe Lua execution is enabled in Matcha. The fallback requires `memory_read` and `memory_write` and a verifiable Luau node format. Check the console for `Loaded Huss Valley v0.6.14` to confirm the updated loader result.

## Controls

| Key | Action |
| --- | --- |
| Right Shift | Show / hide menu |

The menu key can be changed in Settings. Close the menu with X and confirm to stop the script.

## Saved settings

Toggles, sliders, theme and menu key are saved to `huss_valley_config.json` in Matcha's workspace and restored on the next run. Enabled features also restore. Memory addresses are identified again each run and are never saved.

## Version

Current version: **0.6.14**. See [CHANGELOG.md](CHANGELOG.md).
