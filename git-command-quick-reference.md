# Git Command Quick Reference

**Version:** v1.12.0  
**Full guide:** [`git-repository-guide.md`](git-repository-guide.md)  
**Quick-start guide:** [`git-repository-guide-quick-start-guide.md`](git-repository-guide-quick-start-guide.md)  
**Cheat sheet:** [`git-repository-guide-cheat-sheet.md`](git-repository-guide-cheat-sheet.md)

This is a practical quick reference for commonly used Git commands.

It is intentionally command-focused. Use the full guide when you need deeper explanations, examples, troubleshooting, or workflow context.

---

## Filename note

Recommended standalone filename:

```text
git-command-quick-reference-v1.12.0.md
```

Recommended stable repository filename, if you prefer non-versioned companion filenames inside an actual Git repository:

```text
git-command-quick-reference.md
```

Document title casing:

```text
Git Command Quick Reference
```

---

## How to read this reference

Each command includes:

- **What it does**: short description.
- **Common syntax**: beginner-friendly example.
- **Required parameters**: values you must supply.
- **Optional parameters**: useful flags or arguments.
- **Notes**: practical warnings or clarifications.

Placeholders such as `branch-name`, `file-name.md`, `old-tag`, and `new-tag` are variables. Replace them with your actual names.

---

## Most common commands, roughly ranked

| Rank | Command | Why it matters |
|---:|---|---|
| 1 | `git status` | Shows what changed and what is staged. Use constantly. |
| 2 | `git add` | Stages changes for the next commit. |
| 3 | `git commit` | Saves staged changes into Git history. |
| 4 | `git push` | Sends local commits or tags to a remote such as GitHub. |
| 5 | `git pull` | Gets remote changes and integrates them into your current branch. |
| 6 | `git diff` | Shows exactly what changed. |
| 7 | `git log` | Shows commit history. |
| 8 | `git branch` | Lists, creates, or renames branches. |
| 9 | `git switch` | Switches branches or creates a new branch. |
| 10 | `git tag` | Creates or lists version tags. |
| 11 | `git restore` | Restores files or unstages staged changes. |
| 12 | `git remote` | Manages remote repository connections. |
| 13 | `git fetch` | Downloads remote history without integrating it. |
| 14 | `git merge` | Combines another branch/history into the current branch. |
| 15 | `git mv` | Renames or moves tracked files. |
| 16 | `git rm` | Removes tracked files from Git. |
| 17 | `git clone` | Copies an existing repository. |
| 18 | `git init` | Creates a new local Git repository. |
| 19 | `git show` | Shows details for a commit, tag, or object. |
| 20 | `git archive` | Exports a repository snapshot, often as a ZIP. |

---

---

# Commit message prefix quick reference

Commit prefixes are not Git commands. They are a convention used inside commit message text.

Pattern:

```text
type: short imperative summary
```

Common examples:

```bash
git commit -m "docs: document commit message prefixes"
git commit -m "fix: correct canonical domain"
git commit -m "feat: add web applications section"
git commit -m "chore: prepare v2.1.0 release"
```

| Prefix | Meaning | Use when |
|---|---|---|
| `feat` | Feature | User-visible content, capability, page, endpoint, or section is added or expanded |
| `fix` | Bug fix | Something wrong, broken, stale, misleading, or misplaced is corrected |
| `docs` | Documentation | Documentation-only files change |
| `chore` | Maintenance | Routine maintenance, release prep, metadata refresh, or housekeeping |
| `refactor` | Restructure | Internal structure changes without intended visible behavior change |
| `style` | Formatting | Whitespace, indentation, line endings, or formatting-only changes |
| `test` | Tests | Tests, test data, or validation scripts change |
| `build` | Build/dependencies | Build scripts, Dockerfiles, package files, or dependencies change |
| `ci` | CI/CD | GitHub Actions, deployment automation, or validation workflows change |
| `perf` | Performance | Speed, size, load time, or efficiency improves |
| `revert` | Revert | A previous commit is intentionally undone |

Optional scope pattern:

```text
type(scope): summary
```

Examples:

```bash
git commit -m "docs(readme): add repository navigation"
git commit -m "fix(metadata): correct canonical domain"
git commit -m "feat(portfolio): add web applications section"
```

