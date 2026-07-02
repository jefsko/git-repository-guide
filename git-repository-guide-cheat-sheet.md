# Git Repository Cheat Sheet

**Version:** v1.10.0  
**Full guide:** [`git-repository-guide-v1.10.0.md`](git-repository-guide-v1.10.0.md)  
**Quick-start guide:** [`git-repository-guide-quick-start-guide-v1.10.0.md`](git-repository-guide-quick-start-guide-v1.10.0.md)  
**Command quick reference:** [`git-command-quick-reference-v1.10.0.md`](git-command-quick-reference-v1.10.0.md)

## Path

```text
create folder
git init
git add
git commit
create GitHub repo
git remote add origin
git push -u origin main
git tag -a
git push origin tag
repeat for later versions
```

## Use this when

Use this when you want a compact checklist for creating or updating a Git repository and marking file sets as versions with tags.

For explanations, use the quick-start or full guide. For command syntax and parameter details, use [`git-command-quick-reference-v1.10.0.md`](git-command-quick-reference-v1.10.0.md).

---

## Minimum prerequisites

- Git installed.
- GitHub account.
- Local folder of files.
- No secrets or sensitive files staged.
- Repository name chosen.
- Version number chosen, such as `v1.0.0`.

---

## First-time setup

```bash
cd "C:\Path\To\Your\Project"
git init -b main
git status
git add .
git status
git commit -m "Create version v1.0.0"
```

Create an empty GitHub repo, then connect it:

```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git remote -v
git push -u origin main
```

Create and push the first tag:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

---

## Later update with a new version tag

```bash
git status
git add .
git status
git commit -m "Create version v1.1.0"
git push

git tag -a v1.1.0 -m "Version 1.1.0"
git push origin v1.1.0
```

---

## Later update without a new version tag

```bash
git status
git add .
git status
git commit -m "Describe what changed"
git push
```

---

## Common file operations

### Add a file

```bash
git add notes.md
git commit -m "Add notes file"
git push
```

### Update a file

```bash
git add guide.md
git commit -m "Update guide"
git push
```

### Replace same-path file

```bash
git add guide.md
git commit -m "Replace guide with updated version"
git push
```

### Delete a tracked file

```bash
git rm old-file.md
git commit -m "Remove old file"
git push
```

### Move or rename a file

```bash
git mv old-name.md new-name.md
git commit -m "Rename file"
git push
```

---

## `git add .` rules

`git add .` stages changes under the current folder, including subfolders.

It can stage:

- new files;
- modified tracked files;
- deleted tracked files.

It does not need to stage unchanged tracked files again.

Always check:

```bash
git status
git add .
git status
```

---

## Do not share / avoid / warning

- Do not commit passwords, API keys, `.env` files, certificates, or personal data.
- Do not delete unchanged tracked files just to simplify `git add .`.
- Do not tag before committing; tags point to commits.
- Do not assume `git push` pushes tags; push tags explicitly.
- Do not move a published version tag unless you fully understand the consequences.
- Do not rely on a custom release asset ZIP to represent the whole repository unless you packaged it that way.

---

## Accident recovery

### Restore accidentally deleted tracked file

```bash
git restore file-name.md
```

### If deletion was already staged

```bash
git restore --staged file-name.md
git restore file-name.md
```

### Abort merge conflict attempt

```bash
git merge --abort
```

### Abort rebase conflict attempt

```bash
git rebase --abort
```

---

## Branch workflow

Create and push a working branch:

```bash
git switch main
git pull

git switch -c update-guide
git add .
git commit -m "Update guide"
git push -u origin update-guide
```

Merge later:

```bash
git switch main
git pull
git merge update-guide
git push
```

Tag after the final merged result is correct:

```bash
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

---

## Tag and download reminders

| Question | Answer |
|---|---|
| Does a tag apply only to changed files? | No. It points to a full commit snapshot. |
| Do unchanged tracked files appear in `git status`? | No, not unless something changed. |
| Are unchanged tracked files included in a tag? | Yes, if they are tracked at that commit. |
| Does GitHub source ZIP contain all tracked files at the tag? | Yes. |
| Does a custom release asset ZIP contain all tracked files? | Only if you manually put them there. |

---

## Compare, inspect, and export

### List tags

```bash
git tag --list
```

### Show a tag

```bash
git show v1.0.0
```

### Compare two tags

```bash
git diff v1.0.0..v1.1.0
git diff --name-only v1.0.0..v1.1.0
```


### Show files changed between tags

```bash
git diff --name-status v1.1.0..v1.1.1
```

### Show only added files

```bash
git diff --name-status --diff-filter=A v1.1.0..v1.1.1
```

### Show all files in a tag

```bash
git ls-tree -r --name-only v1.1.1
```

### GitHub.com Compare

```text
https://github.com/OWNER/REPO/compare/v1.1.0...v1.1.1
```

If branch/tag names are ambiguous:

```text
https://github.com/OWNER/REPO/compare/tags/v1.1.0...tags/v1.1.1
```

### Export a tag as ZIP

```bash
git archive --format=zip --output project-v1.0.0.zip v1.0.0
```

---

---

## Pull Request workflow

Create branch and push:

```bash
git switch main
git pull

