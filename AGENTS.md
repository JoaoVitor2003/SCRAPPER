# AGENTS.md

Project-specific instructions for Codex agents working in this repository.

## Project Overview

SCRAPPER is a local session observer for web automation. It captures real browser session data through a browser extension, native messaging host, Python REST API, Rust selector helper, and BertUI dashboard.

Use Codex with the local repository, local API, and exported capture files. Treat old AI demo files as legacy examples only; do not base new Codex work on them unless the user explicitly asks for that specific demo.

## Important Paths

- `README.md` - user-facing project documentation.
- `python_api/api.py` - local REST API at `http://localhost:8080`.
- `extension/brave/` - Chromium extension source for Brave, Chrome, and Edge.
- `extension/firefox/` - Firefox extension source.
- `c_core/native_host/` - native messaging host source and binaries.
- `rust_finder/` - Rust CSS selector helper.
- `ui/scrapperui/` - BertUI/Bun/React dashboard.
- `linux/` and `windows/` - platform release copies.
- `install.sh` and `install.ps1` - platform installers.

## Codex Workflow

Use SCRAPPER to capture browser traffic first, then let Codex inspect local exported files while generating or debugging automation code.

```bash
curl -s "http://localhost:8080/api/v1/session/all" > session.json
curl -s "http://localhost:8080/api/v1/requests/recent?limit=100" > recent_requests.json
```

Keep exported cookies, bearer tokens, and raw session dumps local. Do not paste secrets into docs, issues, commit messages, or remote prompts unless the user explicitly approves it.

## Development Commands

- Python API: `python python_api/api.py`
- UI dev server: run `bun run dev` from `ui/scrapperui/`
- UI production build: run `bun run build` from `ui/scrapperui/`
- Rust helper build: run `cargo build --release` from `rust_finder/`

If dependencies are missing, ask before installing or downloading anything.

## Change Guidelines

- Keep docs and examples generic to SCRAPPER, Codex, and local automation.
- Keep new guidance Codex-specific.
- Do not hard-code captured domains, accounts, cookies, tokens, or private request payloads.
- Preserve existing API endpoint shapes unless the user asks for a breaking change.
- Keep generated captures, logs, and local exports out of commits.
- When changing copied platform trees, update the matching root, `linux/`, and `windows/` copies if the repo structure expects them to stay in sync.

## Verification

Run focused checks based on what changed:

- API changes: `python -m py_compile python_api/api.py`
- UI changes: `bun run build` from `ui/scrapperui/`
- Rust changes: `cargo build --release` from `rust_finder/`
- Documentation changes: search for stale terms with `rg -n -i "codex|agents.md"`