Breaking-change pattern:

```bash
git commit -m "feat!: replace guide structure" -m "BREAKING CHANGE: The guide section order and anchor names changed."
```


# Alphabetical command reference

## `git add`

### What it does

Stages file changes for the next commit.

### Common syntax

```bash
git add file-name.md
git add .
git add -A
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Pathspec, such as `file-name.md`, `.`, or folder name | Usually | Tells Git what changes to stage. |

### Optional parameters

| Option | Meaning |
|---|---|
| `.` | Stages changes under the current directory. |
| `-A` or `--all` | Stages additions, modifications, and deletions across the working tree. |
| `-p` or `--patch` | Interactively choose parts of files to stage. |

### Notes

Use `git status` before and after `git add`.

For rename/delete workflows, prefer:

```bash
git add -A
```

---

## `git archive`

### What it does

Creates an archive file, such as a ZIP, from a commit, branch, or tag.

### Common syntax

```bash
git archive --format=zip --output project-v1.0.0.zip v1.0.0
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Tree-ish, such as `v1.0.0`, `main`, or `HEAD` | Yes | The repository snapshot to export. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--format=zip` | Creates a ZIP archive. |
| `--output file.zip` | Writes the archive to the specified filename. |
| `--prefix folder-name/` | Places archived files under a top-level folder inside the archive. |

### Notes

Use this when you want a local ZIP of a tagged version.

---

## `git branch`

### What it does

Lists, creates, deletes, or renames branches.

### Common syntax

```bash
git branch
git branch -a
git branch -M main
git branch -d branch-name
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Branch name | Required for creating, deleting, or renaming | The branch to operate on. |

### Optional parameters

| Option | Meaning |
|---|---|
| `-a` | Lists local and remote-tracking branches. |
| `-M new-name` | Renames the current branch, forcing the rename if needed. |
| `-d branch-name` | Deletes a fully merged local branch. |
| `-D branch-name` | Force-deletes a local branch. Use carefully. |

### Notes

Use `git switch` for switching branches. Use `git branch` mainly for listing, deleting, or renaming.

---

## `git checkout`

### What it does

Older multi-purpose command for switching branches or restoring files.

### Common syntax

```bash
git checkout branch-name
git checkout -b new-branch-name
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Branch, commit, or path | Usually | What to check out or restore. |

### Optional parameters

| Option | Meaning |
|---|---|
| `-b branch-name` | Creates and switches to a new branch. |

### Notes

This guide generally prefers newer, clearer commands:

```bash
git switch branch-name
git restore file-name.md
```

---

## `git clone`

### What it does

Copies an existing repository to your local computer.

### Common syntax

```bash
git clone https://github.com/OWNER/REPO.git
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Repository URL | Yes | The remote repository to clone. |

### Optional parameters

| Option or parameter | Meaning |
|---|---|
| Folder name after URL | Clones into that local folder name. |
| `--branch branch-or-tag` | Checks out the specified branch or tag after cloning. |
| `--depth 1` | Creates a shallow clone with limited history. |

### Notes

Use `git clone` when the repository already exists somewhere else.

Use `git init` when you are starting a new local repository from an existing folder.

---

## `git commit`

### What it does

Saves staged changes into local Git history.

### Common syntax

```bash
git commit -m "Describe what changed"
git commit -m "Summary" -m "Longer body explaining why."
git commit --amend -m "Corrected commit message"
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Staged changes | Yes | Git needs staged changes to create a normal commit. |
| Commit message | Yes | Describes the commit. |

### Optional parameters

| Option | Meaning |
|---|---|
| `-m "message"` | Supplies a commit message from the command line. |
| Multiple `-m` flags | First `-m` is summary; later `-m` values form the body paragraphs. |
| `--amend` | Replaces the most recent commit. Use carefully after pushing. |

### Notes

A one-line commit message is often enough.

A commit body is optional and useful when the why/context matters.

Commit-message prefixes such as `docs:`, `fix:`, `feat:`, and `chore:` are conventions, not Git commands.

---

## `git config`

### What it does

Gets or sets Git configuration values.

### Common syntax

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Config key | Required when setting/getting a specific value | Example: `user.name`. |
| Config value | Required when setting | Example: `"Your Name"`. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--global` | Applies setting to your user account. |
| `--local` | Applies setting only to the current repository. |
| `--list` | Lists active configuration values. |

