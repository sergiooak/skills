---
name: git-safe-rename
description: "MANDATORY skill for ANY file or folder rename, move, relocation, or restructure. Preserves Git history using `git mv`. Use when: renaming files, moving files, reorganizing folders, restructuring directories, relocating modules, changing file paths — even if the user does not explicitly ask to preserve history. This skill MUST be loaded before performing any mv, rename, move, or relocation operation on tracked files."
user-invocable: true
disable-model-invocation: false
argument-hint: "<source> <destination> — the current and new path for the file or folder"
---

# Git-Safe Rename — Always Preserve Git History

> **IMPORTANT**: This skill applies to ALL file/folder moves and renames in this repository.
> Never use OS-level commands (`mv`, `Move-Item`, `Rename-Item`, `cp`) on tracked files.
> Always use `git mv` to preserve commit history.

## Why This Matters

`git log --follow` tracks renames, but only if Git detects the move as a rename (similarity ≥ 50%). This skill ensures every move/rename preserves the full commit history.

## Simple Rename / Move

Use `git mv` instead of OS-level `mv` or `Rename-Item`:

```bash
git mv src/old-name.js src/new-name.js
git mv src/utils/helper.js src/shared/helper.js
```

This stages both the delete and the add in one step. Git auto-detects the rename.

**Rules**:
- Commit the move **separately** from content changes. If you move + heavily edit in the same commit, Git may not detect the rename.
- Keep the commit message descriptive: `refactor: move helper.js to shared/`

## Verify History

After moving, confirm the rename chain is intact:

```bash
git log --follow --oneline src/shared/helper.js
```

You should see commits from before the move.

## Summary Cheat Sheet

| Action | Command | Notes |
|--------|---------|-------|
| Rename | `git mv old new` | Commit move separately from edits |
| Move to new dir | `git mv src/a/file.js src/b/file.js` | Same as rename |
| Verify | `git log --follow --oneline file.js` | Check rename chain |
