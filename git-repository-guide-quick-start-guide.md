# Git Repository Quick-Start Guide

**Version:** v1.16.0  
**Based on full guide:** [`git-repository-guide.md`](git-repository-guide.md)  
**Recommended path:** Create a Git repository, commit your files, push to GitHub, tag a version, and repeat for later versions.  
**Best for:** Creating a versioned documentation or project repository where each version tag identifies a full file-set snapshot.

This is the short, practical version of the full Git Repository Guide. It focuses on the common successful path: create a local repo, connect it to GitHub, commit files, create annotated tags, and understand what is included when you download a tagged version.

Use the full guide when you need deeper explanation, conflict handling, branch workflows, file/folder edge cases, or detailed troubleshooting. Use the command quick reference when you want command syntax and parameter details: [`git-command-quick-reference.md`](git-command-quick-reference.md).

---

## Before you start

You need:

- Git installed.
- A GitHub account.
- A local project folder with files you want to track.
- Permission to create or push to a GitHub repository.
- A decision about your repository name.

Recommended repository name:

```text
git-repository-guide
```

Recommended GitHub description:

```text
A beginner-friendly guide to creating Git repositories and managing versioned file sets
```

For a real repository, keep stable filenames:

```text
README.md
CHANGELOG.md
git-repository-guide.md
```

Standalone downloads may include version numbers, but the active files inside the repo should usually keep stable names.

---

## What this builds

```text
local project folder
        |
        v
local Git repository
        |
        v
GitHub repository named origin
        |
        v
commits on main
        |
        v
annotated version tags such as v1.0.0, v1.1.0, v1.16.0
```

End result:

- Your files are tracked in Git.
- GitHub has a copy of the repository.
- Each meaningful version is marked with an annotated tag.
- A tag download contains the tracked repository snapshot at that tag.

---

## Safety and cleanup notes

Before committing, check that you are not about to commit:

- passwords;
- API keys;
- `.env` files;
- private certificates;
- personal data;
- build output;
- temporary files.

Create or update `.gitignore` before the first commit if needed.

Example:

```gitignore
bin/
obj/
.vs/
node_modules/
.env
*.user
*.log
```

Be careful with `git add .`. It stages new files, modified files, and deleted tracked files under the current folder. Always run `git status` before and after staging.

---

## Quick-start steps

### 1. Open your project folder

In PowerShell:

```powershell
cd "C:\Path\To\Your\Project"
dir
```

**Checkpoint:** You should see the files you want to track.

---

### 2. Initialize the local Git repository

Preferred:

```bash
git init -b main
```

If your Git version does not support `-b main`, use:

```bash
git init
git branch -M main
```

Check status:

```bash
git status
```

**Checkpoint:** Git should report that you are on branch `main` and show files as untracked.

---

### 3. Stage and commit the first file set

Stage files:

```bash
git add .
```

Check what is staged:

```bash
git status
```

Commit:

```bash
git commit -m "Create version v1.0.0"
```

**Checkpoint:** Git should create a commit. This commit is the saved snapshot you will tag next.

---

### 4. Create the GitHub repository

On GitHub:

1. Create a new repository.
2. Use your chosen repository name.
3. Choose Public or Private.
4. Do not initialize with README, `.gitignore`, or license if those files already exist locally.
5. Copy the repository URL.

Connect your local repo to GitHub:

```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git remote -v
```

Push the main branch and set upstream tracking:

```bash
git push -u origin main
```

**Checkpoint:** Your files should appear in the GitHub repository.

---

### 5. Create and push the first version tag

Create an annotated tag:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

Push the tag:

```bash
git push origin v1.0.0
```

Verify local tags:

```bash
git tag --list
```

Inspect the tag:

```bash
git show v1.0.0
```

**Checkpoint:** GitHub should show a `v1.0.0` tag.

---

### 6. Make the next update

Edit or add files normally.

Check what changed:

```bash
git status
```

Stage the intended changes:

```bash
git add .
```

Check again:

```bash
git status
```

Commit:

```bash
git commit -m "Create version v1.1.0"
```

Push the commit. After upstream tracking is configured, plain `git push` usually works:

```bash
git push
```

For careful versioned updates, the explicit form is clearer:

```bash
git push origin main
```

Use one of those branch-push forms, not both every time.

Create and push the next tag:

```bash
git tag -a v1.1.0 -m "Version 1.1.0"
git push origin v1.1.0
```