### Notes

Set `user.name` and `user.email` before committing if Git asks for identity information.

---

## `git diff`

### What it does

Shows differences between files, commits, branches, or tags.

### Common syntax

```bash
git diff
git diff --cached
git diff old-tag..new-tag
git diff --name-status v1.1.0..v1.1.1
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| None | No | With no arguments, shows unstaged changes. |
| Revision range | Optional | Compares two commits, branches, or tags. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--cached` or `--staged` | Shows staged changes. |
| `--stat` | Shows summary statistics. |
| `--name-only` | Shows only changed filenames. |
| `--name-status` | Shows changed filenames plus status codes. |
| `--find-renames` | Enables rename detection. |
| `--diff-filter=A` | Shows only added files. Other filters include `M`, `D`, `R`, and `C`. |

### Notes

Very useful before committing:

```bash
git diff
git diff --cached
```

Very useful between version tags:

```bash
git diff --name-status old-tag..new-tag
```

---

## `git fetch`

### What it does

Downloads remote history without integrating it into your current branch.

### Common syntax

```bash
git fetch
git fetch origin
git fetch --all
git fetch --prune
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Remote name | Optional | Example: `origin`. If omitted, Git uses the default remote for the current branch. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--all` | Fetches from all remotes. |
| `--prune` | Removes stale remote-tracking branches that no longer exist on the remote. |
| `--tags` | Fetches tags explicitly. |

### Notes

Use `git fetch` when you want to inspect remote changes before merging or rebasing.

---

## `git init`

### What it does

Creates a new local Git repository.

### Common syntax

```bash
git init -b main
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| None | No | Running `git init` initializes the current folder as a repository. |

### Optional parameters

| Option | Meaning |
|---|---|
| `-b main` | Creates the initial branch with the specified name. |
| `--initial-branch=main` | Long-form equivalent of `-b main`. |

### Notes

Use this inside the folder you want Git to track.

---

## `git log`

### What it does

Shows commit history.

### Common syntax

```bash
git log
git log --oneline
git log --oneline --decorate --graph --all
git log --all --grep="Ve0sion" --oneline
git log --follow -- file-name.md
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| None | No | Shows history for the current branch. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--oneline` | Shows each commit on one line. |
| `--decorate` | Shows branch and tag names. |
| `--graph` | Shows a text graph of branches/merges. |
| `--all` | Shows all refs, not only the current branch. |
| `--grep="pattern"` | Filters commit messages matching a pattern. |
| `--regexp-ignore-case` | Makes grep matching case-insensitive. |
| `--format="..."` | Customizes log output. |
| `--follow -- file` | Follows file history across renames. |
| `-p` | Shows patches/diffs for commits. |

### Notes

For a readable history graph:

```bash
git log --oneline --decorate --graph --all
```

---

## `git ls-tree`

### What it does

Lists files stored in a tree object, such as a commit or tag snapshot.

### Common syntax

```bash
git ls-tree -r --name-only HEAD
git ls-tree -r --name-only v1.1.1
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Tree-ish, such as `HEAD`, `main`, or `v1.1.1` | Yes | Snapshot to inspect. |

### Optional parameters

| Option | Meaning |
|---|---|
| `-r` | Recursively lists files in subfolders. |
| `--name-only` | Shows only file paths. |

### Notes

Use this to answer:

> What files are contained in this commit or tag?

---

---

## `git ls-files`

### What it does

Lists files in the index and can show end-of-line information.

### Common syntax

```powershell
git ls-files --eol
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| None | No | Lists tracked/indexed files. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--eol` | Shows index, working-tree, and attribute end-of-line information. |
| Pathspec | Limits output to matching files. |

### Notes

Use this to inspect LF/CRLF behavior after adding `.gitattributes`.

---

## `git ls-remote`

### What it does

Shows references available in a remote repository.

### Common syntax

