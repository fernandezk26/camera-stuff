# Caduceus for OM-3 v0.26.3 (the 0xFF fix + automatic WB save into the film)

**v0.26.2 (v0.26.1.1 + a stored WB per film) with two changes, and nothing else.** A downstream build of
[androidfanman/caduceus-om3](https://github.com/androidfanman/caduceus-om3) v0.26.1. **Emulator only: no camera test of this build.**

- **Fix.** The camera could write a `BUNDLES.BIN` that its own check refuses at the next power-on (your COLOR 1–4 slot changes then start neutral).
  Cause: 0xFF bytes in `EDITS.BIN` records (the camera's memory block for the per-film changes was never cleared; the file from the first
  SD-loader build already had them) were copied into the live COLOR slot when a film was chosen. Now the block is cleared when it is made, a good
  `EDITS.BIN` is cleaned when it is read, the live slot is cleaned after every film choice, and the copy of the slots that goes to `BUNDLES.BIN`
  is cleaned before it is written.
- **Automatic WB save.** While a COLOR holds a film, **any change of the camera's WB** (Super Control Panel, WB menu, a button) is copied into that
  film (WB mode, and the Kelvin for Custom WB). Choosing the film later (from another film or COLOR) writes it back, as in v0.26.2. Films you never
  changed follow the camera's WB. COLOR 1–4 themselves, and other picture modes, store nothing; the recall's own writes are not stored back. **INFO**
  on the WB row still works: it stores the camera's WB, or lets a stored WB go when the film already holds exactly that (the next WB change you make
  on that film stores it again). The change is kept in the camera's memory at once and written to the card at the next half-press, like the other
  film changes (`BUNDLES.BIN`, and `EDITS.BIN` when you leave the film). Nothing on screen shows a stored WB.

**The `BUNDLES.BIN` on a card that ran v0.26.2:** if the camera wrote one with 0xFF in it, v0.26.3 refuses it once at power-on (the slot bank starts
neutral; your films' own changes in `EDITS.BIN` are kept) and writes a good file at the next half-press. To start clean on purpose, delete
`OM3MOD/BUNDLES.BIN` (keep a copy first if you like). `EDITS.BIN` is cleaned when read and needs no action.

**Going back to v0.26.1.1 or older:** a film that holds a stored WB makes `BUNDLES.BIN` carry four extra bytes, which the older firmware refuses
(whole file; `BUNDLES.BAK` is the previous one). Now that every WB change is stored, assume it will happen: delete `OM3MOD/BUNDLES.BIN` when you go back,
or accept the neutral slot bank. `EDITS.BIN` is read by the older firmware without a problem.

**Copy to the card:** `DCOLYMP` (flash it) and `OM3MOD` `GUIDES.BIN` (made for this firmware: always copy it with it), `LABELS.BIN` and `TONES.BIN`.
Keep your `EDITS.BIN`, `NAMES.BIN`, `BUNDLES.BIN` and `LOOKS.BIN` (this folder's `LOOKS.BIN` is v0.26.1's own and replaces your films).

Make it: `python3 firmware/patch.py --release v0.26.3`. The files here are the patch (only the bytes this build adds; no OM firmware), the card
files and the expected checksums. The pictures were rendered with a different FreeType / DejaVu than upstream's (as v0.26.1.1's).
