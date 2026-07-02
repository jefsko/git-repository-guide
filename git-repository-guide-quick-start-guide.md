# Git Repository Quick-Start Guide

**Version:** v1.8.0  
**Based on full guide:** [`git-repository-guide-v1.8.0.md`](git-repository-guide-v1.8.0.md)  
**Recommended path:** Create a Git repository, commit your files, push to GitHub, tag a version, and repeat for later versions.  
**Best for:** Creating a versioned documentation or project repository where each version tag identifies a full file-set snapshot.

This is the short, practical version of the full Git Repository Guide. It focuses on the common successful path: create a local repo, connect it to GitHub, commit files, create annotated tags, and understand what is included when you download a tagged version.

Use the full guide when you need deeper explanation, conflict handling, branch workflows, file/folder edge cases, or detailed troubleshooting. Use the command quick reference when you want command syntax and parameter details: [`git-command-quick-reference-v1.8.0.md`](git-command-quick-reference-v1.8.0.md).

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
annotated version tags such as v1.0.0, v1.1.0, v1.8.0
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

Push the commit:

```bash
git push
```

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
- command syntax and parameter meanings;
- troubleshooting and reference commands.

Full guide: [`git-repository-guide-v1.8.0.md`](git-repository-guide-v1.8.0.md)

Command quick reference: [`git-command-quick-reference-v1.8.0.md`](git-command-quick-reference-v1.8.0.md)