```powershell
git ls-remote --tags origin v1.0.0
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Remote name or URL | Usually | Example: `origin`. |
| Pattern | Optional | Example: `v1.0.0`. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--tags` | Shows tags from the remote. |
| `--heads` | Shows branches from the remote. |

### Notes

Useful after replacing a pushed tag to verify the remote tag exists.

---

## `git rev-list`

### What it does

Lists commit objects reachable from a commit, branch, or tag.

### Common syntax

```powershell
git rev-list -n 1 v1.0.0
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Revision, branch, or tag | Yes | The starting point to inspect. |

### Optional parameters

| Option | Meaning |
|---|---|
| `-n 1` | Limits output to one commit. |
| `--max-count=1` | Long-form style equivalent to limiting count. |

### Notes

In PowerShell, this safely stores the commit that a tag points to:

```powershell
$commit = git rev-list -n 1 v1.0.0
```

That is useful when deleting and recreating an older pushed tag without moving it to `HEAD`.


## `git merge`

### What it does

Combines another branch or commit history into the current branch.

### Common syntax

```bash
git switch main
git merge branch-name
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Branch or commit | Usually | The branch or commit to merge into the current branch. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--abort` | Aborts an in-progress merge. |
| `--continue` | Continues after conflicts are resolved. |
| `--no-ff` | Creates a merge commit even if fast-forward is possible. |
| `--ff-only` | Only merges if Git can fast-forward. |

### Notes

Always know which branch you are currently on before merging:

```bash
git status
```

---

## `git mv`

### What it does

Renames or moves a tracked file, directory, or symbolic link.

### Common syntax

```bash
git mv old-name.md new-name.md
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Source path | Yes | Existing tracked file or folder path. |
| Destination path | Yes | New file or folder path. |

### Optional parameters

| Option | Meaning |
|---|---|
| `-f` | Forces rename/move if the destination exists. Use carefully. |
| `-k` | Skips move/rename actions that would fail. |

### Notes

After `git mv`, still commit the change:

```bash
git status
git commit -m "Rename file"
```

For rename workflows with related reference updates, use:

```bash
git add -A
git diff --cached --summary
git diff --cached --name-status --find-renames
```

---

## `git pull`

### What it does

Fetches remote changes and integrates them into the current branch.

### Common syntax

```bash
git pull
git pull origin main
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| None | No | If upstream tracking is configured, plain `git pull` is enough. |
| Remote and branch | Optional | Example: `origin main`. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--ff-only` | Only updates if the result can be a fast-forward. |
| `--rebase` | Replays local commits on top of the fetched branch. |
| `--no-rebase` | Uses merge behavior. |

### Notes

Run `git status` first if you have local changes.

---

## `git push`

### What it does

Sends local commits or tags to a remote repository.

### Common syntax

```bash
git push
git push -u origin main
git push origin v1.0.0
git push origin --delete branch-name
git push --force-with-lease
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| None | No, if upstream tracking is configured | Pushes current branch to its upstream. |
| Remote and branch/tag | Required in many first-time or explicit pushes | Example: `origin main` or `origin v1.0.0`. |

### Optional parameters

| Option | Meaning |
|---|---|
| `-u` or `--set-upstream` | Sets upstream tracking for future plain `git push` and `git pull`. |
| `--follow-tags` | Pushes annotated tags reachable from pushed commits. |
| `--tags` | Pushes all tags. Use carefully. |
| `--delete branch-name` | Deletes a branch on the remote. |
| `--force-with-lease` | Safer force-push; useful after rebasing a private branch. Use carefully. |

### Notes

Plain `git push` does not necessarily push new tags. Push version tags explicitly:

```bash
git push origin v1.0.0
```

Use `--force-with-lease` only when you intentionally rewrote history and it is safe to update the remote branch.

---

## `git rebase`

### What it does

Replays commits onto a new base commit.

### Common syntax

```bash
git switch branch-name
git fetch origin
git rebase origin/main
git rebase -i <bad-commit-sha>~1
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Upstream/base | Usually | The branch or commit to replay your commits onto. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--continue` | Continues after conflicts are resolved. |
| `--abort` | Aborts the rebase. |
| `--skip` | Skips the current patch. |
| `-i` | Interactive rebase. Advanced. |
| `--root` | Rebase from the root commit. Useful only for special history edits. |

### Notes

Rebase rewrites commit IDs. Avoid rebasing shared branches unless everyone agrees.

To fix an older commit message during interactive rebase, change `pick` to `reword` for that commit.

---

## `git remote`

### What it does

Manages named remote repository connections.

### Common syntax

```bash
git remote -v
git remote add origin https://github.com/OWNER/REPO.git
git remote set-url origin https://github.com/OWNER/REPO.git
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Remote name | Required for add/set-url/remove | Commonly `origin`. |
| Remote URL | Required for add/set-url | GitHub or other Git remote URL. |

