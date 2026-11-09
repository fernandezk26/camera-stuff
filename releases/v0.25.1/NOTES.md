# Caduceus for OM-3 v0.25.1 (SD loader)

**v0.25 with automatic SD loading and the drive-mode restart fix.** A downstream build of
[androidfanman/caduceus-om3](https://github.com/androidfanman/caduceus-om3) v0.25; everything else is v0.25.

- **Automatic SD loading (new, not camera-qualified):** your card files (`BUNDLES.BIN`, `GUIDES.BIN`, `LABELS.BIN`, `LOOKS.BIN`,
  `NAMES.BIN`) load a moment after the card is ready, without a half-press first. A small worker task wakes the HLS task, which
  runs the same loader gate the half-press hook uses. The half-press and OK triggers still work. See [docs/SD_LOADER.md](../../docs/SD_LOADER.md).
- **Fix: restart after changing the drive mode** (upstream's fix from v0.26, backported): the WB grid row picked up a screen
  element from the drive-mode screen; it now only uses Picture Mode's.
- **Not included from v0.26:** split toning, `TONES.BIN`, the `*` / Hold-OK changes for split toning.
- `NAMES.BIN` keeps working (its loader moved to a larger flash section to make room).

**Status.** Emulator only (the fix: upstream's recipe faults on v0.25 and completes here; the loader: the card block is published
within 500 ms with no key press, and not at all without the worker). **No camera test of this build yet.** Hardware-only
questions are listed in [docs/SD_LOADER.md](../../docs/SD_LOADER.md): AF / capture starvation, cache visibility, real section
order, no-card poll cost, card removal after the load, power cycle.

**Copy to the card:** `DCOLYMP` (flash it) and the `OM3MOD` files `GUIDES.BIN` (made for this firmware: always copy it with it) and
`LABELS.BIN`. Keep your `EDITS.BIN`, `NAMES.BIN` and `BUNDLES.BIN`. `LOOKS.BIN` (optional) is v0.25's 20 film sims, unchanged; it
**replaces your own films**.

Make it: `python3 firmware/patch.py --release v0.25.1`. The files here are the patch (only the bytes this build adds; no OM
firmware), the card files and the expected checksums.

The pictures in `GUIDES.BIN` / `LABELS.BIN` and the film-digit cells were rendered by a different FreeType / DejaVu than v0.25's, so
they can differ from v0.25's by a pixel or so; the code is v0.25's plus the two changes above.
