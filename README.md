# AgingBench — Companion Website

Static site for **AgingBench**, a benchmark for measuring how agent memory and reasoning degrade over multi-session use.

This repo is the GitHub Pages source. The codebase lives separately at
`https://github.com/<ORG>/aging-bench` (link not yet public — swap `<ORG>` before
the launch announcement).

## Deploy

1. Push this repo to GitHub.
2. **Settings → Pages → Source: Deploy from a branch → Branch: `main`, Folder: `/ (root)`**.
3. Wait ~1 minute. The site appears at `https://<ORG>.github.io/<repo-name>/`.

`.nojekyll` is present so GitHub Pages serves files as-is without Jekyll
processing — needed because the demo uses Pyodide assets under `assets/wasm/`
whose filenames start with underscores.

## Before launch: swap `<ORG>` placeholders

Eight occurrences across two files reference the codebase repo:

```
use.html        (5x)  — Quickstart, three install cards, CI snippet
telemetry.html  (3x)  — terminal-user pip recipe + augment-panel hints
```

Replace `<ORG>` (rendered as `&lt;ORG&gt;` in HTML) with your GitHub org/user
once the codebase repo is public. A single `sed` works:

```bash
sed -i 's|&lt;ORG&gt;|your-org|g' use.html telemetry.html
```

## Pages

- `index.html` — landing page
- `use.html` — three install modes (local-run, telemetry, controlled-suite)
- `telemetry.html` — in-browser demo (Pyodide; no backend)
- `docs.html` — reference: schema, mechanisms, profiles
- `leaderboard.html` — submitted AgingCards

## Notes

- The Pyodide demo (`assets/js/telemetry_demo.js` + `assets/wasm/`) runs entirely
  client-side. No backend service is needed.
- Sample traces under `assets/sample_traces/` are anonymized; one ~4 MB
  `claude_code.jsonl` is the largest asset.
- The `release/` press kit (tweet thread, LinkedIn post) is intentionally **not**
  in this deploy bundle — it lives only in the working repo.
