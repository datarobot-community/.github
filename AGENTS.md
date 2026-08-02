# AGENTS.md

Guidance for coding agents working in this repository.

## What this repo is

The `.github` repo for the [@datarobot-community](https://github.com/datarobot-community) GitHub
organization. It holds org-level defaults, not application code:

- `profile/README.md` — the org profile page rendered at
  <https://github.com/datarobot-community>. Public, indexed, and the first thing most people see.
- `.github/workflows/` — org-level shared workflows.

Almost all work here is editing `profile/README.md`.

## Repository listing rules

`profile/README.md` links to repositories across the DataRobot GitHub orgs. Every link is a public
endorsement, so the listing is governed by hard rules. These apply to **every** repository
reference on the page, in any org (`datarobot-community`, `datarobot`, `datarobot-oss`,
`datarobot-forks`) and in any form — tables, bullets, prose, and the collapsed
"Looking for something that isn't listed?" section.

### Must

- **Public only.** A repository may be listed only if its visibility is `PUBLIC`.
- **Non-archived only.** A repository may be listed only if `isArchived` is `false`.
- **Actively maintained only.** A repository may be listed only if it has been pushed to within
  the last **9 months**. Anything older is stale — remove it.

### Must not

- **Never list an internal or private repository.** Not in a table, not in prose, not in a
  footnote, not "for reference". Private repo names can themselves be sensitive; if you are unsure
  whether a repo is public, verify before writing it down, and omit it if you cannot verify.
- **Never list an archived repository**, even to mark it deprecated. Archived means gone from this
  page. (A *non-archived but deprecated* repo may be called out as deprecated with a pointer to its
  replacement — that is what the `datarobot-agent-templates` note does.)
- **Never link a repo you have not verified exists and is reachable.** A 404 on the org profile is
  worse than an omission.

### Verify before you edit

Run these before adding, and before any pass that touches the listing:

```bash
# Every public, non-archived repo in the org, newest push first
gh repo list datarobot-community --limit 200 --no-archived --visibility public \
  --json name,pushedAt,description,isArchived,visibility \
  --jq 'sort_by(.pushedAt) | reverse | .[] | "\(.pushedAt[:10])  \(.name)"'

# Check one specific repo (any org) before linking it
gh repo view <org>/<repo> --json name,visibility,isArchived,pushedAt,description
```

`pushedAt` is the freshness signal — it covers pushes to any branch, which is the practical
definition of "someone is still working on this."

To find entries that have gone stale, extract the linked repos from the README and check each:

```bash
grep -oE 'github\.com/(datarobot|datarobot-community|datarobot-oss|datarobot-forks)/[A-Za-z0-9._-]+' \
  profile/README.md | sed 's|github.com/||' | sort -u | while read -r r; do
    gh repo view "$r" --json nameWithOwner,visibility,isArchived,pushedAt \
      --jq '[.nameWithOwner, .visibility, (.isArchived|tostring), .pushedAt[:10]] | @tsv' \
      2>/dev/null || echo -e "$r\tNOT-FOUND"
done
```

Anything that comes back non-`PUBLIC`, `true` for archived, `NOT-FOUND`, or with a `pushedAt` older
than 9 months from today must be removed from `profile/README.md` in the same change.

### When pruning

- Remove the row or bullet entirely rather than leaving a commented-out stub.
- If a pruned repo was the only entry in a section, remove the section heading and its intro too —
  don't leave an empty table.
- If a pruned repo has a live successor, add a one-line pointer to the successor instead of the
  dead entry.
- Repos that are legitimately dormant but still correct (a stable Terraform provider, say) are
  still subject to the 9-month rule. The rule is deliberately mechanical; if a listing genuinely
  needs an exception, raise it with the user rather than silently keeping it.

## Editing profile/README.md

- Keep the existing structure: org comparison table → "Start here" → thematic sections → get
  involved. Don't reorganize without being asked.
- Keep the tone: second person, concrete, no marketing superlatives. Describe what a repo *builds*
  or *adds*, not how great it is.
- Descriptions are one sentence. Two at most, and only when the second one earns it.
- GitHub renders this file with the standard GFM subset — `> [!NOTE]`, `> [!TIP]`, tables, and
  `<details>` all work. Raw HTML beyond the centered header block does not always render, so avoid
  adding more.
- Preview locally with `gh markdown-preview` or by pushing to a branch; the org profile only
  renders from `profile/README.md` on the default branch.

## Workflow

- Branch naming: `<github-user>/<short-name>`.
- Run `git diff` before committing; commit messages start with a verb ("adds", "prunes", "fixes").
- Do not `git push` — leave that to the human.
