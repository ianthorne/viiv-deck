# Patient Pathways — prototype

Interactive playtest prototype of the Patient Pathways SDM card game (ViiV NL).
Static, single-file, no build — serves directly from GitHub Pages.

**A neutral SDM + barrier-diagnosis instrument, not a promotion tool.** See `CLAUDE.md`
for the full design brief and the rules that govern every change.

## Run locally

Just open `index.html` in a browser, or:

```bash
python3 -m http.server 8000   # then visit http://localhost:8000
```

## Live (GitHub Pages)

Enabled via repo Settings → Pages → Deploy from a branch → `main` / root.
URL: `https://<your-username>.github.io/viiv-deck/`

## Status

Scaffold of the **sceptic / barrier** demo module and the round loop:
case → conversation → provisional choice → twist → does it hold → capture.
Clinical/product content is intentionally placeholder pending ViiV-supplied,
compliance-checked input. Build target: live role-play at the Cycle Meeting (24–25 Sept).