**Checkpoint:** GitHub should now have the new commit and the new tag.

---

### 7. Understand what a tag contains

A tag points to a commit.

A commit represents the full tracked repository snapshot at that point.

That means a tag is not limited to the files changed in that commit.

Example:

```text
4 files were already tracked
2 files were modified
4 new files were added
0 tracked files were deleted
```

The new tag identifies a snapshot with:

```text
8 tracked files
```

not only the 6 files that changed.

---

### 8. Download or export a version

GitHub's automatic source download for a tag contains the tracked repository snapshot at that tag.

You can also export a version locally:

```bash
git archive --format=zip --output project-v1.0.0.zip v1.0.0
```

**Checkpoint:** The ZIP should contain the tracked files at that tag.

A custom GitHub Release asset ZIP is different. It contains whatever files you manually put into that ZIP.

---

---

---

---

## Rename repositories, folders, and remotes

Use this distinction:

| Rename type | Needs Git commit? | Typical action |
|---|---:|---|
| Local parent folder containing `.git/` | No | Rename in File Explorer or PowerShell |
| Tracked file/folder inside repo | Yes | `git mv` or rename plus `git add -A` |
| GitHub repository name | No, not by itself | Rename in GitHub settings |
| Local remote URL after GitHub rename | No commit | `git remote set-url origin ...` |
| Project/app name inside files | Yes | Search, edit files, commit |

Tracked rename:

```bash
git mv old-path new-path
git status
git commit -m "chore: rename project paths"
```

Update local remote after a GitHub repo rename:

```bash
git remote -v
git remote set-url origin https://github.com/USERNAME/new-repo-name.git
git remote -v
git fetch origin
```

Search for old names:

```bash
git grep "old-name"
```


## Link related repositories

For a hub-and-example series, such as a set of simple website examples, keep each repository independent and connect them through README links and GitHub metadata.

Recommended ranking:

| Rank | Method | Recommendation |
|---:|---|---|
| 1 | README links | Strongly recommended |
| 2 | GitHub topics | Strongly recommended |
| 3 | GitHub About / website links | Recommended |
| 4 | Tags and releases | Recommended |
| 5 | Git submodules | Usually not recommended |
| 6 | Git subtree | Usually not recommended |

Use same-repo relative links for files inside the same repository:

```markdown
[Changelog](CHANGELOG.md)
```

Use full GitHub URLs for links to separate repositories:

```markdown
[Series hub](https://github.com/YOUR-USERNAME/simple-website-examples)
[Example 02](https://github.com/YOUR-USERNAME/simple-website-example-02-basic-site-files)
```

Avoid sibling-folder links as the final form for separate GitHub repos:

```markdown
[Example 02](../simple-website-example-02-basic-site-files/)
```

Use Git CLI for exact push, tag, and release commands even when reviewing files in VS Code or Visual Studio.


## Inspect tags and commit messages

List tags newest-first by version:

```bash
git tag --sort=-v:refname
```

Show a compact graph with branches and tags:

```bash
git log --oneline --decorate --graph --all
```

Show only tagged or decorated commits:

```bash
git log --tags --simplify-by-decoration --oneline
```

Search commit messages:

```bash
git log --all --grep="keyword" --oneline
```

Show commit messages only:

```bash
git log --format=%B
```

Find the nearest reachable tag from the current commit:

```bash
git describe --tags
```

Press `q` to exit the Git pager.

When viewing a file on GitHub, use `Ctrl+F` on Windows/Linux or `Cmd+F` on Mac to search inside that file. Press `.` on GitHub to open the web editor if you want an editor-like view.


## Stop here if your goal is only a quick test

If your only goal was to test Git versioning, stop after:

```text
commit
push
tag
push tag
verify tag exists
```

Then decide whether to keep or delete the test GitHub repository.

If the repository contains anything sensitive, remove the sensitive data from the repository history or delete the test repository before sharing it.

---

## Common later workflows

### Add a new file

```bash
git status
git add notes.md
git status
git commit -m "Add notes file"
git push
```

### Update an existing file

```bash
git status
git add guide.md
git status
git commit -m "Update guide"
git push
```

### Replace an existing file with a newer local copy

```bash
git status
git add guide.md
git status
git commit -m "Replace guide with updated version"
git push
```

### Delete a tracked file intentionally

```bash
git status
git rm old-notes.md
git status
git commit -m "Remove old notes file"
git push
```

### Restore an accidentally deleted tracked file

If not staged:

