# Git Repository Cheat Sheet

**Version:** v1.22.0
**Full guide:** [`git-repository-guide.md`](git-repository-guide.md)
**Quick-start guide:** [`git-repository-guide-quick-start-guide.md`](git-repository-guide-quick-start-guide.md)
**Command quick reference:** [`git-command-quick-reference.md`](git-command-quick-reference.md)

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

For explanations, use the quick-start or full guide. For command syntax and parameter details, use [`git-command-quick-reference.md`](git-command-quick-reference.md).

---

## Minimum prerequisites

- Git installed.
- GitHub account.
- Local folder of files.
- No secrets or sensitive files staged.
- Repository name chosen.
- Version number chosen, such as `v1.0.0`.

---

## Global setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --show-origin --show-scope --list
```

Use `.gitattributes` as shared repository policy. Inspect `core.autocrlf`; do not treat it as a substitute.

## First-time setup

```bash
cd "C:\Path\To\Your\Project"
git init -b main
git status
git add -A
git diff --cached --check
git diff --cached --stat
git diff --cached
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
git show --stat v1.0.0
git push origin v1.0.0
```

---

## Later update with a new version tag

```bash
git status
git add -A
git diff --cached --check
git diff --cached --stat
git diff --cached
git commit -m "Create version v1.1.0"

git tag -a v1.1.0 -m "Version 1.1.0"
git show --stat v1.1.0

# Use one branch-push form:
git push
# or:
git push origin main

git push origin v1.1.0
```

Use one branch-push form, not both every time. Both are shown to make the choice visible.

---

## Later update without a new version tag

```bash
git status
git add .
git status
git commit -m "Describe what changed"

# Normal later push after upstream is configured:
git push

# Explicit branch push:
git push origin main
```

Use one branch-push form, not both every time.

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

### Clean release archive from a tag

```bash
git archive --format=zip --output aws-hello-world-microservice-v1.1.1.zip v1.1.1
git archive --format=zip --prefix=aws-hello-world-microservice-v1.1.1/ --output aws-hello-world-microservice-v1.1.1.zip v1.1.1
```

Use only one archive command. The second form adds a top-level folder.

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


---

---

## Commit-message prefixes

Pattern:

```text
type: short imperative summary
```

Common choices:

| Prefix | Use when |
|---|---|
| `feat` | user-visible content/capability added or expanded |
| `fix` | wrong, broken, stale, misleading, or misplaced item corrected |
| `docs` | documentation-only change |
| `chore` | routine maintenance or release prep |
| `style` | formatting-only change |
| `refactor` | internal restructure without intended behavior change |

Examples:

```bash
git commit -m "docs: document commit message prefixes"
git commit -m "fix: correct canonical domain"
git commit -m "feat: add web applications section"
git commit -m "chore: prepare v2.1.0 release"
```


---

---

---

---

---

---

## GitHub Releases

| Goal | Command / reminder |
|---|---|
| Create annotated tag | `git tag -a vX.Y.Z -m "Version X.Y.Z"` |
| Push one tag | `git push origin vX.Y.Z` |
| Verify remote tag | `git ls-remote --tags origin vX.Y.Z` |
| Release memory aid | `Commit = record; Tag = name; Release = explain/distribute` |
| Recommended GitHub Release title | `vX.Y.Z` |
| Generated notes comparison | Check the Previous tag |
| Show ignored files | `git status --ignored` |
| Explain ignore rule | `git check-ignore -v path/to/file` |
| Stop tracking ignored file | `git rm --cached path/to/file` |
| Stop tracking ignored folder | `git rm -r --cached path/to/folder` |
| Force-add ignored file | `git add -f path/to/file` |


## `.gitignore` quick checks

Starter `.gitignore` patterns:

```gitignore
bin/
obj/
node_modules/
*.log
*.tmp
.env
.env.*
.DS_Store
Thumbs.db
*.user
```


## Staging, rename review, and wording

| Goal | Command / wording |
|---|---|
| See compact status | `git status --short` |
| See unstaged summary | `git diff --stat` |
| Stage all repo changes | `git add -A` |
| Stage current folder and below | `git add .` |
| Check staged quality | `git diff --cached --check` |
| See staged summary | `git diff --cached --stat` |
| See exact staged patch | `git diff --cached` |
| Check renames | `git status --short --renames` |
| Check staged rename status | `git diff --cached --name-status --find-renames` |
| Show repo root | `git rev-parse --show-toplevel` |
| Check `.gitattributes` | `Test-Path .\.gitattributes` |
| Create folder in PowerShell | `New-Item -ItemType Directory -Force ".\docs\reference"` |
| Preferred wording | `committed locally and pushed to origin` |
| Avoid wording | `checked into origin` |

Careful review sequence:

```bash
git status --short
git diff --stat
git add -A
git status --short --renames
git diff --cached --stat
git diff --cached --name-status --find-renames
```


## Multiline commit bodies

PowerShell:

```powershell
git commit -m "Subject" -m @'
Body paragraph.

