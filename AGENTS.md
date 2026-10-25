# exam-prep

## Hard rule: Markdown only

Every tracked file in this repository is Markdown, with three narrow exceptions:

- `.gitignore` and `.gitattributes`
- `.github/**`, `.githooks/**`, `.opencode/**` (the enforcement machinery)
- images under `assets/` (`png`, `jpg`, `jpeg`, `gif`, `svg`, `webp`)

Do not create any other file type — no JSON, YAML, TXT, CSV, PDF, HTML, or
standalone code files. Code samples belong in fenced blocks inside a `.md` file.
Diagrams belong in `assets/` and are referenced from Markdown.

If a task appears to need a different file type, stop and ask instead of
creating it.

## Conventions

- One topic per file, lowercase hyphenated names: `binary-search-trees.md`.
- Link between notes with relative paths so the repo browses well on GitHub.
- Add a new subject to the README progress table when you start it.
- Run `git config core.hooksPath .githooks` once per clone to enable the
  pre-commit check.

## Git flow

`main` is locked: never commit to it and never try to push to it. GitHub rejects
the push. Work on a side branch and open a PR:

```sh
git switch -c notes/<topic>
git commit -am "<topic>: <what changed>"
git push -u origin notes/<topic>
gh pr create --fill
```

The `auto-merge` robot arms auto-merge; GitHub merges once `markdown-only`
passes, then the head branch is deleted. Do not merge a PR whose
`markdown-only` check is red.

PRs that touch `.github/workflows/**` cannot be merged by the robot — GitHub
blocks `GITHUB_TOKEN` from doing that. Ask the user to run
`gh pr merge <n> --squash --delete-branch` for those.
