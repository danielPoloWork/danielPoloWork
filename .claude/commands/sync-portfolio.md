---
description: Sync the README Portfolio section from each public repo's .portfolio.json
allowed-tools: Bash(node scripts/sync-portfolio.mjs*), Bash(git diff*), Bash(git add*), Bash(git commit*), Bash(gh*)
---

Update the GitHub profile README so its Portfolio section reflects every public
repository's `.portfolio.json` metadata.

Steps:

1. Run the deterministic generator:
   `node scripts/sync-portfolio.mjs`
   It rewrites only the text between the `<!-- PORTFOLIO:START -->` and
   `<!-- PORTFOLIO:END -->` markers in `README.md`, sourcing each entry from the
   `.portfolio.json` of every public, non-fork repo owned by the profile.

2. Show the resulting `git diff -- README.md` so the user can review what changed.

3. If there are changes, ask the user whether to commit and push. Only commit when
   they confirm. Use a message like `Sync portfolio from repo metadata`.

Notes:
- A repo appears in the portfolio only if it has a `.portfolio.json`. To add or remove
  a project, edit (or delete) that file in the repo itself — no change here is needed.
- Ordering is controlled by the `order` field in each `.portfolio.json` (ascending;
  ties broken alphabetically by title).
- If the generator reports missing markers, the README is missing the START/END pair.