- First item
- Second item
'@
```

Cross-shell message file:

```powershell
git commit -F commit-message.txt
```

## Upstream tracking

```powershell
# First explicit push and tracking setup
git push -u origin main

# Verify
git branch -vv
git rev-parse --abbrev-ref --symbolic-full-name "@{upstream}"

# Set separately
git branch --set-upstream-to=origin/main main

# Remove tracking only
git branch --unset-upstream
```

## Namespaced tags

```powershell
git check-ref-format "refs/tags/component/v1.0.0"
git tag -a component/v1.0.0 -m "Release Component v1.0.0"
git push origin component/v1.0.0
git tag --list "component/*" --sort=-version:refname
```

## Delete a tag locally and remotely

```powershell
git tag -d v1.0.0
git push origin --delete v1.0.0

git tag --list v1.0.0
git ls-remote --tags origin v1.0.0
git log --oneline --decorate -10
```

## Shared and local ignore rules

| Rule file | Scope | Committed? |
|---|---|---:|
| `.gitignore` | Shared project | Usually yes |
| `.git/info/exclude` | One clone | No |
| Global `core.excludesFile` | All repos for one user | No |

```powershell
git check-ignore -v path/to/file
git status --ignored
git ls-files --others --ignored --exclude-standard
```

## Consolidated defaults and verification

| Goal | Recommendation / command |
|---|---|
| Primary branch | `main` |
| Primary remote | `origin` |
| First pre-release snapshot | `v0.1.0` |
| First stable baseline | `v1.0.0` |
| Stable tag message | `Version X.Y.Z` |
| Pre-release tag message | `Pre-release X.Y.Z` |
| Push tags | One intentional tag at a time |
| Verify remotes | `git remote -v` |
| Verify branch tracking | `git branch -vv` |
| Verify tag | `git show --stat --oneline vX.Y.Z` |
| Verify remote tag | `git ls-remote --tags origin vX.Y.Z` |
| Inspect line endings | `git ls-files --eol` |
| Renormalize line endings | `git add --renormalize .` |
| Search tracked files | `git grep "search text"` |
| PowerShell search | `Get-ChildItem -Recurse -File \| Select-String -Pattern "search text"` |

Pre-release tag:

```bash
git tag -a v0.1.0 -m "Pre-release 0.1.0"
git push origin v0.1.0
```

Stable tag:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

Final verification:

```bash
git status
git remote -v
git branch -vv
git log --oneline --decorate -5
git show --stat --oneline vX.Y.Z
git ls-remote --tags origin vX.Y.Z
git ls-files --eol
```


## Rename repo, folder, project, or remote

| Scenario | Command / action |
|---|---|
| Rename local parent folder | Rename in File Explorer or `Rename-Item`; no commit if only parent folder changed |
| Rename tracked file/folder | `git mv old-path new-path` |
| Stage manual rename | `git add -A` |
| Verify rename | `git diff --cached --summary` |
| Rename GitHub repo | GitHub repo settings |
| Update local remote | `git remote set-url origin https://github.com/USERNAME/new-repo-name.git` |
| Search old names | `git grep "old-name"` |
| PowerShell search | `Get-ChildItem -Recurse -File \| Select-String -Pattern "old-name"` |

Tracked rename:

```bash
git mv old-path new-path
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
git commit -m "chore: rename project paths"
```

Remote update after GitHub repo rename:

```bash
git remote -v
git remote set-url origin https://github.com/USERNAME/new-repo-name.git
git remote -v
git fetch origin
```

Old-name cleanup:

```bash
git grep "old-name"
git add -A
git commit -m "docs: update renamed repository references"
git push origin main
```


## Related repo linking

| Goal | Recommendation |
|---|---|
| Link hub to examples | README table with full GitHub URLs |
| Link example to hub | README link back to hub |
| Link previous/next examples | Full GitHub cross-repo links |
| Link files inside same repo | Relative links such as `CHANGELOG.md` |
| Link separate repos | Absolute GitHub URLs |
| Group related repos | Shared GitHub topic |
| Use submodules | Usually avoid for beginner examples |
| Use subtree | Usually avoid for beginner examples |

