# Caduceus for OM-3 v0.26.2 (stored WB per film)

**v0.26.1.1 (v0.26.1 + automatic SD loading) with a stored white balance per film, and nothing else.** A downstream build of
[androidfanman/caduceus-om3](https://github.com/androidfanman/caduceus-om3) v0.26.1. **Emulator only: no camera test of this build.**

- **Take:** on the **WB row** of Picture Mode, with a COLOR that holds a film, press **INFO**: the camera's current WB mode (and, for Custom WB,
  its Kelvin) is stored in the film. Press INFO again while the camera still shows exactly that, and the film lets it go (it follows the
  camera's WB again). Nothing on the screen shows that a WB is stored; to check, choose another film and back.
- **Recall:** choosing that film (when it is not the film already on) writes the stored mode, and for Custom WB the Kelvin, to the camera's WB.
  Not at power-on, not when you pick the same film again, not for COLOR 1–4 themselves. The camera's WB then stays whatever you change it to
  ("last write wins"). The WB shift (A-B / G-M) of the film is separate and unchanged.
- Kept like the other changes: `BUNDLES.BIN` (at the half-press) and `EDITS.BIN` (when you leave the film). `LOOKS.BIN` is never written with it,
  and the Control Panel is unchanged. Format: [docs/FORMATS.md](../../docs/FORMATS.md).

**Going back to v0.26.1.1 or older:** once a film has a stored WB, `BUNDLES.BIN` carries four extra bytes and the older firmware **refuses the
whole file**: your COLOR 1–4 changes in `BUNDLES.BIN` (hue / light / shift / Extras of the live COLOR) start neutral until the next save.
`BUNDLES.BAK` is the previous file and `EDITS.BIN` (per-film changes) is read without a problem. To avoid it, take the stored WB off every film
(choose another film and back so the camera shows that film's WB, then INFO on the WB row) before going back, or delete `BUNDLES.BIN`.

**Copy to the card:** `DCOLYMP` (flash it) and `OM3MOD` `GUIDES.BIN` (made for this firmware: always copy it with it), `LABELS.BIN` and `TONES.BIN`.
Keep your `EDITS.BIN`, `NAMES.BIN`, `BUNDLES.BIN` and `LOOKS.BIN` (this folder's `LOOKS.BIN` is v0.26.1's own and replaces your films).

Make it: `python3 firmware/patch.py --release v0.26.2`. The files here are the patch (only the bytes this build adds; no OM firmware), the card
files and the expected checksums. The pictures were rendered with a different FreeType / DejaVu than upstream's (as v0.26.1.1's).