### Optional parameters

| Option or subcommand | Meaning |
|---|---|
| `-v` | Shows remote names and URLs. |
| `add name url` | Adds a remote. |
| `set-url name url` | Changes a remote URL. |
| `remove name` | Removes a remote. |

### Notes

`origin` is a remote name, not a branch.

---

## `git reset`

### What it does

Moves the current branch or unstages changes, depending on how it is used.

### Common syntax

```bash
git reset
git reset --hard HEAD
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| None | No | Plain `git reset` unstages staged changes. |
| Commit | Optional | Moves/reset to a specific commit, depending on mode. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--soft` | Moves HEAD but keeps changes staged. |
| `--mixed` | Default. Moves HEAD and unstages changes. |
| `--hard` | Discards working tree changes. Dangerous. |

### Notes

Be careful with:

```bash
git reset --hard
```

It can discard local work.

---

## `git restore`

### What it does

Restores files or unstages staged changes.

### Common syntax

```bash
git restore file-name.md
git restore --staged file-name.md
git restore --source v1.0.0 -- README.md
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Path | Usually | File or folder to restore/unstage. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--staged` | Unstages a file without changing working-tree content. |
| `--source commit-or-tag` | Restores from a specific commit, branch, or tag. |

### Notes

To undo an accidental staged deletion:

```bash
git restore --staged file-name.md
git restore file-name.md
```

---

## `git rm`

### What it does

Removes tracked files from Git and usually from the working tree.

### Common syntax

```bash
git rm file-name.md
git rm -r folder-name
git rm --cached file-name.md
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Path | Yes | File or folder to remove from tracking. |

### Optional parameters

| Option | Meaning |
|---|---|
| `-r` | Recursively removes a tracked folder. |
| `--cached` | Stops tracking the file but keeps it locally. |
| `-f` | Forces removal. Use carefully. |

### Notes

Use `git rm --cached` when a file should remain on disk but should no longer be tracked.

---

## `git show`

### What it does

Shows details about a commit, tag, or object.

### Common syntax

```bash
git show
git show HEAD
git show v1.0.0
git show --stat --oneline HEAD
git show --no-patch --format=fuller HEAD
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Object, commit, or tag | Optional | If omitted, Git shows `HEAD`. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--stat` | Shows file-change statistics. |
| `--oneline` | Condenses commit display. |
| `--name-only` | Shows names of changed files. |
| `--name-status` | Shows names and status codes for changed files. |
| `--no-patch` | Shows metadata/message without a patch. |
| `--format=fuller` | Shows fuller commit metadata. |

### Notes

Useful for inspecting tags:

```bash
git show v1.0.0
```

---

## `git status`

### What it does

Shows the current repository state.

### Common syntax

```bash
git status
git status --short
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| None | No | Shows status for the current repository. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--short` | Shows compact two-column status. |
| `--branch` | Shows branch and tracking information. |

### Notes

Use this constantly:

```bash
git status
```

Especially before and after:

```bash
git add
git commit
git push
```

---

## `git switch`

### What it does

Switches branches or creates and switches to a new branch.

### Common syntax

```bash
git switch main
git switch -c new-branch-name
git switch --detach v1.0.0
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Branch name | Required when switching branches | The branch to switch to. |

### Optional parameters

| Option | Meaning |
|---|---|
| `-c branch-name` | Creates and switches to a new branch. |
| `--detach commit-or-tag` | Checks out a commit or tag without creating a branch. |

### Notes

Use `git switch` instead of older `git checkout` for clearer branch switching.

---

