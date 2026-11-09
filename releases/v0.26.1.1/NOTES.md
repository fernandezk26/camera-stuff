# Caduceus for OM-3 v0.26.1.1 (SD loader)

**v0.26.1 with automatic SD loading, and nothing else.** A downstream build of
[androidfanman/caduceus-om3](https://github.com/androidfanman/caduceus-om3) v0.26.1: the same worker as
[v0.25.1](../v0.25.1/NOTES.md), ported onto v0.26.1. Split toning, the WB shift ±7, the drive-mode restart fix and everything else
are v0.26.1's.

- **Automatic SD loading (not camera-qualified):** your card files (`BUNDLES.BIN`, `GUIDES.BIN`, `LABELS.BIN`, `TONES.BIN`,
  `LOOKS.BIN`, `NAMES.BIN`) load a moment after the card is ready, without a half-press first. A small worker task wakes the HLS
  task, which runs the same loader gate the half-press hook uses. The half-press and OK triggers still work.
  See [docs/SD_LOADER.md](../../docs/SD_LOADER.md).
- `NAMES.BIN` keeps working (its loader moved to a larger flash section to make room).

**Status.** Emulator only. The card block (guides, `LOOKS.BIN`, `TONES.BIN`) is published within 500 ms with no key press, and not
at all on an unmodified v0.26.1 built the same way; upstream's drive-mode recipe completes; the split-toning pages (INFO walk) behave
as on the unmodified build. **No camera test of this build yet** (v0.25.1, the same worker on v0.25, was camera-flashed by its
owner and liked; that is not a test of this build). Hardware-only questions are in
[docs/SD_LOADER.md](../../docs/SD_LOADER.md): AF / capture starvation, cache visibility, real section order, no-card poll cost,
card removal after the load, power cycle.

**Copy to the card:** `DCOLYMP` (flash it) and the `OM3MOD` files `GUIDES.BIN` (made for this firmware: always copy it with it),
`LABELS.BIN` and **`TONES.BIN`** (v0.26 needs it). Keep your `EDITS.BIN`, `NAMES.BIN` and `BUNDLES.BIN`. `LOOKS.BIN` is v0.26.1's own
(the tuned 20 film sims), unchanged; it **replaces your films**.

Make it: `python3 firmware/patch.py --release v0.26.1.1`. The files here are the patch (only the bytes this build adds; no OM firmware),
the card files and the expected checksums.

The pictures in `GUIDES.BIN` / `LABELS.BIN` / `TONES.BIN` and the film-digit cells were rendered by a different FreeType / DejaVu
than upstream's, so they can differ from v0.26.1's by a pixel or so; the code is v0.26.1's plus the loader.
