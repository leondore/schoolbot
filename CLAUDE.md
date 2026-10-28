# schoolbot

## Privacy: this repo is public

Issues, PRs, commit messages and committed code are publicly indexed. Never put real personal data in them; use placeholders. See `docs/agents/issue-tracker.md` for the substitution list. Real values live only in secrets, deployed config and git-ignored `testdata/`.

## Agent skills

### Issue tracker

GitHub Issues on `leondore/schoolbot` via the `gh` CLI, with a no-personal-data rule. See `docs/agents/issue-tracker.md`.

### Triage labels

Default five-role vocabulary (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: `GLOSSARY.md` and `docs/adr/` at the repo root. See `docs/agents/domain.md`.