```bash
git restore file-name.md
```

If already staged:

```bash
git restore --staged file-name.md
git restore file-name.md
```

### Use a working branch for safer work

```bash
git switch main
git pull

git switch -c update-guide
git status
git add .
git status
git commit -m "Update guide"
git push -u origin update-guide
```

Then open a Pull Request or merge the branch later.

Tag versions from `main` after the final merged result is correct.

---

---

## Compare two versions

To see which files changed between two tags:

```bash
git diff --name-status v1.1.0..v1.1.1
```

To see only added files:

```bash
git diff --name-status --diff-filter=A v1.1.0..v1.1.1
```

To see all files contained in one tag:

```bash
git ls-tree -r --name-only v1.1.1
```

On GitHub.com, open the repository and add `/compare` to the end of the repository URL. Then set the earlier tag as the base and the newer tag as the compare target.

Example:

```text
base: v1.1.0
compare: v1.1.1
```

---

## Use a Pull Request for reviewed changes

For larger or reviewed changes, use a working branch and Pull Request instead of committing directly to `main`.

```bash
git switch main
git pull

git switch -c update-guide
git status
git add .
git status
git commit -m "Update guide"
git push -u origin update-guide
```

Then on GitHub:

1. Open the repository.
2. Click **Compare & pull request**, or go to **Pull requests** > **New pull request**.
3. Set `main` as the base branch.
4. Set your working branch as the compare branch.
5. Review the diff.
6. Create the Pull Request.
7. Review, update, and merge when ready.

After the Pull Request is merged, tag from `main`:

```bash
git switch main
git pull
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```


---

## Rename a tracked file

Use this when a tracked file has the wrong or confusing name.

Preferred workflow:

```powershell
git mv old-name.md new-name.md
```

Then update any Markdown links or references that mention the old filename.

Stage and verify:

```powershell
git add -A
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
```

Commit:

```powershell
git commit -m "Rename guide file"
```

If this rename is part of a versioned documentation update, tag after the final commit:

```powershell
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

If you already deleted the old file and copied in the renamed file manually, try this first:

```powershell
git add -A
git diff --cached --summary
git diff --cached --name-status --find-renames
```

If Git detects a rename, you can usually continue. If it still shows delete plus add and you care about clean rename display, redo the rename with `git mv`.


---

## Import historical version folders

Use this when you have old backup folders such as `v0.1.0`, `v0.1.1`, and `v1.0.0` and want to reconstruct Git history.

Basic pattern:

```powershell
# Copy one historical version folder's contents into the repo first.
git status
git add -A
git status
git commit -m "message for that version"
```

Repeat for each version folder in order.

Use annotated tags for production releases only:

```powershell
git tag -a v1.0.0 -m "Release v1.0.0: initial production publish. Original production publish: 2026-03-17."
```

If you forget to tag before the next commit, find the old commit and tag it directly:

```powershell
git log --oneline
git tag -a v1.0.0 <commit-sha> -m "Release v1.0.0: initial production publish. Original production publish: 2026-03-17."
```

---

## Fix a tag message mistake

If the tag has not been pushed:

```powershell
git tag -d vX.Y.Z
git tag -a vX.Y.Z -m "Version X.Y.Z"
```

If an older pushed tag needs to be recreated without moving it to the latest commit:

```powershell
$commit = git rev-list -n 1 vX.Y.Z
git push origin --delete vX.Y.Z
git tag -d vX.Y.Z
git tag -a vX.Y.Z $commit -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Verify:

```powershell
git show vX.Y.Z
git tag -n99 vX.Y.Z
git ls-remote --tags origin vX.Y.Z
```

---

## Add line-ending rules

Before the first commit of a new Windows-managed website or documentation repo, add `.gitattributes`.

Minimal starter idea:

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

Inspect line endings:

```powershell
git ls-files --eol
```


---

## Document release identity

For a reconstructed website repository, document these clearly:

```text
Repository name
Canonical URL
Optional alias
Site heading
Browser title
Production release tags
```

Example:

```text
Repository name: demo-jeffskone-com
Canonical URL: https://demo.jeffskone.com
Optional alias: https://portfolio.jeffskone.com
Site heading: Jeff Skone's AWS Portfolio
Browser title: Jeff Skone's AWS Portfolio | AWS Demos
```

Recommended release-note sections:

```markdown
## Summary

## Production Publish Date

## Highlights

## Notes
```

For reconstructed projects, consider adding:

