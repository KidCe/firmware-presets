# Kitsi preset rules

These rules apply to personal presets in `presets/kitsi/`. Treat the other preset directories as the Betaflight catalog and leave them unchanged unless the task explicitly targets them.

## Layout and metadata

- Keep every personal preset directly in `presets/kitsi/`; use one `.txt` file per independently useful preset.
- Name files `Kitsi_<Purpose>.txt`. Start each Configurator title with `Kitsi` so the presets group together in search results.
- Let `#$ CATEGORY` control Configurator grouping. Use the most specific category from `indexer/Settings.js`; do not use directory names as category metadata.
- Keep metadata in this order: `TITLE`, one `FIRMWARE_VERSION` line per supported release family, `CATEGORY`, `STATUS`, `KEYWORDS`, `AUTHOR`, `DESCRIPTION`, optional `WARNING`, then optional `INCLUDE` and `DISCUSSION`.
- Use `COMMUNITY` for personal presets. Credit an upstream author in `AUTHOR` and say what Kitsi adapted in the description when applicable.
- Keep descriptions concise and state what the preset changes. Put receiver mapping, video system, UART, LED count, and other hardware constraints in `WARNING`.

## Firmware and behavior

- Add multiple `FIRMWARE_VERSION` lines for release families whose CLI setting names and values are known to work. If the maintainer explicitly requests wider Configurator visibility before compatibility is established, mark that compatibility as unverified in the preset description or warning. Metadata makes a preset visible; it does not prove compatibility.
- Include `feature TELEMETRY` in every Kitsi preset. It enables Betaflight's telemetry feature, but it does not select a receiver protocol, configure a UART, or guarantee that the attached receiver supports telemetry. Explain any remaining setup in the description or warning.
- Use an `(EXCLUSIVE)` option group whenever the user must choose exactly one UART, protocol, LED count, or other conflicting hardware option. Give each option a distinct, accurate label.
- A preset included by another preset does not expose the included preset's option checkboxes. Keep option-bearing presets separate, or repeat their choices in the parent preset.
- Keep presets focused. Leave board identity, calibration, PID, filters, motor setup, and VTX tables out unless the title and warning clearly identify the matching craft or hardware.
- Do not add `save` commands. Betaflight Configurator applies the snippet and the user chooses when to save.
- Avoid `defaults` and broad reset commands unless the preset explicitly promises a reset and explains its scope.

## Index workflow

- Run `npm run verify` after editing presets. This checks preset metadata, includes, and indexer rules; it does not test commands against firmware or a flight controller.
- Run `npm run index` after every preset addition, removal, rename, or metadata/content change.
- Commit the changed preset files together with the generated `index.json` and `index_hash.txt` so the Configurator can discover the same content that is in Git.
- Review the generated index entries and confirm that every Kitsi preset has its intended title, category, author, and firmware-version list.
