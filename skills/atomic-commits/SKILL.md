---
name: atomic-commits
description: "Split working-tree changes into atomic, logical commits — never one giant commit — grouped by feature/topic, each written to Conventional Commits format. Use when committing changes or reviewing/planning a commit before executing it."
user-invocable: true
disable-model-invocation: false
argument-hint: "[commit | review | plan] — 'commit' stages and commits directly, 'review' or 'plan' shows the plan for approval first"
---

# Atomic Commits

## Workflow

1. **Inspect** — `git status` + `git diff` (staged and unstaged) to see everything that changed.
2. **Group** — cluster files into atomic, logical commit units (see Grouping below). Every changed file must end up in exactly one group.
3. **Draft messages** — one message per group, in Conventional Commits format (below).
4. **Check breaking changes** — any group with a breaking change: pause, confirm with the user (see Breaking Changes) before proceeding.
5. **Stage and commit** — "commit": run all commits after the breaking-change check. "review"/"plan": present the grouping and messages, wait for approval, then commit.
6. **Summarize** — `git log --oneline -<n>` (n = commits made), show it to the user.

---

## Grouping

Group into the smallest commits that could be reviewed independently:

- Same feature → one commit
- Tests for a changed module → same commit as the module
- Docs → separate `docs` commit
- Config/tooling → separate `chore`/`build` commit
- Formatting-only → separate `style` commit

Never mix behavior changes with style or docs in one commit.

**Unrelated changes in one file** (e.g. a new constant plus an unrelated fix) need splitting below the file level — see [`partial-staging.md`](./partial-staging.md).

---

## Commit Format

```
<type>(<scope>): <summary>

- <change 1>
- <change 2>
- <change 3>

[BREAKING CHANGE: <description>]
```

### Header

- Target ≤ 50 chars, hard limit 72: `type(scope): summary`
- Too long? Drop articles, abbreviate, shorten verbs (`implement` → `add`, `resolve issue where` → `fix`)

### Types

| Type       | When to use                                 |
|------------|----------------------------------------------|
| `feat`     | New feature or capability                    |
| `fix`      | Bug fix                                      |
| `docs`     | Documentation only                           |
| `style`    | Formatting / whitespace / separators         |
| `refactor` | Code restructuring with no behavior change   |
| `test`     | Tests added or updated                       |
| `chore`    | Tooling, deps, config                        |
| `ci`       | CI/CD pipelines                              |
| `build`    | Build system / dependency changes            |

### Scope

PascalCase, module/domain name — not the file name: `feat(Auth): add JWT login`. Skip it when the type is `chore`/`ci`/`build` on config files, or the change spans many unrelated domains.

### Body

Bullet list of *what* changed, one fact per line — not *why* (that belongs in the PR description). Omit trivial details unless they affect callers. 3–6 bullets is typical; fewer if the summary already says it all.

### Breaking Changes

- Header: `!` after type/scope — `feat(Auth)!: remove legacy login`
- Footer: `BREAKING CHANGE: <what changed and what callers must do>`
- Always confirm before committing: "This commit contains a breaking change: `<description>`. Proceed?"

---

## Examples

### Standard, with scope

```
feat(FieldMatcher): add confidence threshold filtering

- Add MIN_CONFIDENCE constant (default 0.85)
- Filter Textract blocks below threshold before matching
- Update matchFields() return type to include confidence
```

### No scope (cross-cutting docs)

```
docs: add bilingual OCR pipeline documentation

- Create docs/ocr.md (English)
- Create docs/ocr.pt-BR.md (Portuguese)
- Add cross-links between both files
```

### Breaking change

```
feat(Queries)!: rename comprovante status field

- Rename DB column reference from `status` to `statusOCR`
- Update all SELECT and UPDATE queries in queries.js

BREAKING CHANGE: DB column `status` was renamed to `statusOCR` — run migration before deploying
```