```text
RELEASES.md
IMPORT-NOTES.md
```

Use `RELEASES.md` for production release summaries and `IMPORT-NOTES.md` to explain how historical backup folders were reconstructed into Git history.


---

---

## Choose a commit-message prefix

Commit prefixes are not Git commands. They are a convention for making history easier to scan.

Use this pattern:

```text
type: short imperative summary
```

Common choices:

| Prefix | Use when |
|---|---|
| `feat` | user-visible content, capability, page, endpoint, or section is added or expanded |
| `fix` | something wrong, broken, stale, misleading, or misplaced is corrected |
| `docs` | documentation-only files change |
| `chore` | routine maintenance, release prep, metadata refresh, or housekeeping |
| `style` | formatting, whitespace, table formatting, or line-ending-only changes |
| `refactor` | internal structure changes without intended visible behavior change |

Examples:

```bash
git commit -m "docs: document commit message prefixes"
git commit -m "fix: correct canonical domain"
git commit -m "feat: add web applications section"
git commit -m "chore: prepare v2.1.0 release"
```

Commit prefixes belong in commit messages, not tag names. Keep tag names clean, such as `v1.16.0`, and tag messages simple, such as `Version 1.12.0`.


## Fix commit-message typos

Search commit messages:

```bash
git log --all --grep="Ve0sion" --oneline
git log --all --regexp-ignore-case --grep="ve0sion" --oneline
```

Fix the latest unpushed commit message:

```bash
git log -1 --oneline
git commit --amend -m "Corrected commit message"
git log -1 --oneline
```

Fix an older unpushed commit message:

```bash
git log --oneline
git rebase -i <bad-commit-sha>~1
```

In the editor, change `pick` to `reword` for the bad commit.

If rewritten history was already pushed and it is safe to rewrite that branch:

```bash
git push --force-with-lease
```

Do not rewrite shared, protected, tagged, released, or deployed history just to fix a minor typo unless you fully understand the consequences.


---

## Push branch and tag explicitly

For careful versioned guide or website work, push the branch and the tag explicitly.

```powershell
git status
git add -A
git status
git commit -m "docs: update guide"
git push origin main

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Plain `git push` may be enough when the current branch is already tracking an upstream branch, but `git push origin main` is clearer.

Check tracking and unpushed commits:

```powershell
git status
git branch -vv
git log --oneline origin/main..main
git log --oneline main..origin/main
```

Use a working branch for larger changes:

```powershell
git switch main
git pull
git switch -c update-guide
```

Use `main` directly only when that is appropriate for your repo and risk level.


## If something fails

| Problem | Most likely fix |
|---|---|
| `git status` shows files you did not mean to include | Do not commit yet. Remove, restore, or ignore those files first. |
| `git add .` staged a deleted file | Use `git restore --staged file` and `git restore file` if the deletion was accidental. |
| `git push` says upstream is missing | Use `git push -u origin main` for first push, or `git push -u origin branch-name` for a new branch. |
| `git push` is rejected | Run `git pull`, resolve any issues, then push again. |
| Tag exists locally but not on GitHub | Run `git push origin vX.Y.Z`. |
| GitHub source ZIP has more files than expected | It contains the full tracked snapshot at the tag, not only changed files. |
| Custom release asset ZIP has different contents | That ZIP was manually packaged and may intentionally contain selected files only. |

---

## Where to read more

Use the full guide when you need:

- Git terms and deeper concepts;
- GitHub Releases vs. production deployments;
- Visual Studio Code Git workflows;
- README and CHANGELOG structure;
- branch, merge, rebase, and conflict guidance;
- file/folder move, rename, delete, and replace scenarios;
- commit message body examples;
- practical staging and tag download scenarios;
- comparing tags locally and on GitHub.com;
- Pull Request workflows;
- renaming tracked files with `git mv`;
- updating links after a file rename;
- historical version folder imports;
- tag correction workflows;
- LF/CRLF and `.gitattributes` guidance;
- release notes and import documentation;
- commit-message typo correction workflows;
- commit-message prefix selection;
- canonical URL and repository identity planning;
- command syntax and parameter meanings;
- explicit branch and tag push workflows;
- `.gitignore`, `.gitkeep`, repository folder, and GitHub topics basics;
- troubleshooting and reference commands.

Full guide: [`git-repository-guide.md`](git-repository-guide.md)

Command quick reference: [`git-command-quick-reference.md`](git-command-quick-reference.md)