## `git tag`

### What it does

Lists, creates, deletes, or inspects tags.

### Common syntax

```bash
git tag --list
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

### Required parameters

| Parameter | Required? | Meaning |
|---|---:|---|
| Tag name | Required when creating or deleting | Example: `v1.0.0`. |
| Tag message | Required for annotated tag with `-a` when using `-m` | Example: `"Version 1.0.0"`. |

### Optional parameters

| Option | Meaning |
|---|---|
| `--list` | Lists tags. |
| `-a` | Creates an annotated tag. |
| `-m "message"` | Supplies the annotated tag message. |
| `-d tag-name` | Deletes a local tag. |
| `-n` | Shows tag annotations. |

### Notes

For meaningful versions, prefer annotated tags:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

---

---

# `.gitattributes` quick reference

`.gitattributes` is not a Git command. It is a repository file that tells Git how to treat matching paths.

Common line-ending starter rules:

```gitattributes
* text=auto
*.md   text eol=crlf
*.html text eol=crlf
*.css  text eol=crlf
*.js   text eol=crlf
*.ps1  text eol=crlf
*.sh   text eol=lf
*.png  binary
*.jpg  binary
*.gif  binary
*.webp binary
```

Use:

```powershell
git ls-files --eol
```

to inspect the result.


# Common placeholder meanings

| Placeholder | Meaning | Example |
|---|---|---|
| `OWNER` | GitHub username or organization | `octocat` |
| `REPO` | Repository name | `hello-world` |
| `origin` | Conventional remote name | `origin` |
| `main` | Common primary branch name | `main` |
| `branch-name` | Any branch name | `update-guide` |
| `file-name.md` | File path | `README.md` |
| `old-name.md` | Old file path before rename | `old-guide.md` |
| `new-name.md` | New file path after rename | `new-guide.md` |
| `old-tag` | Earlier version tag | `v1.0.0` |
| `new-tag` | Later version tag | `v1.1.0` |
| `HEAD` | Current checked-out commit | `HEAD` |
| `HEAD~1` | Parent of current commit | `HEAD~1` |
| `bad-commit-sha` | Commit whose message needs correction | `a1b2c3d` |
| `vX.Y.Z` | Version tag placeholder | `v1.12.0` |
| `RELEASES.md` | Optional production-release documentation file | `RELEASES.md` |
| `IMPORT-NOTES.md` | Optional historical reconstruction notes file | `IMPORT-NOTES.md` |

---

# Common status codes

Used by commands such as:

```bash
git status --short
git diff --name-status
```

| Code | Meaning |
|---|---|
| `A` | Added |
| `M` | Modified |
| `D` | Deleted |
| `R` | Renamed |
| `C` | Copied |
| `??` | Untracked file |

---

# Quick decision table

| Goal | Command to start with |
|---|---|
| See what changed | `git status` |
| Stage everything intentionally | `git add -A` |
| Stage current-folder changes | `git add .` |
| Save staged changes | `git commit -m "Message"` |
| Push current branch | `git push` |
| Push first branch and set upstream | `git push -u origin main` |
| Push a version tag | `git push origin vX.Y.Z` |
| Compare version tags | `git diff --name-status old-tag..new-tag` |
| List files in a tag | `git ls-tree -r --name-only tag-name` |
| Rename a tracked file | `git mv old-name.md new-name.md` |
| Inspect line endings | `git ls-files --eol` |
| Verify remote tag | `git ls-remote --tags origin vX.Y.Z` |
| Save commit pointed to by a tag | `git rev-list -n 1 vX.Y.Z` |
| Search commit messages for typo | `git log --all --grep="TYPO" --oneline` |
| Fix latest commit message | `git commit --amend -m "Corrected message"` |
| Need a commit-message prefix | Choose based on change type: `docs`, `fix`, `feat`, `chore`, `style`, or `refactor` |
| Fix older commit message | `git rebase -i <bad-commit-sha>~1`, then `reword` |
| Push rewritten private branch | `git push --force-with-lease` |
| Restore accidental file deletion | `git restore file-name.md` |
| Unstage a file | `git restore --staged file-name.md` |
| View history | `git log --oneline --decorate --graph --all` |
