# Exam Prep

An open workspace for exam preparation: notes, summaries, and practice material,
kept in Markdown so everything stays diff-friendly and searchable.

## Status

Scaffolding only — no study content yet. The repo has this README, `AGENTS.md`,
`assets/` for diagrams, and the guardrails that keep it Markdown-only.

### Markdown-only rule

Everything tracked here is `.md`, except `.gitignore`, `.gitattributes`, the
`.github/`/`.githooks/`/`.opencode/` config, and images under `assets/`.

| Layer | Where | Purpose |
| --- | --- | --- |
| Ignore allowlist | `.gitignore` | Non-Markdown files never show up in `git status` |
| Pre-commit hook | `.githooks/pre-commit` | Rejects the commit locally |
| CI check | `.github/workflows/markdown-only.yml` | Fails the build on any non-allowlisted file |
| Ruleset | branch `main` | Requires the CI check; direct pushes are blocked |
| Auto-merge robot | `.github/workflows/auto-merge.yml` | Arms auto-merge; GitHub merges only when the check is green |
| Agent rules | `.opencode/opencode.jsonc`, `AGENTS.md` | Stops the agent creating other file types |

Enable the hook once per clone:

```sh
git config core.hooksPath .githooks
```

### Branch flow

`main` is locked. Nothing is pushed to it directly — GitHub rejects the push.
Every change goes through a side branch and a pull request:

```sh
git switch -c notes/graphs          # one branch per change
git commit -am "graphs: add traversal notes"
git push -u origin notes/graphs
gh pr create --fill                 # robot arms auto-merge on open
```

The `auto-merge` workflow queues the PR for squash merge. GitHub then merges it
itself, but only after the required `markdown-only` check passes. If the branch
contains a file that is not Markdown (or an allowlisted exception), that check
fails and the PR stays open — no bad file can reach `main`. Merged branches are
deleted automatically.

To review a PR without merging, open it as a **draft**; the robot skips drafts.

**One exception:** a PR that changes `.github/workflows/**` cannot be merged by
the robot. GitHub forbids `GITHUB_TOKEN` from merging workflow changes (it can
never hold the `workflows` permission), so merge those yourself:

```sh
gh pr merge <number> --squash --delete-branch
```

The branch cleanup still runs either way.

## Planned structure

```text
exam-prep/
├── README.md
├── notes/          # one file per topic, written while studying
├── subjects/       # per-subject index pages linking to notes
├── practice/       # questions, past papers, worked solutions
└── cheatsheets/    # one-page condensed revision sheets
```

Each folder gets an `index.md` as a table of contents, so the repo stays
navigable on GitHub without any tooling.

## How to use this repo

1. **Capture as you go.** Write notes in your own words, one topic per file.
2. **Link, don't duplicate.** Index pages link to notes; a fact lives in one place.
3. **Practice beats rereading.** Add attempts and corrections to `practice/`,
   including the mistakes — those are the valuable part.
4. **Condense late.** Cheatsheets are written in the final pass, from the notes,
   not copied from a textbook.
5. **Commit often.** Small commits with a subject prefix, e.g.
   `git commit -m "algorithms: add graph traversal notes"`.

## Progress

| Subject | Notes | Practice | Cheatsheet | Confidence |
| --- | --- | --- | --- | --- |
| _add subjects here_ | — | — | — | — |

## Conventions

- Markdown only (`.md`), UTF-8, one topic per file.
- File names: lowercase, hyphenated, e.g. `binary-search-trees.md`.
- Dates in ISO format (`2026-10-25`) where they matter.
- Keep line lengths reasonable so diffs stay readable.

---

Public repository. Shared for reference; corrections and suggestions are welcome.
