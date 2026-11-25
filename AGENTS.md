# Agent guide

This is a **fork** of [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd), adapted for the COF (Chief of Staff) workflow. Upstream is `upstream/main`; this repo is `origin/main`. Read `README.md` for what changed.

## Start here

1. `README.md` — purpose and fork delta.
2. `skills/i-have-adhd/SKILL.md` — the canonical behavior. This is the file to edit when changing rules.
3. `INSTALL.md` — upstream install docs (names not yet rewritten; substitute `cof-i-have-adhd`).
4. `CONTRIBUTING.md` before proposing changes.

## Source-of-truth rules

- Change `skills/i-have-adhd/SKILL.md` first, then copy it byte-identically to `.cursor/skills/i-have-adhd/SKILL.md` (`cmp` must pass — CI enforces).
- Rules 1–10 and the packaging (hooks, manifests, install docs) track upstream. Rules 11–15 and the "COF overlay" section are this fork's; do not push them upstream without asking the founder.
- Keep the `i-have-adhd` **directory** name under `skills/` (hooks and tests reference it). The **plugin name** is `cof-i-have-adhd`.
- Version bumps: bump `version` in `.claude-plugin/plugin.json`, `.codex-plugin/plugin.json`, `package.json`, `qwen-extension.json`, `kimi.plugin.json` together.

## Verification

```bash
python3 -m unittest discover -s tests -v
python3 scripts/run_evals.py validate
```

Hooks must stay silent without the opt-in flag (`~/.claude/.i-have-adhd-always`). Do not change hook behavior to auto-enable.

## Do not

- Do not remove the upstream attribution in LICENSE, README, or SKILL.md frontmatter.
- Do not rename `skills/i-have-adhd/` — tests and hooks hard-code it.
- Do not add founder-specific private data (names, keys, paths outside this repo) to any file here.
