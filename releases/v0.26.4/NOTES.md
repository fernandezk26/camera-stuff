# Caduceus for OM-3 v0.26.4 (the camera's own WB screen on the WB row)

**v0.26.3 (the 0xFF fix + automatic WB save into the film) with one change, and nothing else.** A downstream build of
[androidfanman/caduceus-om3](https://github.com/androidfanman/caduceus-om3) v0.26.1. **Emulator only: no camera test of this build.**

- **The WB row of Picture Mode (COLOR 1–4) opens the camera's full white balance screen** (WB mode, Custom WB with its Kelvin, Keep Warm, and the
  WB± cell) when you press **OK**, left / right or turn a dial on it, instead of the WB shift (fine-tune) screen. A WB mode or Kelvin you set there is saved
  into the film the COLOR holds by v0.26.3's automatic save (kept in the camera's memory at once, written to the card at the next half-press).
- **The film's own WB shift (A-B / G-M, −7..+7) is kept, one step deeper.** The WB± cell in the camera's WB screen shows the film's shift, and its icon opens the
  same fine-tune screen as before, changing the film's shift. Nothing changes in `LOOKS.BIN`, `BUNDLES.BIN` or `EDITS.BIN`.
- **Leaving:** **MENU** in the WB screen comes back to the WB row; **MENU** in the fine-tune screen goes back to the WB screen; **OK** or a half-press leaves to
  live view, as the camera's own screen does when it is opened from the Super Control Panel.

**Going back to v0.26.3 or v0.26.2:** the files are the same format, nothing to clean. **Going back to v0.26.1.1 or older:** see v0.26.3's notes (a film that holds a stored WB
makes `BUNDLES.BIN` carry four extra bytes the older firmware refuses: delete `OM3MOD/BUNDLES.BIN` when you go back).

**Copy to the card:** `DCOLYMP` (flash it) and `OM3MOD` `GUIDES.BIN` (made for this firmware: always copy it with it), `LABELS.BIN` and `TONES.BIN`.
Keep your `EDITS.BIN`, `NAMES.BIN`, `BUNDLES.BIN` and `LOOKS.BIN` (this folder's `LOOKS.BIN` is v0.26.1's own and replaces your films).

Make it: `python3 firmware/patch.py --release v0.26.4`. The files here are the patch (only the bytes this build adds; no OM firmware), the card
files and the expected checksums. The pictures were rendered with a different FreeType / DejaVu than upstream's (as v0.26.1.1's).
