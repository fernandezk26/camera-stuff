# Caduceus for OM-3 v0.26.5 (the camera's own WB screen from the WB row, no grid on the row, no redirect on the way out)

**v0.26.4 with two changes, nothing else.** A downstream build of [androidfanman/caduceus-om3](https://github.com/androidfanman/caduceus-om3) v0.26.1.
**Emulator only: no camera test of this build.** v0.26.4 was tried on a camera: after changing the WB in the camera's WB screen and pressing MENU, live view froze, and then the
whole camera froze at the next half-press (battery out). The cause is not proven.

- **The WB row no longer shows the grid.** The row shows only "WB" and its small WB± icon. OK (or left / right / a dial) opens the camera's own WB screen, and
  the WB± cell there (its icon) opens the fine-tune grid with the film's own shift, as in v0.26.4.
- **Every way out of the camera's WB screen is the camera's own** (MENU, OK, half-press, time-out). v0.26.4 sent MENU back to Picture Mode by changing the screen's ending;
  that is removed. MENU in the fine-tune grid still goes back to the WB screen. The automatic save of WB changes into the film (v0.26.3) is unchanged.
- Space: `.ext11` 65072 / 65536 (48 B less than v0.26.4); `GUIDES.BIN` size unchanged.

**Going back to v0.26.4, v0.26.3 or v0.26.2:** same file formats, nothing to clean. **Older:** see v0.26.3's notes (delete `OM3MOD/BUNDLES.BIN` when going back to v0.26.1.1).

**Copy to the card:** `DCOLYMP` (flash it) and `OM3MOD` `GUIDES.BIN` (made for this firmware: always copy it with it), `LABELS.BIN` and `TONES.BIN` (as v0.26.3's).
Keep your `EDITS.BIN`, `NAMES.BIN`, `BUNDLES.BIN` and `LOOKS.BIN`.

Make it: `python3 firmware/patch.py --release v0.26.5`.
