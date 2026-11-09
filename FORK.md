# About this fork

This repository is a downstream fork of [androidfanman/caduceus-om3](https://github.com/androidfanman/caduceus-om3)
(Apache-2.0, Copyright 2026 androidfanman; itself based on cakelesscoder/caduceus-ep7), kept to try changes on an OM-3 and
to contribute them back. The licence and NOTICE are unchanged.

| Branch / tag | What |
|---|---|
| `main` | Upstream `main` (remote `upstream`), plus one commit that stops the release workflow publishing releases from this fork. |
| `sdload/v0.25.1`, tag `v0.25.1` | Upstream v0.25 + the WB-grid restart fix (a71bd6b, WB part) + automatic SD loading. `releases/v0.25.1/`. |

No OM firmware is stored here: `releases/*/patch.json` hold only the bytes the patch writes. Contributions go upstream as
pull requests from a branch rebased on upstream `main`.
