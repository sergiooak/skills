# Partial File Staging

When a single file has changes belonging to different commits, split it below the file level with `git add -p` instead of staging the whole file.

**Split when:**

- The file's changes belong to 2+ different logical commits
- Separators/formatting were added alongside behavior changes
- A shared module gained functions for different features

**Don't split when:**

- All changes in the file serve the same purpose
- Splitting would leave a commit where the code doesn't compile or run
- The hunks are too interleaved to separate cleanly

```bash
# Interactive hunk selection (preferred)
git add -p <file>
# y=stage, n=skip, s=split hunk, q=quit

# Stage a specific line range via patch application
git diff <file> | head -n <end> | tail -n <count> | git apply --cached
```

Rule: every commit must leave the codebase valid and runnable — never split a file in a way that breaks an intermediate commit.
