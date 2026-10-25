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
| Agent rules | `.opencode/opencode.jsonc`, `AGENTS.md` | Stops the agent creating other file types |

Enable the hook once per clone:

```sh
git config core.hooksPath .githooks
```

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
