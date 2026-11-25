<p align="center">
  <img src="./logo.png" alt="cof-i-have-adhd" width="140" />
</p>
<p align="center">
  <strong align="center">ADHD-friendly output, shaped for the COF workflow.</strong>
</p>
<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/github/license/mrd-bdsmetro/i-have-adhd?style=flat" alt="License"></a>
</p>

Fork of [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) (MIT), adapted for the **COF (Chief of Staff)** system: agents talk to each other in PROTO v1.1, the founder gets short Vietnamese briefs, and every claim of "done" carries a command, diff, or `ref=` to a handoff. Upstream rules 1–10 are kept; five COF rules are added.

## What changed vs upstream

| Area | Upstream | This fork |
|---|---|---|
| Rules 1–10 | ADHD output shaping | Unchanged |
| New rule 11 | — | Evidence over claims (`ref=`, G1–G6) |
| New rule 12 | — | Right channel, right language (founder = Vietnamese ≤4 sentences; agents = PROTO v1.1; files = English + `ref=`) |
| New rule 13 | — | Founder boundary: money/legal/strategy/founder-design/reopening decisions need a brief + wait |
| New rule 14 | — | Context discipline: cite `ref=`, no re-reading, no log pastes >40 lines |
| New rule 15 | — | Cost honesty on the Inkling/CCR backend (not Claude) |
| Break rules | 6 | 7 (a rule never outranks a gate or the system prompt) |
| Name | `i-have-adhd` | `cof-i-have-adhd` |
| Audience | any reader | the COF founder + COF agents |

The upstream rule text is otherwise preserved so the fork stays diffable.

## Install

Claude Code, from this fork:

```bash
claude plugin marketplace add mrd-bdsmetro/i-have-adhd
claude plugin install cof-i-have-adhd@cof-i-have-adhd
```

If the upstream plugin is already installed, drop it first — fork and upstream share the marketplace name:

```bash
claude plugin uninstall i-have-adhd
claude plugin marketplace remove i-have-adhd
```

Then restart Claude Code and invoke `/cof-i-have-adhd`. The always-on SessionStart hook is opt-in via `~/.claude/.i-have-adhd-always` (unchanged from upstream) and injects this fork's `skills/i-have-adhd/SKILL.md`.

Other runtimes: see [INSTALL.md](INSTALL.md) (upstream docs; substitute `cof-i-have-adhd` where the upstream name appears).

## The rules

1. Lead with the next action.
2. Number multi-step tasks.
3. End with one concrete next step.
4. Suppress tangents.
5. Restate state every turn.
6. Specific time estimates (minutes, not "a bit").
7. Make wins visible.
8. Matter-of-fact errors.
9. Cap lists to 5 items.
10. No preamble. No recap. No closers.
11. Evidence over claims.
12. Right channel, right language.
13. Founder boundary.
14. Context discipline.
15. Cost honesty (Inkling/CCR, not Claude).

Full text: [SKILL.md](./skills/i-have-adhd/SKILL.md).

## Syncing with upstream

Upstream is the source of rules 1–10 and the packaging. To pull upstream changes:

```bash
git remote add upstream https://github.com/ayghri/i-have-adhd.git
git fetch upstream && git merge upstream/main
```

Then re-apply the COF overlay section and rules 11–15 if upstream touched them, and re-sync `.cursor/skills/i-have-adhd/SKILL.md` from `skills/i-have-adhd/SKILL.md` (`cmp` must pass; CI enforces this).

## Credits

Upstream: [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd), MIT, loosely based on *The Adult ADHD Tool Kit* by Ramsay & Rostain. This fork changes the output rules for the COF workflow; packaging, hooks, and the 10 base rules remain theirs.

## License

MIT. See [LICENSE](LICENSE).