git switch -c update-guide
git add .
git commit -m "Update guide"
git push -u origin update-guide
```

On GitHub:

1. Open Pull Request from `update-guide` into `main`.
2. Review the **Files changed** tab.
3. Address comments with follow-up commits.
4. Merge when ready.

After merge, tag from `main`:

```bash
git switch main
git pull
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

If the PR branch is out of date:

```bash
git switch update-guide
git fetch origin
git merge origin/main
git push
```


---

## Rename workflow

### Preferred tracked-file rename

```powershell
git mv old-name.md new-name.md
git add -A
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
git commit -m "Rename file"
```

### Manual PowerShell rename

```powershell
Rename-Item old-name.md new-name.md
git add -A
git diff --cached --summary
git diff --cached --name-status --find-renames
```

### Short PowerShell alias

```powershell
ren old-name.md new-name.md
git add -A
```

### View history after rename

```bash
git log --follow -- new-name.md
```

### Rename troubleshooting

| Problem | Fix |
|---|---|
| Rename shows as delete plus add | Try `git diff --cached --name-status --find-renames` |
| Rename still not detected | Accept delete/add or redo with `git mv` |
| File was heavily rewritten during rename | Consider two commits: rename first, rewrite second |
| Links still point to old filename | Search repo for old filename and update references |


---

## Historical import and tag repair

### Import a historical folder snapshot

```powershell
git status
git add -A
git status
git commit -m "message for that version"
```

### Tag a production release

```powershell
git tag -a vX.Y.Z -m "Release vX.Y.Z: short release summary. Original production publish: YYYY-MM-DD."
git push origin vX.Y.Z
```

### Tag an older commit

```powershell
git log --oneline
git tag -a vX.Y.Z <commit-sha> -m "Version X.Y.Z"
```

### Fix a local unpushed tag

```powershell
git tag -d vX.Y.Z
git tag -a vX.Y.Z -m "Version X.Y.Z"
```

### Fix an older pushed tag safely

```powershell
$commit = git rev-list -n 1 vX.Y.Z
git push origin --delete vX.Y.Z
git tag -d vX.Y.Z
git tag -a vX.Y.Z $commit -m "Version X.Y.Z"
git push origin vX.Y.Z
```

### Verify tags

```powershell
git show vX.Y.Z
git tag -n99 vX.Y.Z
git ls-remote --tags origin vX.Y.Z
```

---

## Line endings

### Add basic `.gitattributes`

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

### Inspect line endings

```powershell
git ls-files --eol
```


---

## Release notes and import docs

### Release-note structure

```markdown
## Summary

## Production Publish Date

YYYY-MM-DD

## Highlights

- Important change 1.
- Important change 2.

## Notes

- Historical import notes.
- Domain or deployment notes.
```

### Useful documentation files

| File | Purpose |
|---|---|
| `README.md` | Project overview and canonical URL |
| `CHANGELOG.md` | Notable changes by version |
| `RELEASES.md` | Production publish dates and release summaries |
| `IMPORT-NOTES.md` | Historical reconstruction notes |


## Common fixes

| Problem | Fix |
|---|---|
| Forgot to push tag | `git push origin vX.Y.Z` |
| Staged wrong file | `git restore --staged file-name` |
| Accidentally deleted tracked file | `git restore file-name` |
| Push rejected | `git pull`, resolve issues, then `git push` |
| Need to see what is staged | `git diff --cached --stat` |
| Need to see tracked files | `git ls-tree -r --name-only HEAD` |
| Need to see latest commit stats | `git show --stat --oneline HEAD` |
| Need to verify a rename | `git diff --cached --summary` and `git diff --cached --name-status --find-renames` |
| Need to inspect line endings | `git ls-files --eol` |

---

## Good commit-message patterns

One-line commit:

```bash
git commit -m "Add quick-start guide"
```

Commit with body:

```bash
git commit -m "Add quick-start guide" -m "Add a concise setup path for creating a Git repository, pushing to GitHub, and tagging versioned file sets."
```

Rule of thumb:

```text
summary = what changed
body = why it changed or what future readers should know
```
