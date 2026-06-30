# Creating a Git Repository and Marking File Sets as Versions

Document version: v1.1.0  
Previous locked version: v1.0.0  
Version status: Locked standalone Markdown version  
Update type: Additive update  
Versioning method: Document metadata only; no Git repository package required  
Future edit policy: Do not overwrite this `v1.1.0` file. Save future changes as a new version, such as `v1.1.1` or `v1.2.0`.  
Current as of: 2026-06-29

Revision note: This `v1.1.0` edition preserves the `v1.0.0` guide and additively incorporates supplemental Git tagging, repository naming, retrieval, and pager guidance from the uploaded reference file `git_tags_versioning_reference(1).md`.

---

## Table of Contents

- [1. Purpose of This Guide](#1-purpose-of-this-guide)
- [2. The Core Concept](#2-the-core-concept)
- [3. Proper Terms](#3-proper-terms)
- [4. Recommended Workflow](#4-recommended-workflow)
- [5. Create the Local Git Repository](#5-create-the-local-git-repository)
- [6. Create the GitHub Repository](#6-create-the-github-repository)
- [7. Mark the First File Set as v1.0.0](#7-mark-the-first-file-set-as-v100)
- [8. Continue Editing and Mark the Next File Set as v1.1.0](#8-continue-editing-and-mark-the-next-file-set-as-v110)
- [9. View, Compare, Export, or Restore a Version](#9-view-compare-export-or-restore-a-version)
- [10. Tags vs. Releases vs. Production Deployments](#10-tags-vs-releases-vs-production-deployments)
- [11. Using Visual Studio Code](#11-using-visual-studio-code)
- [12. Naming and Versioning Recommendations](#12-naming-and-versioning-recommendations)
- [13. Common Mistakes to Avoid](#13-common-mistakes-to-avoid)
- [14. Quick Command Cheat Sheet](#14-quick-command-cheat-sheet)
- [Appendix A: Expanded Git Command Reference](#appendix-a-expanded-git-command-reference)
- [Appendix B: Expanded VS Code Reference](#appendix-b-expanded-vs-code-reference)
- [Appendix C: Expanded Versioning Concepts](#appendix-c-expanded-versioning-concepts)
- [Appendix D: Production Release and Deployment Details](#appendix-d-production-release-and-deployment-details)
- [Appendix E: Troubleshooting](#appendix-e-troubleshooting)
- [Appendix F: Knowledge Base and How-To Reference](#appendix-f-knowledge-base-and-how-to-reference)
- [Appendix G: References](#appendix-g-references)
- [Index](#index)

---

## 1. Purpose of This Guide

You already have:

- Git installed.
- A GitHub account.
- A folder of files you want to track.
- A desire to mark one file set as `v1.0.0`, then later mark a newer file set as `v1.1.0`.

That is a normal Git workflow.

The main idea is:

> You commit the current tracked file set, then tag that commit.

In everyday language, you might say:

> “This is the `v1.0.0` file set.”

In more precise Git language, say:

> “This is the repository snapshot identified by the `v1.0.0` tag.”

Both are understandable. The second one is more technically correct.

Git documentation describes tags as a way to mark specific points in repository history, commonly for release points such as version numbers. [R1]

---

## 2. The Core Concept

Git does **not** directly tag a random folder, loose group of files, or unsaved edits.

Git tags a **commit**.

A commit represents the tracked state of the repository at that moment. So when you create a tag like `v1.0.0`, you are really saying:

> “The commit I am tagging represents version `v1.0.0`.”

That commit identifies the tracked project state. Later, when you create `v1.1.0`, you are tagging a newer commit that represents the newer tracked file set.

The flow is:

```bash
edit files
git status
git add .
git commit -m "Create version v1.0.0"
git tag -a v1.0.0 -m "Version 1.0.0"
```

Then later:

```bash
edit files
git status
git add .
git commit -m "Create version v1.1.0"
git tag -a v1.1.0 -m "Version 1.1.0"
```

Now Git can tell the difference between the two snapshots.

The key rule:

> A version tag only captures what has already been committed.

If a file is untracked, unstaged, modified but not committed, ignored by `.gitignore`, or not saved from your editor, it is not part of that tagged version.

---

## 3. Proper Terms

### Repository

A **repository**, or **repo**, is the Git-tracked project. It includes your files and Git’s history.

### Working Tree

The **working tree** is the project folder you are actively editing.

### Staging Area

The **staging area**, also called the index, is where you place changes before committing them.

When you run:

```bash
git add .
```

you are staging changes.

### Commit

A **commit** is a saved snapshot in Git history.

Git’s glossary describes a commit as a point in Git history and also as the action of storing a new snapshot of the project’s state. [R3]

### Tag

A **tag** is a named reference to a specific point in Git history.

For this guide, tags are how you mark versions:

```text
v1.0.0
v1.1.0
v1.4.2
v1.5.0
```

Git’s tagging guide describes this as marking important points in history. [R1]

### Annotated Tag

An **annotated tag** is a Git tag object with metadata, including the tagger, date, message, and optionally a cryptographic signature. Git’s `git-tag` documentation distinguishes annotated tags from lightweight tags and says annotated tags are created with options such as `-a`, `-s`, or `-u`. [R2]

For meaningful versions, use annotated tags:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

### Lightweight Tag

A **lightweight tag** is just a name pointing to an object, usually a commit. [R2]

Example:

```bash
git tag v1.0.0
```

Lightweight tags work, but they are not the recommended default for meaningful version markers. For versioned snapshots like `v1.0.0`, use annotated tags.

### Version

A **version** is the human-readable label you assign to a meaningful project state.

Examples:

```text
v1.0.0
v1.1.0
v1.4.2
```

Git does not decide what these numbers mean. You define that policy.

### Semantic Versioning

**Semantic Versioning**, or **SemVer**, is the common `MAJOR.MINOR.PATCH` format:

```text
1.4.2
```

Meaning:

```text
MAJOR.MINOR.PATCH
```

SemVer’s official specification says version numbers and how they change are meant to communicate meaning about what changed from one version to the next. [R14]

Many Git projects prefix version tags with `v`:

```text
v1.4.2
```

The `v` is a convention, not a Git requirement.

### GitHub Release

A **GitHub Release** is a GitHub object based on a Git tag. It can include release notes, source archives, and downloadable assets. GitHub’s documentation says releases are based on Git tags, and tags mark specific points in repository history. [R8]

### Production Deployment

A **production deployment** means a specific commit, branch, or tag was actually deployed to the production environment.

This is different from a tag.

A tag says:

> “This is version `v1.1.0`.”

A production deployment says:

> “Version `v1.1.0` is now running in production.”

GitHub Actions environments can represent deployment targets such as `production`, `staging`, or `development`. [R11]

---

## 4. Recommended Workflow

For your situation, use this rule:

> Commit every meaningful file set, then create an annotated tag for each version you want to reference later.

That means:

```text
Commit A -> tag v1.0.0
Commit B -> tag v1.1.0
Commit C -> tag v1.2.0
```

Whether or not those versions are released to production is a separate decision.

Recommended policy:

| Thing | Example | Meaning |
|---|---|---|
| Commit | `Create version v1.0.0` | Saved repository snapshot |
| Tag | `v1.0.0` | Name for that versioned snapshot |
| GitHub Release | Release page for `v1.0.0` | Published/packageable release |
| Production deployment | Deploy `v1.0.0` | Version actually running in production |

Use tags for versioned snapshots.

Use GitHub Releases when you want a public or official release page.

Use deployment records, release notes, GitHub Actions environments, or your deployment platform to track what actually went to production.

---

## 5. Create the Local Git Repository

Open a terminal in your project folder.

On Windows PowerShell:

```powershell
cd "C:\Path\To\Your\Project"
```

Check the folder contents:

```powershell
dir
```

Initialize the Git repository:

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

Before committing, make sure you are not about to commit sensitive files, such as:

- Passwords
- API keys
- `.env` files
- Private certificates
- Build output
- Temporary files
- Personal data

Create or update `.gitignore` as needed.

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

Adjust the ignore rules for your project. A .NET project, Node project, Python project, document project, and static website may all need different ignore rules.

Stage the files:

```bash
git add .
```

Commit the first file set:

```bash
git commit -m "Create version v1.0.0"
```

At this point, Git has a saved snapshot. The snapshot is not yet tagged. That comes next.

---

## 6. Create the GitHub Repository

You can create the GitHub repository through the GitHub website, GitHub CLI, or VS Code.

### Option A: GitHub Website

On GitHub:

1. Use the upper-right create menu.
2. Choose **New repository**.
3. Select the owner.
4. Enter the repository name.
5. Choose **Public** or **Private**.
6. Do not initialize with a README, `.gitignore`, or license if you already committed those locally.
7. Create the repository.

GitHub’s repository creation documentation describes the web flow for creating a new repository. [R4]

GitHub’s command-line import documentation specifically advises not initializing the new GitHub repository with README, license, or `.gitignore` files when you are pushing existing local code. [R5]

After GitHub creates the empty repository, copy the repository URL.

Then connect your local repository to GitHub:

```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
```

Verify the remote:

```bash
git remote -v
```

Push the main branch:

```bash
git push -u origin main
```

### Option B: GitHub CLI

If you have GitHub CLI installed, authenticate first:

```bash
gh auth login
```

Create a private GitHub repository from the current folder:

```bash
gh repo create YOUR-REPO-NAME --private --source=. --remote=origin --push
```

Create a public GitHub repository from the current folder:

```bash
gh repo create YOUR-REPO-NAME --public --source=. --remote=origin --push
```

The GitHub CLI manual documents `gh repo create` for creating repositories, including non-interactive creation with `--public`, `--private`, or `--internal`. [R12]

### Option C: VS Code

VS Code can publish a local repository directly to GitHub with **Publish to GitHub**, which creates a new GitHub repository and pushes commits in one step. [R6]

This is covered in more detail in [Section 11](#11-using-visual-studio-code).

---

## 7. Mark the First File Set as v1.0.0

Once the `v1.0.0` file set has been committed, create an annotated tag:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

Message wording note: the tag name is `v1.0.0`, but the annotated tag message is written as `Version 1.0.0`. That is intentional. The leading `v` in the tag name already means “version,” so repeating it in the human-readable message is valid but slightly redundant. A clean pattern is `git tag -a v1.0.0 -m "Version 1.0.0"`.

Push the tag to GitHub:

```bash
git push origin v1.0.0
```

Important:

> A normal `git push` usually pushes commits on the current branch. It does not automatically push every tag. Push version tags explicitly.

You can also push commits and annotated tags together with:

```bash
git push --follow-tags
```

For this guide, the most explicit beginner-friendly command is still:

```bash
git push origin v1.0.0
```

Verify your local tags:

```bash
git tag --list
```

Inspect the tag:

```bash
git show v1.0.0
```

Now you can accurately say:

> “The `v1.0.0` tag identifies the commit containing the v1.0.0 file set.”

Or more casually:

> “The files at `v1.0.0` are the v1.0.0 version.”

---

## 8. Continue Editing and Mark the Next File Set as v1.1.0

Continue editing files normally.

When the current project state should become `v1.1.0`, check status:

```bash
git status
```

Stage the changes:

```bash
git add .
```

Commit the new version:

```bash
git commit -m "Create version v1.1.0"
```

Tag the commit:

```bash
git tag -a v1.1.0 -m "Version 1.1.0"
```

Push the commit:

```bash
git push
```

Push the tag:

```bash
git push origin v1.1.0
```

You now have two versioned snapshots:

```text
v1.0.0
v1.1.0
```

Each tag points to a different commit. Each commit represents a different tracked file set.

---

## 9. View, Compare, Export, or Restore a Version

### List all tags

```bash
git tag --list
```

### Show a tag

```bash
git show v1.0.0
```

### View recent commits and tags

```bash
git log --oneline --decorate --graph --all
```

### Compare v1.0.0 to v1.1.0

Show all content differences:

```bash
git diff v1.0.0..v1.1.0
```

Show only changed file names:

```bash
git diff --name-only v1.0.0..v1.1.0
```

Show commits between versions:

```bash
git log --oneline v1.0.0..v1.1.0
```

### Temporarily view files at v1.0.0

```bash
git switch --detach v1.0.0
```

You are now looking at the repository as it existed at `v1.0.0`.

Return to `main`:

```bash
git switch main
```

### Create a branch from an old version

If you want to edit from `v1.0.0`, do not edit the tag. Create a branch from the tag:

```bash
git switch -c hotfix/v1.0.1 v1.0.0
```

Then edit, commit, tag, and push as usual.

### Export the v1.0.0 file set as a ZIP

```bash
git archive --format=zip --output project-v1.0.0.zip v1.0.0
```

Git’s `archive` documentation says it creates an archive containing the tree structure for the named tree. A tag can be used to identify the tree you want to archive. [R16]

### Restore one file from v1.0.0

Example:

```bash
git restore --source v1.0.0 -- README.md
```

Git’s `restore` documentation describes restoring working tree files from a source tree, commonly named by a commit, branch, or tag. [R15]

---

## 10. Tags vs. Releases vs. Production Deployments

This is where terminology matters.

### A tag is a version marker

A tag says:

> “This commit is version `v1.1.0`.”

That is true whether or not the version was released to production.

Use tags for:

- Internal baselines.
- Review versions.
- Document versions.
- Software versions.
- Milestones.
- Production releases.

### A GitHub Release is a published release object

A GitHub Release is based on a tag and can include release notes and downloadable assets. [R8]

Use a GitHub Release when you want to say:

> “This tagged version is officially published or packaged.”

Create a release with GitHub CLI:

```bash
gh release create v1.1.0 --title "v1.1.0" --notes "Describe what changed in v1.1.0."
```

The GitHub CLI manual for `gh release create` specifically describes creating a release from an annotated tag after creating and pushing the tag. [R13]

### A production deployment means something is running in production

A production deployment says:

> “This commit, branch, or tag is now deployed to production.”

This is operational information. It is not automatically the same thing as a Git tag.

GitHub environments can represent deployment targets such as `production`, `staging`, or `development`. [R11]

### Does production need a different tag?

Usually, no.

If `v1.1.0` is the version, keep it as `v1.1.0`.

If it goes to production, document that in one or more of these ways:

1. Create a GitHub Release for `v1.1.0`.
2. Say in the release notes that `v1.1.0` was deployed to production.
3. Use GitHub Actions environments or another deployment system to record the production deployment.
4. Deploy from the immutable tag `v1.1.0`.

Avoid creating a separate version number just because the same version went to production.

Better:

```text
v1.1.0 = the version
production deployment = v1.1.0 deployed to production
```

Less ideal:

```text
v1.1.0 = internal version
v1.1.0-prod = production version
```

That can become confusing unless your team has a very specific reason for it.

---

## 11. Using Visual Studio Code

VS Code is excellent for Git day-to-day work.

Use VS Code for:

- Reviewing changed files.
- Seeing diffs.
- Staging changes.
- Writing commit messages.
- Committing.
- Publishing to GitHub.
- Running Git commands in the integrated terminal.

VS Code’s Source Control documentation describes the Source Control view as the central place for Git workflows such as staging, committing, branching, merge conflicts, and GitHub integration. [R6]

### Open the folder

In VS Code:

```text
File > Open Folder...
```

Select the project folder.

Or open from a terminal:

```bash
code .
```

### Open Source Control

Use:

```text
Ctrl+Shift+G
```

Or click the Source Control icon in the Activity Bar.

### Initialize the repository

If the folder is not already a Git repository, VS Code should offer an **Initialize Repository** action in the Source Control view.

That is equivalent in spirit to:

```bash
git init
```

### Stage and commit

In Source Control:

1. Review changed files.
2. Stage individual files, or stage all changes.
3. Enter a commit message.
4. Commit.

For the first version:

```text
Create version v1.0.0
```

For the next version:

```text
Create version v1.1.0
```

### Publish to GitHub

If the local repo does not yet have a GitHub remote, VS Code can show **Publish to GitHub**.

VS Code’s docs say **Publish to GitHub** creates a new repository and pushes your commits in one step. [R6]

### Tagging in VS Code

For tagging, use the integrated terminal.

Open:

```text
View > Terminal
```

Or:

```text
Ctrl+`
```

Then run:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

VS Code’s terminal documentation says the integrated terminal lets you run command-line tools from inside VS Code. [R7]

The terminal is the best way to document tag commands because it is exact, current, and not dependent on optional extensions or UI variations.

---

## 12. Naming and Versioning Recommendations

### Use the `v` prefix

Recommended:

```text
v1.0.0
v1.1.0
v1.4.2
v1.5.0
```

Avoid mixing styles:

```text
1.0.0
v1.1
release-1.2
Version_1_Final
```

Pick one style and stick to it.

### Use annotated tags for meaningful versions

Recommended:

```bash
git tag -a v1.1.0 -m "Version 1.1.0"
```

Not recommended for meaningful shared versions:

```bash
git tag v1.1.0
```

Lightweight tags are not wrong, but annotated tags are better for version markers because they carry metadata. [R2]

### Use SemVer-style increments

Typical SemVer-style meaning:

| Change | Example | Meaning |
|---|---|---|
| Patch | `v1.0.0` to `v1.0.1` | Fixes or very small corrections |
| Minor | `v1.0.0` to `v1.1.0` | New content/features without a major break |
| Major | `v1.0.0` to `v2.0.0` | Breaking change, major rewrite, or major restructuring |

For documentation projects, define your own interpretation:

- Patch: spelling, grammar, formatting, tiny clarification.
- Minor: new section, new example, new appendix, meaningful expansion.
- Major: major restructure, incompatible procedure, or a fundamentally new version of the material.

---

## 13. Common Mistakes to Avoid

### Mistake 1: Tagging uncommitted files

Tags point to commits, not uncommitted edits.

Always run:

```bash
git status
```

If files are modified, staged, untracked, or unsaved in your editor, resolve that before tagging.

### Mistake 2: Forgetting to push the tag

This pushes commits:

```bash
git push
```

This pushes a tag:

```bash
git push origin v1.1.0
```

### Mistake 3: Moving a published version tag

Avoid changing what `v1.1.0` points to after it has been pushed.

A version tag should be treated as stable.

### Mistake 4: Using a tag as a branch

A tag is a fixed marker. It is not where ongoing work happens.

To edit from an old tag, create a branch:

```bash
git switch -c hotfix/v1.0.1 v1.0.0
```

### Mistake 5: Treating a GitHub Release and production deployment as the same thing

They are related, but different.

A GitHub Release publishes or packages a tagged version. [R8]

A production deployment means a ref was deployed to an environment such as production. [R11]

---

## 14. Quick Command Cheat Sheet

### First-time setup

```bash
cd "C:\Path\To\Your\Project"
git init -b main
git status
git add .
git commit -m "Create version v1.0.0"
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git push -u origin main
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

### Create the next version

```bash
git status
git add .
git commit -m "Create version v1.1.0"
git tag -a v1.1.0 -m "Version 1.1.0"
git push
git push origin v1.1.0
```

### Compare versions

```bash
git diff v1.0.0..v1.1.0
git diff --name-only v1.0.0..v1.1.0
git log --oneline v1.0.0..v1.1.0
```

### Export a version

```bash
git archive --format=zip --output project-v1.0.0.zip v1.0.0
```

### Create a GitHub Release

```bash
gh release create v1.1.0 --title "v1.1.0" --notes "Describe what changed in v1.1.0."
```

---

# Appendix A: Expanded Git Command Reference

This appendix repeats and expands the commands from the guide. That is intentional.

## A.1 Commands in typical workflow order

### `cd`

```powershell
cd "C:\Path\To\Your\Project"
```

Moves your terminal into the project folder.

Official reference: shell-specific command, not a Git command.

### `git init -b main`

```bash
git init -b main
```

Creates a new local Git repository using `main` as the initial branch name.

Official reference: [R17]

### `git status`

```bash
git status
```

Shows changed, staged, and untracked files.

Official reference: [R18]

### `git add .`

```bash
git add .
```

Stages all changes under the current folder, subject to `.gitignore`.

Official reference: [R19]

### `git commit`

```bash
git commit -m "Create version v1.0.0"
```

Creates a commit from staged changes.

Official reference: [R20]

### `git remote add origin`

```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
```

Connects the local repo to GitHub.

Official reference: [R21]

### `git remote -v`

```bash
git remote -v
```

Lists configured remotes.

Official reference: [R21]

### `git push -u origin main`

```bash
git push -u origin main
```

Pushes `main` to GitHub and sets the upstream relationship.

Official reference: [R22]

### `git tag -a`

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

Creates an annotated tag.

Official reference: [R2]

### `git push origin <tag>`

```bash
git push origin v1.0.0
```

Pushes a specific tag to GitHub.

Official reference: [R22]

---

## A.2 Commands in alphabetical order

### `gh auth login`

```bash
gh auth login
```

Signs in to GitHub CLI.

Official reference: [R23]

### `gh release create`

```bash
gh release create v1.1.0 --title "v1.1.0" --notes "Describe what changed."
```

Creates a GitHub Release.

Official reference: [R13]

### `gh repo create`

```bash
gh repo create YOUR-REPO-NAME --private --source=. --remote=origin --push
```

Creates a GitHub repository from the command line.

Official reference: [R12]

### `git add`

```bash
git add .
```

Stages files.

Official reference: [R19]

### `git archive`

```bash
git archive --format=zip --output project-v1.0.0.zip v1.0.0
```

Exports the tracked files at a tag to an archive.

Official reference: [R16]

### `git branch -M`

```bash
git branch -M main
```

Renames the current branch to `main`.

Official reference: [R24]

### `git commit`

```bash
git commit -m "Create version v1.0.0"
```

Creates a commit.

Official reference: [R20]

### `git diff`

```bash
git diff v1.0.0..v1.1.0
```

Shows differences between versions.

Official reference: [R25]

### `git diff --name-only`

```bash
git diff --name-only v1.0.0..v1.1.0
```

Shows only changed file names.

Official reference: [R25]

### `git init`

```bash
git init -b main
```

Creates a new repository.

Official reference: [R17]

### `git log`

```bash
git log --oneline --decorate --graph --all
```

Shows commit history.

Official reference: [R26]

### `git push`

```bash
git push
```

Pushes commits to the configured upstream.

Official reference: [R22]

### `git push --follow-tags`

```bash
git push --follow-tags
```

Pushes missing annotated tags that are reachable from the commits being pushed.

Official reference: [R22]

### `git push -u origin main`

```bash
git push -u origin main
```

Pushes `main` and sets upstream tracking.

Official reference: [R22]

### `git push origin <tag>`

```bash
git push origin v1.1.0
```

Pushes one tag.

Official reference: [R22]

### `git remote add`

```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
```

Adds a remote.

Official reference: [R21]

### `git remote -v`

```bash
git remote -v
```

Lists remotes.

Official reference: [R21]

### `git restore`

```bash
git restore --source v1.0.0 -- README.md
```

Restores a file from a tag, branch, or commit.

Official reference: [R15]

### `git show`

```bash
git show v1.0.0
```

Shows information about a tag or commit.

Official reference: [R27]

### `git status`

```bash
git status
```

Shows current repository state.

Official reference: [R18]

### `git switch`

```bash
git switch main
```

Switches branches.

```bash
git switch --detach v1.0.0
```

Temporarily views the repository at a tag.

```bash
git switch -c hotfix/v1.0.1 v1.0.0
```

Creates a branch from a tag.

Official reference: [R28]

### `git tag`

```bash
git tag --list
```

Lists tags.

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

Creates an annotated tag.

```bash
git tag -d v1.0.0
```

Deletes a local tag.

```bash
git push origin --delete v1.0.0
```

Deletes a remote tag.

Use tag deletion carefully.

Official reference: [R2]

---

# Appendix B: Expanded VS Code Reference

## B.1 Source Control view

VS Code’s Source Control view is the main Git UI. It supports reviewing changes, staging, committing, branching, resolving merge conflicts, and GitHub integration. [R6]

Open it with:

```text
Ctrl+Shift+G
```

Or select the Source Control icon in the Activity Bar.

## B.2 Initialize Repository

If your folder is not yet a Git repository, VS Code can show **Initialize Repository**.

This creates a Git repository for the opened folder.

## B.3 Commit workflow

A typical VS Code Git workflow is:

1. Edit files.
2. Open Source Control.
3. Review changes.
4. Stage files.
5. Enter a commit message.
6. Commit.

## B.4 Publish to GitHub

VS Code’s documentation says that if you start with a local folder and want to save it to GitHub, you can use the **Publish to GitHub** button in the Source Control view. [R29]

Use this when:

- You already have a local repository.
- You have committed files.
- You want VS Code to create the GitHub remote repository.

## B.5 Integrated Terminal

Use the integrated terminal for exact commands.

Open it with:

```text
View > Terminal
```

Or:

```text
Ctrl+`
```

VS Code’s terminal documentation describes the integrated terminal as a way to run command-line tools from within VS Code. [R7]

For tags, run:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

This is clearer and more durable than relying on optional UI commands or extensions.

---

# Appendix C: Expanded Versioning Concepts

## C.1 “File set” vs. “repository snapshot”

Reader-friendly phrase:

> “The v1.0.0 file set.”

Technically precise phrase:

> “The tracked repository state at the commit tagged `v1.0.0`.”

Best compromise:

> “The files as they existed at tag `v1.0.0`.”

## C.2 Why tags point to commits

A tag points to a Git object, usually a commit. [R2]

The commit identifies the tracked state of the project. That is why tags are the right way to mark a versioned file set.

## C.3 Annotated vs. lightweight tags

Annotated tag:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

Best for:

- Version markers.
- Shared history.
- Release candidates.
- Production releases.
- Anything another person or future-you may rely on.

Lightweight tag:

```bash
git tag v1.0.0
```

Best for:

- Temporary labels.
- Local bookmarks.
- Private references.

For this guide, use annotated tags.

## C.4 Internal versions are still valid versions

A version does not need to go to production to be useful.

Example:

```text
v1.0.0 = first stable internal baseline
v1.1.0 = reviewed draft
v1.2.0 = production release
```

All three can be valid tags.

Only `v1.2.0` may have been released or deployed.

## C.5 SemVer for documentation projects

SemVer is software-oriented, but the pattern is still useful for documents and file sets. [R14]

Example policy:

- Patch: spelling, grammar, formatting, tiny clarification.
- Minor: new section, new example, new appendix, meaningful expansion.
- Major: major restructure, incompatible procedure, or a fundamentally new version of the material.

---

# Appendix D: Production Release and Deployment Details

## D.1 Recommended production model

Use the same version tag.

Example:

```text
Tag: v1.1.0
GitHub Release: v1.1.0
Production deployment: v1.1.0
```

That is clear.

## D.2 When to create a GitHub Release

Create a GitHub Release when:

- You want release notes.
- You want a visible release page.
- You want source archives.
- You want uploaded assets.
- You want to say this version was officially published.

GitHub Releases are based on Git tags. [R8]

## D.3 When to record a deployment

Record a deployment when:

- The version actually went to staging.
- The version actually went to production.
- You need an audit trail.
- You use CI/CD.
- You need approval gates or environment protection rules.

GitHub environments can represent targets such as production, staging, and development. [R11]

## D.4 Should there be a separate production tag?

Usually, no.

Prefer:

```text
v1.1.0 deployed to production
```

over:

```text
v1.1.0-prod
```

A separate production tag can be useful in specialized workflows, but it can also create confusion.

## D.5 Avoid moving production tags

Avoid a moving tag named:

```text
production
```

Tags are usually expected to be stable.

If you need a moving pointer, consider:

- A deployment record.
- A `production` branch.
- Your CI/CD environment history.
- Release notes.

---

# Appendix E: Troubleshooting

## E.1 The tag does not appear on GitHub

You probably created it locally but did not push it.

Run:

```bash
git push origin v1.0.0
```

## E.2 I tagged the wrong commit

If the tag is only local:

```bash
git tag -d v1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"
```

If the tag was pushed:

```bash
git push origin --delete v1.0.0
git tag -d v1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

Use this carefully. Published version tags should generally be treated as permanent.

## E.3 I want to edit an old version

Create a branch from the old tag:

```bash
git switch -c hotfix/v1.0.1 v1.0.0
```

Do not try to “edit the tag.”

## E.4 I want a ZIP of an old version

```bash
git archive --format=zip --output project-v1.0.0.zip v1.0.0
```

## E.5 I want one file from an old version

```bash
git restore --source v1.0.0 -- path/to/file.ext
```

Then inspect and commit if appropriate.

---


# Appendix F: Knowledge Base and How-To Reference

This appendix is intentionally more question-and-answer oriented than the main guide. It incorporates and expands the supplemental reference material supplied for the `v1.1.0` update. The purpose is to answer the practical questions that often come up immediately after a user creates a repository, commits the first files, and starts using tags for versions.

## F.1 Is it GitHub, Github, github, or Git Hub?

The official product/company styling is:

```text
GitHub
```

Use **GitHub** in documentation, README files, guides, and professional writing.

| Form | Recommended? | Notes |
|---|---:|---|
| `GitHub` | Yes | Official capitalization used by GitHub documentation. [R4] |
| `Github` | No | Common informal typo. |
| `github` | Sometimes | Acceptable in lowercase contexts such as URLs, package names, usernames, or command-line text. |
| `Git Hub` | No | Incorrect as the product/company name. |

Example:

```markdown
This project is hosted on GitHub.
```

## F.2 What is a good repository name?

A good repository name should be short, specific, descriptive, and durable.

For a simple web calculator used as a Selenium testing target, this is better:

```text
selenium-calculator-example
```

than this:

```text
calculator
```

`calculator` is understandable, but it is generic. Six months later, you may not remember whether it was a production calculator, a learning exercise, a Selenium demo, a JavaScript experiment, or something else.

Good repository names usually follow these guidelines:

- Use lowercase unless there is a strong project convention otherwise.
- Use hyphens between words: `selenium-calculator-example`.
- Avoid spaces.
- Avoid vague names like `test`, `demo`, `project`, or `calculator` unless the repo is private and temporary.
- Name the repo for its purpose, not only its contents.
- Prefer names that still make sense when seen in a GitHub URL.

Examples:

| Repository name | When it makes sense |
|---|---|
| `selenium-calculator-example` | Best general-purpose name for a calculator app used with Selenium examples. |
| `web-calculator-selenium-demo` | Clear, but slightly longer. |
| `calculator-selenium-tests` | Good if the repo mainly contains Selenium tests. |
| `sample-web-calculator` | Good if the focus is the calculator app itself. |
| `calculator` | Fine for a tiny private repo, but not very descriptive. |

## F.3 What should the GitHub repository description be?

A GitHub repository description should be a short, clear label that answers:

> What is this repository?

For the sample calculator project, a good description is:

```text
Sample web calculator used for Selenium automated testing examples
```

That description is specific, short, and purpose-oriented.

Avoid making the description mostly about the tool that helped create the files. For example, instead of this:

```text
Claude: Web calculator
```

prefer this:

```text
Sample web calculator used for Selenium automated testing examples
```

If the project was created with help from Claude, ChatGPT, Copilot, or another AI tool, mention that in the README if it matters. GitHub’s README guidance says the README is where you explain why the project is useful, what people can do with it, and how to use it. [R36]

Example README wording:

```markdown
This sample web calculator was created with assistance from Claude and is used as a simple target application for Selenium automated test cases.
```

## F.4 Should a GitHub repository description include a period?

Usually, omit the period when the description is a short label-style phrase.

Recommended:

```text
Sample web calculator used for Selenium automated testing examples
```

Also acceptable, but less common for a short GitHub description:

```text
Sample web calculator used for Selenium automated testing examples.
```

Rule of thumb:

| Description style | Period? | Example |
|---|---:|---|
| Short phrase | Usually no | `Sample web calculator used for Selenium automated testing examples` |
| Complete sentence | Usually yes | `This repository contains a sample web calculator used for Selenium automated testing examples.` |
| Multiple sentences | Yes | `This repository contains a sample web calculator. It is used for Selenium testing examples.` |

## F.5 What is the proper term for a commit “name”?

The proper term is usually **commit message**.

When you run this:

```bash
git commit -m "Update calculator behavior"
```

`Update calculator behavior` is the commit message.

A commit also has a generated identifier, commonly called a **commit hash**, **commit SHA**, or **SHA**.

Example:

```text
a1b2c3d Update calculator behavior
```

In that line:

- `a1b2c3d` is the abbreviated commit hash/SHA.
- `Update calculator behavior` is the commit message.

For one-line commit messages, a common best practice is:

- Use a short imperative phrase.
- Start with a verb.
- Do not usually end with a period.
- Keep it specific enough to be useful later.

Good examples:

```text
Add initial calculator files
Update calculator behavior
Fix division-by-zero test case
Document version tag workflow
```

Less helpful examples:

```text
Update
Changes
Final
More stuff
Fixed things.
```

Periods are usually unnecessary in short one-line commit messages. If the commit message has a longer body with multiple sentences, normal sentence punctuation is fine.

## F.6 What is the difference between a tag name and a tag message?

This command has both:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

| Part | Proper term | Meaning |
|---|---|---|
| `v1.0.0` | Tag name | The name you use to refer to the version. |
| `Version 1.0.0` | Annotated tag message | Human-readable message stored in the annotated tag. |

The tag name commonly includes the leading `v`:

```text
v1.0.0
```

The human-readable tag message usually does not need to repeat the `v`:

```text
Version 1.0.0
```

This is valid but redundant:

```bash
git tag -a v1.0.0 -m "Version v1.0.0"
```

This is cleaner:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

The reason is simple: the `v` in `v1.0.0` already means “version.”

## F.7 Does tagging apply to the whole repo?

Yes.

A Git tag points to a commit. A commit represents the tracked state of the repository at that moment. Therefore, a tag identifies the whole repository snapshot, not an individual file and not a loose subset of files. [R1] [R2]

Suppose `v1.0.0` contains:

```text
index.html
styles.css
calculator.js
```

You commit those files and tag the commit:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

Now `v1.0.0` identifies the repository snapshot containing those tracked files as they existed at that commit.

## F.8 If I add or update one file, does the next tag apply to all files?

Yes.

Suppose `v1.0.0` contains:

```text
index.html
styles.css
calculator.js
```

Then you edit only:

```text
calculator.js
```

You commit and tag the new version:

```bash
git add calculator.js
git commit -m "Update calculator behavior"
git tag -a v1.0.1 -m "Version 1.0.1"
```

The `v1.0.1` tag still identifies the whole repository snapshot:

```text
index.html       unchanged from v1.0.0
styles.css      unchanged from v1.0.0
calculator.js   changed in v1.0.1
```

That is normal and correct.

A version tag means:

> This whole committed repository state is version 1.0.1.

It does not mean:

> Only the file that changed is version 1.0.1.

## F.9 Can I tag just a subset of files?

Not directly.

Git tags point to commits. Commits represent repository snapshots. Git does not directly support saying “tag only these three files as `v1.0.1`” while excluding the rest of the repository from the meaning of that tag.

But there are several practical patterns depending on what you actually need.

### Case A: You edited several files but only want some changes included in the version

Stage only the files that belong in the version:

```bash
git status
git add calculator.js
git commit -m "Fix calculator behavior"
git tag -a v1.0.1 -m "Version 1.0.1"
```

Other edited but unstaged files are not part of that commit, so they are not part of the `v1.0.1` snapshot.

This is useful when you are working on a larger change but need to release a small fix first.

### Case B: You want a ZIP that contains only selected files

Tag the whole repository snapshot, but export only selected files:

```bash
git archive -o calculator-v1.0.1.zip v1.0.1 index.html styles.css calculator.js
```

This creates a ZIP containing only those paths from the tagged snapshot. Git’s archive command creates an archive from a named tree, and a tag can identify the tree to archive. [R16]

### Case C: You have multiple components in one repository

Example:

```text
calculator-app/
selenium-tests/
docs/
```

You can use component-specific tag names:

```bash
git tag -a calculator-v1.0.1 -m "Calculator version 1.0.1"
git tag -a selenium-tests-v0.2.0 -m "Selenium tests version 0.2.0"
```

Technically, both tags still point to whole commits. The tag names tell humans which component the version refers to.

### Case D: The components are truly independent

If two parts of a project have independent lifecycles, separate repositories may be cleaner.

Example:

```text
web-calculator
web-calculator-selenium-tests
```

Separate repositories may make sense when:

- Different teams own the parts.
- The parts are released on different schedules.
- One project can be reused without the other.
- Each project needs separate issues, pull requests, releases, or permissions.
- The combined repository is becoming confusing.

For a small learning project, keep the app and tests together unless there is a clear reason to split them.

## F.10 How should source code and test cases be versioned together?

If the test cases are written specifically for the source code in the same repository, version them together.

Example:

```text
v1.0.0 = calculator app + initial Selenium tests
v1.0.1 = calculator bug fix + updated Selenium expectations
v1.1.0 = new calculator feature + new Selenium tests
```

This is often the simplest and best model because the source code and tests form one working project snapshot.

Use one repo when:

- The tests are tightly coupled to the app.
- The tests and app should change together.
- A version should mean “this app and these tests go together.”
- The project is small or educational.

Consider multiple repos when:

- The app and test suite evolve independently.
- The test suite is used against multiple apps.
- The app has one release cycle and the tests have another.
- Separate teams own the app and tests.
- Separate permissions or workflows are needed.

For many projects, especially novice-to-intermediate projects, one repository with regular version tags is the best starting point.

## F.11 What is the difference between tagging, versioning, and creating releases?

These terms are related, but they are not the same.

| Term | What it is | Example |
|---|---|---|
| Versioning | The overall practice of assigning version numbers to meaningful project states. | `1.0.0`, `1.0.1`, `1.1.0` |
| Git tag | The Git mechanism used to name a specific commit. | `v1.0.0` |
| Annotated tag | A tag with metadata and a message. | `git tag -a v1.0.0 -m "Version 1.0.0"` |
| GitHub Release | A GitHub release page/package based on a tag. | Release notes for `v1.0.0` |
| Production deployment | The act or record of putting a ref into production. | Deploy `v1.0.0` to production |

GitHub’s release documentation says releases are based on Git tags, and tags mark points in repository history. [R8]

Simple rule:

- Use **versions** to communicate project meaning.
- Use **Git tags** to mark versioned snapshots in Git.
- Use **GitHub Releases** to publish or package tagged versions.
- Use **deployment records** to track what actually went to production.

## F.12 Should every commit get a tag?

No.

A commit is already a saved snapshot. Tag only the commits that matter as named versions, milestones, releases, review baselines, or stable checkpoints.

Good reasons to tag:

- First usable version.
- Review-ready version.
- Published release.
- Production deployment candidate.
- Before a major rewrite.
- A version you expect to reference later.

Poor reasons to tag:

- Every small typo fix.
- Every experimental commit.
- Every commit just because Git allows it.

For normal work, many commits will not have tags. That is good.

## F.13 How do I retrieve or download a particular version?

There are several good options.

### Option A: View a tag locally

Modern style:

```bash
git switch --detach v1.0.0
```

Older widely supported style:

```bash
git checkout v1.0.0
```

This puts you in detached HEAD mode, which is fine for inspecting, testing, or copying files. Git’s checkout documentation covers checking out branches or paths and is still widely used, while `git switch` is the clearer modern command for switching branches or detached states. [R33] [R28]

Return to main:

```bash
git switch main
```

or:

```bash
git checkout main
```

### Option B: Create a branch from a tag

Use this if you want to edit from an old version:

```bash
git switch -c fix-v1.0.0 v1.0.0
```

or:

```bash
git checkout -b fix-v1.0.0 v1.0.0
```

### Option C: Download a tag ZIP from GitHub

On GitHub:

1. Open the repository.
2. Open **Tags** or **Releases**.
3. Choose the tag, such as `v1.0.0`.
4. Download the source code ZIP.

GitHub’s releases/tags documentation explains that you can view a repository’s releases and tags by release name or tag version number. [R10]

A common direct URL shape is:

```text
https://github.com/OWNER/REPOSITORY/archive/refs/tags/v1.0.0.zip
```

Replace `OWNER`, `REPOSITORY`, and `v1.0.0` with the actual values.

### Option D: Create a ZIP locally with `git archive`

```bash
git archive -o project-v1.0.0.zip v1.0.0
```

Selected files only:

```bash
git archive -o calculator-v1.0.1.zip v1.0.1 index.html styles.css calculator.js
```

### Option E: Clone and check out a specific tag

Explicit two-step approach:

```bash
git clone https://github.com/OWNER/REPOSITORY.git
cd REPOSITORY
git checkout v1.0.0
```

Single command shape:

```bash
git clone --branch v1.0.0 --single-branch https://github.com/OWNER/REPOSITORY.git
```

Git clone supports `--branch` and `--single-branch`; with tags, the result may be a detached HEAD, which is normal. [R34]

## F.14 How do I compare two versions?

Show all content differences:

```bash
git diff v1.0.0 v1.0.1
```

Show only changed file names:

```bash
git diff --name-only v1.0.0 v1.0.1
```

Show commits between the two tags:

```bash
git log v1.0.0..v1.0.1
```

Show compact one-line commit history:

```bash
git log --oneline v1.0.0..v1.0.1
```

This is useful when writing release notes. Git’s `diff` command compares changes between commits, trees, files, or the working tree, and `log` shows commit history. [R25] [R26]

## F.15 What does `git show v1.0.0` do?

This command displays information about the object named `v1.0.0`:

```bash
git show v1.0.0
```

If `v1.0.0` is an annotated tag, this usually shows:

1. The tag information.
2. The tag message.
3. The commit the tag points to.
4. The commit message.
5. Often, the diff associated with that commit.

`git show v1.0.0` does **not** switch your files to that version. It only displays information. Git’s `show` documentation describes showing objects such as commits and tags. [R27]

Compare:

```bash
git show v1.0.0
```

Shows information.

```bash
git switch --detach v1.0.0
```

Changes your working tree to view that version.

## F.16 Why did `git show v1.0.0` open in an interactive screen?

Git probably opened the output in a **pager**.

A pager displays long output one screen at a time. Git can pipe output into a pager and supports `--no-pager` to avoid doing so. [R30]

Git’s configuration documentation says Git’s pager preference order is `$GIT_PAGER`, then `core.pager`, then `$PAGER`, then the default chosen at compile time, usually `less`. [R31]

So on many systems, the pager is `less`.

This can feel like a special Git mode, but it is usually just Git showing output through `less`.

## F.17 How do I use Git’s pager?

Most pager keys work immediately. You usually do **not** press Enter after them unless the command itself needs a search term.

The most common keys are listed first.

| Key | Case-sensitive? | What it does | Notes |
|---|---:|---|---|
| `q` | Yes | Quit the pager | Returns to the command prompt. |
| `Space` | No | Move forward one page | Very common. |
| `Enter` | No | Move forward one line | Useful for careful reading. |
| `b` | Yes | Move backward one page | Lowercase `b`. |
| `G` | Yes | Jump to the end | Uppercase `G`, usually `Shift+G`. Do not press Enter afterward. |
| `g` | Yes | Jump to the beginning | Lowercase `g`. |
| `/text` then `Enter` | The slash command is lowercase; search matching can depend on settings | Search forward for `text` | Type `/`, the search text, then press Enter. |
| `n` | Yes | Next search result | Lowercase `n`. |
| `N` | Yes | Previous search result | Uppercase `N`, usually `Shift+N`. |
| `h` | Yes | Help | Shows less help if available. Press `q` to leave help. |

Specific answers:

- To jump to the end, press uppercase `G` (`Shift+G`).
- `G` is case-sensitive. Lowercase `g` jumps to the beginning.
- You do **not** need to press Enter after `G`.
- After jumping to the end, you are still inside the pager. Press `q` when you want to return to the command prompt.
- You can go from end to beginning with lowercase `g`.
- You can move backward with `b` or forward with `Space`.

The `less` manual describes `less` as a pager that can move backward and forward through output and does not need to read an entire file before starting. [R32]

## F.18 How do I avoid the pager?

For one command:

```bash
git --no-pager show v1.0.0
```

Save the output to a file:

```bash
git show v1.0.0 > v1.0.0.txt
```

Pipe to another command:

```bash
git show v1.0.0 | cat
```

Configure Git globally not to use a pager:

```bash
git config --global core.pager cat
```

That global setting is usually not recommended for beginners because the pager is useful for long diffs and logs. Prefer `git --no-pager ...` when you only want to bypass it once.

On PowerShell, you can also set an environment variable for the current session:

```powershell
$env:GIT_PAGER = "cat"
git show v1.0.0
```

Close and reopen the terminal to clear that temporary session variable.

## F.19 How do I delete a tag?

Delete a local tag:

```bash
git tag -d v1.0.0
```

Delete a remote tag from GitHub:

```bash
git push origin --delete v1.0.0
```

Use this carefully. Published version tags should usually be treated as stable.

## F.20 How do I rename a tag?

Git does not really rename tags directly. The usual workflow is:

1. Create the corrected tag.
2. Delete the old tag locally.
3. Delete the old tag remotely if it was pushed.

Example:

```bash
git tag -a v1.0.0-corrected -m "Version 1.0.0 corrected"
git tag -d old-tag-name
git push origin v1.0.0-corrected
git push origin --delete old-tag-name
```

Be cautious if anyone else may already be using the old tag.

## F.21 How do I see which commit a tag points to?

Show the commit hash for the tag:

```bash
git rev-list -n 1 v1.0.0
```

Git’s `rev-list` command lists commit objects in reverse chronological order and is often used for plumbing-style history queries. [R35]

Show the tag without the patch:

```bash
git show --no-patch v1.0.0
```

Show all tags with short messages:

```bash
git tag -n
```

Sort tags by creator date:

```bash
git tag --sort=creatordate
```

Reverse chronological:

```bash
git tag --sort=-creatordate
```

## F.22 Should I use branches or tags?

Use both, but for different jobs.

| Need | Best tool |
|---|---|
| Ongoing development | Branch |
| Fixed version snapshot | Tag |
| Experimental work | Branch |
| Release marker | Tag |
| Bug fix based on an old version | Branch from tag, then create a new tag |
| Production deployment record | Deployment system, environment record, release notes, or release page |

A branch moves as new commits are added.

A version tag should not move.

## F.23 Can I modify files while checked out at a tag?

You can edit files while checked out at a tag, but you will usually be in detached HEAD mode.

That is fine for temporary inspection, but not ideal for ongoing work.

Better:

```bash
git switch -c fix-v1.0.0 v1.0.0
```

Then make changes on that branch.

## F.24 Should I create GitHub Releases too?

For a simple private project, tags may be enough.

Create GitHub Releases when you want:

- A release notes page.
- Downloadable assets.
- A polished public release history.
- Source archives grouped by version.
- A clearer distinction between “tagged internally” and “published externally.”

Tags are the underlying Git version markers. GitHub Releases are a presentation and packaging layer on top of tags. [R8] [R9]

## F.25 Recommended README section for a tagged project

A simple README section could look like this:

````markdown
## Version Tags

This repository uses Git tags to mark versioned snapshots of the project.

Examples:

- `v1.0.0` - Initial calculator example
- `v1.0.1` - Small update or fix to the calculator

To view a specific version:

```bash
git checkout v1.0.0
```

To return to the main branch:

```bash
git checkout main
```
````

For a real README, you may prefer `git switch --detach v1.0.0` and `git switch main`, but `git checkout` is still common and widely recognized.

## F.26 Recommended beginner workflow for a small calculator project

Initial version:

```bash
git add .
git commit -m "Add initial calculator example"
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin main
git push origin v1.0.0
```

Patch version:

```bash
git status
git add calculator.js
git commit -m "Update calculator behavior"
git tag -a v1.0.1 -m "Version 1.0.1"
git push origin main
git push origin v1.0.1
```

Result:

```text
v1.0.0 = first complete project snapshot
v1.0.1 = small fix or update
```

Most important idea:

> A tag labels a repository snapshot. A repository snapshot is the file set. That is why tags are a good way to version file sets in Git.


# Appendix G: References

## Core conceptual references

[R1] Git Book, “Git Basics - Tagging.”  
https://git-scm.com/book/en/v2/Git-Basics-Tagging

[R2] Git documentation, `git-tag`.  
https://git-scm.com/docs/git-tag

[R3] Git documentation, `gitglossary`.  
https://git-scm.com/docs/gitglossary

[R4] GitHub Docs, “Creating a new repository.”  
https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository

[R5] GitHub Docs, “Adding locally hosted code to GitHub.”  
https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github

[R6] Visual Studio Code Docs, “Source Control in VS Code.”  
https://code.visualstudio.com/docs/sourcecontrol/overview

[R7] Visual Studio Code Docs, “Terminal Basics.”  
https://code.visualstudio.com/docs/terminal/basics

[R8] GitHub Docs, “About releases.”  
https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases

[R9] GitHub Docs, “Managing releases in a repository.”  
https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository

[R10] GitHub Docs, “Viewing your repository’s releases and tags.”  
https://docs.github.com/en/repositories/releasing-projects-on-github/viewing-your-repositorys-releases-and-tags

[R11] GitHub Docs, “Deployment environments.”  
https://docs.github.com/en/actions/concepts/workflows-and-actions/deployment-environments

[R12] GitHub CLI Manual, `gh repo create`.  
https://cli.github.com/manual/gh_repo_create

[R13] GitHub CLI Manual, `gh release create`.  
https://cli.github.com/manual/gh_release_create

[R14] Semantic Versioning 2.0.0.  
https://semver.org/

[R15] Git documentation, `git-restore`.  
https://git-scm.com/docs/git-restore

[R16] Git documentation, `git-archive`.  
https://git-scm.com/docs/git-archive

## Git command references used in Appendix A

[R17] Git documentation, `git-init`.  
https://git-scm.com/docs/git-init

[R18] Git documentation, `git-status`.  
https://git-scm.com/docs/git-status

[R19] Git documentation, `git-add`.  
https://git-scm.com/docs/git-add

[R20] Git documentation, `git-commit`.  
https://git-scm.com/docs/git-commit

[R21] Git documentation, `git-remote`.  
https://git-scm.com/docs/git-remote

[R22] Git documentation, `git-push`.  
https://git-scm.com/docs/git-push

[R23] GitHub CLI Manual, `gh auth login`.  
https://cli.github.com/manual/gh_auth_login

[R24] Git documentation, `git-branch`.  
https://git-scm.com/docs/git-branch

[R25] Git documentation, `git-diff`.  
https://git-scm.com/docs/git-diff

[R26] Git documentation, `git-log`.  
https://git-scm.com/docs/git-log

[R27] Git documentation, `git-show`.  
https://git-scm.com/docs/git-show

[R28] Git documentation, `git-switch`.  
https://git-scm.com/docs/git-switch

## VS Code reference used in Appendix B

[R29] Visual Studio Code Docs, “Quickstart: Use source control in VS Code.”  
https://code.visualstudio.com/docs/sourcecontrol/quickstart

## Additional references used in Appendix F


[R30] Git documentation, `git` global options, including `--no-pager`.  
https://git-scm.com/docs/git

[R31] Git documentation, `git-config`, including `core.pager`.  
https://git-scm.com/docs/git-config

[R32] Linux manual page, `less(1)`.  
https://man7.org/linux/man-pages/man1/less.1.html

[R33] Git documentation, `git-checkout`.  
https://git-scm.com/docs/git-checkout

[R34] Git documentation, `git-clone`.  
https://git-scm.com/docs/git-clone

[R35] Git documentation, `git-rev-list`.  
https://git-scm.com/docs/git-rev-list

[R36] GitHub Docs, “About the repository README file.”  
https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes

---

# Index

## Annotated tag

See [3. Proper Terms](#3-proper-terms), [7. Mark the First File Set as v1.0.0](#7-mark-the-first-file-set-as-v100), and [Appendix C](#appendix-c-expanded-versioning-concepts).

## Branch

See [9. View, Compare, Export, or Restore a Version](#9-view-compare-export-or-restore-a-version) and [Appendix A](#appendix-a-expanded-git-command-reference).

## Commit

See [2. The Core Concept](#2-the-core-concept), [3. Proper Terms](#3-proper-terms), and [Appendix C](#appendix-c-expanded-versioning-concepts).

## Deployment

See [10. Tags vs. Releases vs. Production Deployments](#10-tags-vs-releases-vs-production-deployments), [Appendix D](#appendix-d-production-release-and-deployment-details), and [Appendix F](#appendix-f-knowledge-base-and-how-to-reference).

## File set

See [1. Purpose of This Guide](#1-purpose-of-this-guide), [2. The Core Concept](#2-the-core-concept), and [Appendix C](#appendix-c-expanded-versioning-concepts).

## GitHub CLI

See [6. Create the GitHub Repository](#6-create-the-github-repository) and [Appendix A](#appendix-a-expanded-git-command-reference).

## GitHub repository description

See [Appendix F.3](#f3-what-should-the-github-repository-description-be) and [Appendix F.4](#f4-should-a-github-repository-description-include-a-period).

## Git pager

See [Appendix F.16](#f16-why-did-git-show-v100-open-in-an-interactive-screen), [Appendix F.17](#f17-how-do-i-use-gits-pager), and [Appendix F.18](#f18-how-do-i-avoid-the-pager).

## Knowledge Base

See [Appendix F: Knowledge Base and How-To Reference](#appendix-f-knowledge-base-and-how-to-reference).

## Repository naming

See [Appendix F.2](#f2-what-is-a-good-repository-name).

## Tag message

See [Appendix F.6](#f6-what-is-the-difference-between-a-tag-name-and-a-tag-message).

## GitHub Release

See [10. Tags vs. Releases vs. Production Deployments](#10-tags-vs-releases-vs-production-deployments) and [Appendix D](#appendix-d-production-release-and-deployment-details).

## Lightweight tag

See [3. Proper Terms](#3-proper-terms) and [Appendix C](#appendix-c-expanded-versioning-concepts).

## Production

See [10. Tags vs. Releases vs. Production Deployments](#10-tags-vs-releases-vs-production-deployments) and [Appendix D](#appendix-d-production-release-and-deployment-details).

## Repository

See [3. Proper Terms](#3-proper-terms) and [5. Create the Local Git Repository](#5-create-the-local-git-repository).

## Semantic Versioning

See [12. Naming and Versioning Recommendations](#12-naming-and-versioning-recommendations) and [Appendix C](#appendix-c-expanded-versioning-concepts).

## Tag

See [3. Proper Terms](#3-proper-terms), [7. Mark the First File Set as v1.0.0](#7-mark-the-first-file-set-as-v100), and [Appendix A](#appendix-a-expanded-git-command-reference).

## Version

See [8. Continue Editing and Mark the Next File Set as v1.1.0](#8-continue-editing-and-mark-the-next-file-set-as-v110) and [12. Naming and Versioning Recommendations](#12-naming-and-versioning-recommendations).

## VS Code

See [11. Using Visual Studio Code](#11-using-visual-studio-code) and [Appendix B](#appendix-b-expanded-vs-code-reference).