Good same-repo link:

```markdown
[Changelog](CHANGELOG.md)
```

Good cross-repo link:

```markdown
[Series hub](https://github.com/YOUR-USERNAME/simple-website-examples)
```

Avoid as final separate-repo link:

```markdown
[Example 02](../simple-website-example-02-basic-site-files/)
```


## GitHub file search and history lookup

| Goal | Shortcut or command |
|---|---|
| Search current GitHub file | `Ctrl+F` / `Cmd+F` |
| Open GitHub web editor | `.` |
| Search a path on GitHub | `keyword path:git-repository-guide.md` |
| List tags newest-first | `git tag --sort=-v:refname` |
| Show tagged commits | `git log --tags --simplify-by-decoration --oneline` |
| Inspect tag | `git show v1.0.0` |
| Nearest reachable tag | `git describe --tags` |
| Show tag refs and hashes | `git show-ref --tags` |
| Show commit messages | `git log --oneline` |
| All-ref graph | `git log --all --graph --decorate --oneline` |
| Oldest-first complete messages | `git log --all --reverse --format="%H%n%B%n"` |
| Search commit messages | `git log --all --grep="keyword" --oneline` |
| Inspect one commit | `git show --stat --summary <commit-hash>` |
| Show file statuses | `git show --name-status --find-renames --format= <commit-hash>` |
| Show complete snapshot paths | `git ls-tree -r --name-only <commit-hash>` |
| Exit pager | `q` |


## Release-tag timing

```powershell
git commit -m "Release version X.Y.Z"
git tag -a vX.Y.Z -m "Version X.Y.Z"
git show --stat vX.Y.Z
git push origin main
git push origin vX.Y.Z
```

Create and inspect the tag while `HEAD` still identifies the intended release commit. If tagging later, specify the older commit hash explicitly.

## Repository-health check

```powershell
Test-Path .git
git rev-parse --is-inside-work-tree
git rev-parse --show-toplevel
git rev-parse --git-dir
git status
git branch -vv
git remote -v
git show-ref --heads --tags
git fsck --full
git fetch origin --prune
git rev-parse main
git rev-parse origin/main
git status -sb
```

VS Code can initialize a new repository, but it cannot silently reconstruct deleted commits, tags, remotes, and upstream tracking.

## Count one commit's file statuses

```powershell
$statuses = @(git diff-tree --root --no-commit-id --name-status --find-renames -r HEAD)
"Added: $(@($statuses | Where-Object { $_ -match '^A\s' }).Count) | Modified: $(@($statuses | Where-Object { $_ -match '^M\s' }).Count) | Deleted: $(@($statuses | Where-Object { $_ -match '^D\s' }).Count) | Renamed: $(@($statuses | Where-Object { $_ -match '^R\d*\s' }).Count)"
```

## Commit-message typo fixes

### Search commit messages

```bash
git log --all --grep="Ve0sion" --oneline
git log --all --regexp-ignore-case --grep="ve0sion" --oneline
```

### Fix latest unpushed commit message

```bash
git commit --amend -m "Corrected commit message"
```

### Fix older unpushed commit message

```bash
git rebase -i <bad-commit-sha>~1
```

Change `pick` to `reword`.

### Push rewritten private branch

```bash
git push --force-with-lease
```

### Abort rebase

```bash
git rebase --abort
```


---

## Explicit push and repo hygiene

### Push branch and one tag

```powershell
git push origin main
git push origin vX.Y.Z
```

### Release checklist

```powershell
git status
git add -A
git status
git commit -m "docs: update guide"
git tag -a vX.Y.Z -m "Version X.Y.Z"
git show --stat vX.Y.Z
git push origin main
git push origin vX.Y.Z
```

### Verify branch state

```powershell
git branch -vv
git log --oneline origin/main..main
git log --oneline main..origin/main
```

### Useful hygiene files

| File | Purpose |
|---|---|
| `.gitignore` | Ignore untracked local/generated files |
| `.gitattributes` | Control text/binary and line-ending behavior |
| `.gitkeep` | Preserve intentionally empty folders |

### Suggested folders

```text
docs/
assets/
scripts/
.github/
archive/
```


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
| Need to check unpushed commits | `git log --oneline origin/main..main` |
| Need to search commit messages | `git log --all --grep="TYPO" --oneline` |
| Need to fix latest commit message | `git commit --amend -m "Corrected message"` |
| Need a commit prefix | Use `docs`, `fix`, `feat`, `chore`, `style`, or `refactor` based on the change type |

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
