---
name: git-safe-rename
description: "Rename or move any tracked file or folder using `git mv` instead of OS-level mv/Move-Item/Rename-Item/cp, so Git history follows the file. Use when renaming, moving, or restructuring tracked files or folders — even if history preservation isn't explicitly requested."
user-invocable: true
disable-model-invocation: false
argument-hint: "<source> <destination> — the current and new path for the file or folder"
---

# Git-Safe Rename

Never use OS-level `mv`, `Move-Item`, `Rename-Item`, or `cp` on tracked files — always `git mv`.

## Workflow

1. **Move** — `git mv <source> <destination>`. Stages the delete and the add in one step; Git auto-detects the rename.
2. **Commit alone** — commit the move before any content edits. Git only auto-detects a rename above roughly 50% content similarity; mixing in edits can push it under that threshold and split the file's history.
3. **Verify** — `git log --follow --oneline <destination>`. Done when commits from before the move show up in the output; if they don't, the move landed as a delete+add, not a rename.

## Example

```bash
git mv src/old-name.js src/new-name.js
git mv src/utils/helper.js src/shared/helper.js
```

Commit message: `refactor: move helper.js to shared/`
