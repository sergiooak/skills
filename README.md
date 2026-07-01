# skills

🇧🇷 [Leia em português](./README.pt-BR.md)

A personal, growing library of Claude Code skills I use often. Public in case it's useful to someone else — install via [skills.sh](https://www.skills.sh/) or the `skills` CLI, use anything here however you like.

## Structure

```
skills/
├── skills/
│   ├── atomic-commits/    # SKILL.md — split changes into logical commits, Conventional Commits format
│   └── git-safe-rename/   # SKILL.md — enforce `git mv` for renames/moves, preserve history
└── AGENTS.md               # philosophy, conventions, how to contribute (humans + AI agents)
```

## Usage

Install all skills:

```
npx skills add sergiooak/skills
```

Or install one:

```
npx skills add sergiooak/skills --skill atomic-commits
npx skills add sergiooak/skills --skill git-safe-rename
```

- [`atomic-commits`](./skills/atomic-commits/SKILL.md) — splits working-tree changes into multiple logical, atomic commits (never one giant commit), grouped by feature/topic, then writes each message following Conventional Commits rules.
- [`git-safe-rename`](./skills/git-safe-rename/SKILL.md) — forces `git mv` instead of OS-level move/rename on tracked files, so Git history follows the file.

For the reasoning behind the structure and how to add new skills, see [`AGENTS.md`](./AGENTS.md).

## License

MIT — see [LICENSE](./LICENSE).
