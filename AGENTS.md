# Agent Instructions

Personal skills lib for Claude Code.

## Repo purpose

Reusable, self-contained Claude Code skills. One skill = one directory + `SKILL.md`. Not prompts, not generic scripts — model-invocable capabilities with explicit trigger conditions.

## Structure

- `skills/<name>/SKILL.md` — flat, one level deep. Matches the `skills` CLI's default discovery path (`skills/<name>/SKILL.md`).
- `skills/<name>/` may hold supporting files (scripts, references) alongside `SKILL.md` if a skill needs them — not the case yet.

## Philosophy

**One directory per skill, no categories yet.** Split into `skills/<category>/<name>/` only once the collection is big enough that a flat list gets hard to scan — not preemptively.

**`SKILL.md` is the whole skill.** Frontmatter (`name`, `description`, `user-invocable`, `disable-model-invocation`, `argument-hint`) plus one markdown body. No separate config files.

**`description` = trigger, not blurb.** It decides whether Claude auto-invokes the skill — write it as "use when X, Y, Z" trigger conditions, not marketing copy.

**Name = what people search for.** Kebab-case, keyword-rich, matches what someone would type into `npx skills add` or the skills.sh search box — not a clever/branded name.

## Access pattern

Skills install via the [skills.sh](https://www.skills.sh/) CLI: `npx skills add sergiooak/skills` (all) or `npx skills add sergiooak/skills/<name>` (one). Listing/ranking on skills.sh is automatic from install telemetry — no submission step required.

## Adding a skill

1. `mkdir skills/<name>` — name = kebab-case, keyword-rich.
2. Write `SKILL.md`: frontmatter (`name`, `description` with trigger conditions) + body (workflow, rules, examples).
3. Test it locally in `~/.claude/skills/<name>` before publishing.
4. Commit: `feat: add <name> skill`.

## Conventions

- Frontmatter fields: `name`, `description`, `user-invocable`, `disable-model-invocation`, `argument-hint` (when the skill takes args).
- No build, no tests, no CI. Just markdown edits.
