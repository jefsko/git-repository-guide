# Creating a Git Repository and Marking File Sets as Versions

Document version: v1.5.0  
Previous locked version: v1.4.0  
Version status: Locked standalone Markdown version  
Update type: Additive update  
Versioning method: Document metadata only; no Git repository package required  
Future edit policy: Do not overwrite this `v1.5.0` file. Save future changes as a new version, such as `v1.5.1` or `v1.6.0`.  
Current as of: 2026-06-30

Revision note: This `v1.5.0` edition preserves the `v1.4.0` guide and additively incorporates initial commit message vs. commit body guidance, multiple `-m` commit examples, and commit body vs. repository description clarification from the v1.5.0 update brief.

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
- [15. Repository Packaging and Stable Filenames](#15-repository-packaging-and-stable-filenames)
- [16. First-Time Setup vs. Later Updates](#16-first-time-setup-vs-later-updates)
- [17. Branching, Merging, and Rebasing](#17-branching-merging-and-rebasing)
- [18. Git Push Object Counts and Git Objects](#18-git-push-object-counts-and-git-objects)
- [19. Adding, Updating, and Replacing Files](#19-adding-updating-and-replacing-files)
- [20. Fetch, Pull, Merge, Rebase, and Conflict Basics](#20-fetch-pull-merge-rebase-and-conflict-basics)
- [21. File and Folder Change Workflows](#21-file-and-folder-change-workflows)
- [22. Commit Messages, Commit Bodies, and Repository Descriptions](#22-commit-messages-commit-bodies-and-repository-descriptions)
- [Appendix A: Expanded Git Command Reference](#appendix-a-expanded-git-command-reference)
- [Appendix B: Expanded VS Code Reference](#appendix-b-expanded-vs-code-reference)
- [Appendix C: Expanded Versioning Concepts](#appendix-c-expanded-versioning-concepts)
- [Appendix D: Production Release and Deployment Details](#appendix-d-production-release-and-deployment-details)
- [Appendix E: Troubleshooting](#appendix-e-troubleshooting)
- [Appendix F: Knowledge Base and How-To Reference](#appendix-f-knowledge-base-and-how-to-reference)
- [Appendix G: Command Sequences and Workflow Recipes](#appendix-g-command-sequences-and-workflow-recipes)
- [Appendix H: File Update, Merge, and Conflict Scenarios](#appendix-h-file-update-merge-and-conflict-scenarios)
- [Appendix I: File and Folder Operation Scenarios](#appendix-i-file-and-folder-operation-scenarios)
- [Appendix J: Commit Message and Commit Body Examples](#appendix-j-commit-message-and-commit-body-examples)
- [Appendix K: References](#appendix-k-references)
- [Index](#index)

---

## 1. Purpose of This Guide

You already have:

- Git installed.
- A GitHub account.
- A folder of files you want to track.
- A desire to mark one file set as `v1.0.0`, then later mark newer file sets as `v1.1.0`, `v1.2.0`, `v1.3.0`, `v1.4.0`, `v1.5.0`, or another version.

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

Use **repository** for formal explanations and first mentions. After that, **repo** is a common and acceptable abbreviation.

### Remote

A **remote** is a named connection to another copy of the repository, usually on GitHub.

The conventional default remote name is:

```text
origin
```

`origin` is not a branch. It is a local nickname for the remote repository URL.

### Branch

A **branch** is a movable name pointing to a line of work.

The modern common primary branch name is:

```text
main
```

Older repositories may use:

```text
master
```

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

Check status again to confirm what is staged:

```bash
git status
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

## 15. Repository Packaging and Stable Filenames

This guide is meant to become a real Git repository. Once it is in a repository, the active guide file should keep one stable filename:

```text
git-repository-guide.md
```

Do not keep renaming the active guide file for every version, such as:

```text
git-repository-guide-v1.1.0.md
git-repository-guide-v1.2.0.md
git-repository-guide-v1.3.0.md
```

Those names are acceptable for standalone downloads in a chat or file-sharing context, but they are not the best pattern inside the actual repository.

Inside the repository, use Git history to track versions:

```text
commit history
tags
GitHub Releases
CHANGELOG.md
```

The recommended repository structure is:

```text
git-repository-guide/
├─ README.md
├─ CHANGELOG.md
└─ git-repository-guide.md
```

Recommended repository name:

```text
git-repository-guide
```

Recommended GitHub repository description:

```text
A beginner-friendly guide to creating Git repositories and managing versioned file sets
```

Do not add a period to the GitHub description. Treat it like a short label.

### README.md

Use:

```text
README.md
```

The README should be short. It should identify the project, explain what the repository contains, point to the main guide file, list major topics, state the current guide version, and summarize the versioning policy.

GitHub displays a repository README when it exists in expected locations such as the repository root. [R36]

### CHANGELOG.md

Use:

```text
CHANGELOG.md
```

The changelog should summarize notable changes by version. It does not replace Git history, but it gives humans a convenient summary of what changed.

### Version history for this guide

Recommended history:

| Version | Description |
|---|---|
| `v0.1.0` | Original pre-release draft |
| `v1.0.0` | First complete locked baseline |
| `v1.1.0` | Additive expansion with expanded Git reference and Knowledge Base |
| `v1.2.0` | Additive expansion covering repository packaging, push workflows, branch workflows, and Git object-count guidance |
| `v1.3.0` | Additive expansion covering file update workflows, fetch/pull/merge/rebase workflows, merge scenarios, conflict resolution, and Git tooling |
| `v1.4.0` | Additive expansion covering file/folder operations and direct-to-main vs. working-branch push workflows |
| `v1.5.0` | Additive expansion covering commit message/body guidance and initial commit documentation examples |

### Commit messages, tag names, tag messages, and changelog entries

These are related but not the same thing.

| Thing | Example | Purpose |
|---|---|---|
| Commit message | `Expand guide with branch workflow guidance` | Describes what changed in one commit |
| Tag name | `v1.2.0` | Identifies the version marker |
| Tag message | `Version 1.2.0` | Describes the annotated tag |
| Changelog entry | `Additive expansion covering repository packaging, push workflows, branch workflows, and Git object-count guidance` | Human-readable version summary |
| GitHub Release title | `v1.2.0` or `Version 1.2.0` | Title for a GitHub Release page |
| GitHub Release notes | Bulleted summary of changes | Published release summary |

Preferred annotated tag pattern:

```bash
git tag -a v1.2.0 -m "Version 1.2.0"
```

Avoid unnecessary redundancy except when showing what not to do:

```bash
git tag -a v1.2.0 -m "Version v1.2.0"
```

The tag name already has the leading `v`. The tag message does not need to repeat it.

---

## 16. First-Time Setup vs. Later Updates

A common source of confusion is that first-time setup commands are not the same as everyday update commands.

### First-time repository setup

Use this when starting a brand-new local repository and connecting it to GitHub for the first time.

Minimal version:

```bash
git init -b main
git add .
git commit -m "Add original pre-release draft"

git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git push -u origin main

git tag -a v0.1.0 -m "Version 0.1.0"
git push origin v0.1.0
```

Recommended beginner-friendly version:

```bash
git init -b main
git status
git add .
git status
git commit -m "Add original pre-release draft"

git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git remote -v
git push -u origin main

git tag -a v0.1.0 -m "Version 0.1.0"
git push origin v0.1.0
```

The second `git status` is intentional. It lets you confirm exactly what is staged before committing.

### Normal later update without a new version tag

Minimal version:

```bash
git add .
git commit -m "Describe what changed"
git push
```

Recommended version:

```bash
git status
git add .
git status
git commit -m "Describe what changed"
git push
```

No tag command is needed if you are not marking a new version.

### Later update with a new version tag

Minimal version:

```bash
git add .
git commit -m "Describe what changed"
git push

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Recommended version:

```bash
git status
git add .
git status
git commit -m "Describe what changed"
git push

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Example:

```bash
git status
git add .
git status
git commit -m "Expand guide with repository packaging and branch workflow guidance"
git push

git tag -a v1.2.0 -m "Version 1.2.0"
git push origin v1.2.0
```

### Why later updates usually use plain `git push`

The first push usually uses:

```bash
git push -u origin main
```

The `-u` option sets upstream tracking. After that, Git knows that your local `main` branch pushes to `origin/main`, so later branch pushes can usually be:

```bash
git push
```

Use `git push -u origin main` again only when upstream tracking is missing or when setting upstream for a new branch. `--set-upstream` is the long form of `-u`. [R22]

### `git tag`, `git push`, and `git push origin <tag>`

These commands do different things.

```bash
git tag
```

lists local tags.

```bash
git tag -a v1.2.0 -m "Version 1.2.0"
```

creates an annotated tag locally.

```bash
git push
```

pushes commits from the current branch to its configured upstream branch.

```bash
git push origin v1.2.0
```

pushes the specific tag `v1.2.0` to GitHub.

Do not rely on plain `git push` to publish a newly created tag. The clear beginner-friendly pattern is:

```bash
git push
git push origin v1.2.0
```

A useful optional alternative is:

```bash
git push --follow-tags
```

This can push annotated tags reachable from the commits being pushed. [R22]

### Command requirement matrix

| Command | First-time setup | Later update, no tag | Later update with tag | Notes |
|---|---:|---:|---:|---|
| `git init -b main` | Yes | No | No | Creates the local repository. |
| `git status` before `git add` | Recommended | Recommended | Recommended | Shows what changed before staging. |
| `git add .` | Yes | Yes | Yes | Stages changes. |
| `git status` after `git add` | Recommended | Recommended | Recommended | Confirms what is staged. |
| `git commit -m "..."` | Yes | Yes | Yes | Creates a commit. |
| `git remote add origin ...` | Yes, if no remote exists | No | No | Connects the local repository to GitHub. |
| `git remote -v` | Recommended | Optional | Optional | Verifies the remote URL. |
| `git push -u origin main` | Yes, if upstream is not set | Usually no | Usually no | Pushes and sets upstream tracking. |
| `git push` | No after first `-u` push | Yes | Yes | Pushes commits after upstream is set. |
| `git tag -a vX.Y.Z -m "Version X.Y.Z"` | Only if tagging first version | No | Yes | Creates an annotated tag locally. |
| `git push origin vX.Y.Z` | Only if pushing first tag | No | Yes | Publishes the tag. |

---

## 17. Branching, Merging, and Rebasing

The earlier workflow in this guide is intentionally simple and often works directly on `main`.

That is acceptable for a small solo documentation project or beginner practice.

For larger changes, team projects, reviewed work, or safer version-control habits, use a branch.

A safer workflow is:

```text
create a working branch
make changes there
commit the changes
push the branch
merge the branch into main
tag the version from main
```

### `origin`, `main`, and `master`

`origin` is the conventional name for the remote repository.

```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
```

`origin` is not a branch. It is a local nickname for a remote repository URL.

`main` is the modern common name for the primary branch.

```bash
git push -u origin main
```

In that command, `origin` is the remote and `main` is the branch.

`master` is the older traditional default branch name. Many older repositories still use `master`; many newer repositories use `main`.

Recommended policy for this guide:

- Use `origin` as the remote name.
- Use `main` as the primary branch name for new repositories.
- Mention that older repositories may use `master`.
- Do not rename an existing `master` branch casually if scripts, collaborators, branch protections, deployment settings, or documentation depend on it.

Basic rename example:

```bash
git branch -m master main
git push -u origin main
```

Then update GitHub’s default branch setting before deleting the old remote branch. Do not delete the old remote primary branch until the default branch and integrations have been updated.

### What is a branch?

A branch is a movable name pointing to a line of work.

For beginners:

> A branch lets you work on changes separately from the primary version of the project.

Create and switch to a new branch:

```bash
git switch -c update-v1.2.0-guide
```

Older tutorials may use:

```bash
git checkout -b update-v1.2.0-guide
```

Both are common. This guide prefers `git switch` because it is clearer for branch switching. [R28]

Switch branches:

```bash
git switch main
git switch update-v1.2.0-guide
```

List local branches:

```bash
git branch
```

List local and remote-tracking branches:

```bash
git branch -a
```

Push a new branch and set upstream tracking:

```bash
git push -u origin update-v1.2.0-guide
```

### Working branches vs. temporary branches

Git does not technically have a special branch type called a “working branch” or “temporary branch.”

A branch is just a branch.

The labels describe how humans intend to use the branch.

| Informal branch type | Meaning | Example |
|---|---|---|
| Working branch | Branch where active work happens | `update-v1.2.0-guide` |
| Feature branch | Branch for a feature or major update | `add-branching-section` |
| Topic branch | Branch for a focused topic/change | `fix-changelog-format` |
| Temporary branch | Short-lived branch for testing or experiments | `try-rebase-example` |

### Should work happen directly on `main`?

For small solo projects, working directly on `main` can be acceptable.

For team projects, important projects, or changes that need review, use a branch.

| Workflow | Pros | Cons |
|---|---|---|
| Direct to `main` | Simple, fewer commands, good for tiny solo projects | Unfinished work lands on the official branch; less review-friendly |
| Branch-based | Keeps `main` stable, supports review, safer for experiments | More commands and more concepts |

Recommended guide position:

> Learn the direct-to-`main` workflow first as the simplest baseline. Once comfortable, use branches for meaningful work and merge into `main` when ready.

### Branch-based update workflow

Create a working branch:

```bash
git status
git switch -c update-v1.2.0-guide
```

Make changes, then commit and push the branch:

```bash
git status
git add .
git status
git commit -m "Describe what changed"
git push -u origin update-v1.2.0-guide
```

Merge after review or testing:

```bash
git switch main
git pull
git merge update-v1.2.0-guide
git push
```

If the merged result is a new version:

```bash
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Optional cleanup after merge:

```bash
git branch -d update-v1.2.0-guide
git push origin --delete update-v1.2.0-guide
```

### GitHub Pull Request workflow

A Pull Request is a GitHub feature for proposing, reviewing, discussing, and merging changes from one branch into another. [R42]

Typical command-line setup:

```bash
git switch -c update-v1.2.0-guide
git add .
git commit -m "Describe what changed"
git push -u origin update-v1.2.0-guide
```

Then on GitHub:

1. Open a Pull Request from `update-v1.2.0-guide` into `main`.
2. Review the changes.
3. Resolve comments or requested changes.
4. Merge the Pull Request.
5. Pull the updated `main` locally.

After the Pull Request is merged:

```bash
git switch main
git pull
```

If the merged result is a new version:

```bash
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

### What is merging?

Merging combines changes from one branch into another branch.

Common example:

```text
merge update-v1.2.0-guide into main
```

Command example:

```bash
git switch main
git pull
git merge update-v1.2.0-guide
git push
```

Git’s merge documentation describes merging as incorporating changes from named commits into the current branch. [R38]

A fast-forward merge happens when `main` has not changed since the working branch was created. Git can simply move `main` forward.

A merge commit happens when both branches have new commits. Git combines the histories with a new commit.

What can go wrong:

- Merge conflicts.
- Both branches changed the same lines.
- One branch deleted a file while another edited it.
- Files were renamed differently.
- The automatic merge succeeds but the combined result is logically wrong.

Basic conflict workflow:

```bash
git status
```

Open conflicted files and look for markers like:

```text
<<<<<<< HEAD
current branch version
=======
incoming branch version
>>>>>>> branch-name
```

Edit the file so it contains the correct final content.

Then:

```bash
git add conflicted-file.md
git commit
```

Abort the merge if needed:

```bash
git merge --abort
```

Recommended merge practices:

- Start from an up-to-date `main`.
- Keep branches focused.
- Merge smaller changes more frequently.
- Review the diff before merging.
- Run checks or proofread after merging.
- Tag versions only after the final merged result is correct.

Useful commands:

```bash
git diff main..branch-name
git log --oneline --graph --decorate --all
```

### What is rebasing?

Rebasing moves or replays commits from one branch onto another base commit.

Beginner explanation:

> Rebasing takes the work from your branch and re-applies it as if it started from the latest version of another branch.

Example:

```bash
git switch update-v1.2.0-guide
git fetch origin
git rebase origin/main
```

Git’s rebase documentation describes reapplying commits on top of another base tip. [R39]

Rebasing can:

- create a cleaner, more linear history;
- update a private working branch with the latest `main` changes;
- avoid some unnecessary merge commits;
- make the final history easier to read.

Merge vs. rebase:

| Topic | Merge | Rebase |
|---|---|---|
| Basic idea | Combines branches | Replays commits onto a new base |
| History shape | May preserve branching structure | Creates a more linear history |
| Commit IDs | Existing commits stay as they are | Rewritten commits get new IDs |
| Beginner safety | Safer/easier to understand | More powerful but easier to misuse |
| Collaboration | Safe for shared branches | Be careful on shared branches |

Good cases for rebase:

- updating a private branch before merging;
- cleaning up local work before sharing;
- keeping a feature branch current with `main`;
- making history easier to review.

Avoid rebasing commits that other people are already using unless everyone understands and agrees.

Reason:

> Rebase rewrites commit history. Rewritten commits get new commit IDs.

Recommended beginner rule:

> Merge is the safer beginner default. Rebase your own private local branch if useful. Do not rebase shared branches unless you know exactly why you are doing it.

Rebase conflict workflow:

```bash
git status
```

Fix the conflicted files.

Then:

```bash
git add conflicted-file.md
git rebase --continue
```

Abort the rebase if needed:

```bash
git rebase --abort
```

---

## 18. Git Push Object Counts and Git Objects

When Git says something like:

```text
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), done.
```

it is not saying that three project files were pushed.

It is saying that three Git objects were pushed.

For a simple first commit with one file in the repository root, the three objects are commonly:

| Git object | Meaning |
|---|---|
| Blob | The contents of the committed file |
| Tree | The directory snapshot that points to blobs and subtrees |
| Commit | Commit metadata, including author, date, message, parent commit if any, and the tree it points to |

Simple model:

```text
commit object
└─ tree object
   └─ blob object for the file
```

Git stores content and history as objects. A commit points to a tree, and the tree points to file contents stored as blobs. [R3]

### Will Git push always show three objects?

No.

The object count depends on new commits, trees, blobs, tag objects, and what the remote already has.

For a normal first commit with files in the repository root:

```text
objects pushed = 1 commit + 1 tree + 1 blob per unique file content
```

Examples:

| First commit contents | Likely objects pushed |
|---|---|
| 1 file in root | 1 commit + 1 tree + 1 blob = 3 objects |
| 2 different files in root | 1 commit + 1 tree + 2 blobs = 4 objects |
| 3 different files in root | 1 commit + 1 tree + 3 blobs = 5 objects |

Important nuances:

| Situation | Blob behavior |
|---|---|
| Add one new file | Usually one new blob |
| Add two different files | Usually two new blobs |
| Add two files with identical content | Possibly one shared blob |
| Modify one existing file | New blob for the new contents |
| Rename a file without changing content | Usually no new blob |
| Delete a file | No new blob |
| Add files in subfolders | More tree objects may be needed |

If the first commit contains:

```text
README.md
docs/git-repository-guide.md
```

Git may need:

```text
1 commit object
1 root tree object
1 docs/ tree object
2 blob objects
= 5 objects
```

If the commit is already on GitHub and you push only a new annotated tag, Git may push just one tag object because the commit, tree, and blobs are already on the remote.

### How to see file counts instead

To see the actual tracked files in the current commit:

```bash
git ls-tree -r --name-only HEAD
```

`git ls-tree` lists the contents of a tree object. [R37]

To see file-change counts in the latest commit:

```bash
git log --stat --oneline -1
```

To see what changed in the latest commit:

```bash
git show --stat --oneline HEAD
```

To see what files changed before committing:

```bash
git status
```

To see a staged-change summary before committing:

```bash
git diff --cached --stat
```

Mental model:

```text
Files changed = human/project view
Objects pushed = Git storage view
```



---

## 19. Adding, Updating, and Replacing Files

The earlier sections explain the normal Git flow:

```text
edit files
git status
git add
git commit
git push
```

This section makes that flow more explicit for ordinary file work.

The key idea:

> Adding, updating, replacing, deleting, and renaming files are all just different kinds of changes. Git records the next committed snapshot.

### Adding a new file

Suppose the repository already exists and you create a new file:

```text
notes.md
```

Check status:

```bash
git status
```

Git should show `notes.md` as an untracked file.

Stage the new file:

```bash
git add notes.md
```

Check status again:

```bash
git status
```

Commit the new file:

```bash
git commit -m "Add notes file"
```

Push the commit:

```bash
git push
```

In plain English:

> Adding a file means Git did not previously track that path, and now the next commit includes it.

You can also stage all current changes under the current folder:

```bash
git add .
```

Use `git add .` when you intentionally want to stage all current changes. Use a specific path, such as `git add notes.md`, when you want to stage only one file.

### Updating an existing tracked file

Suppose the repository already tracks this file:

```text
guide.md
```

You edit it locally and want the repository to contain the updated version.

Use:

```bash
git status
git add guide.md
git status
git commit -m "Update guide"
git push
```

Git treats this as the same tracked file path with newer content in a newer commit.

### Replacing an existing file with a newer local copy

Suppose this file already exists in the repository:

```text
guide.md
```

Then you copy a newer version over the local file, but the filename and path stay the same:

```text
guide.md
```

Use:

```bash
git status
git add guide.md
git status
git commit -m "Replace guide with updated version"
git push
```

If the path is the same, Git normally treats this as a modification to the existing tracked file. It does not matter whether you edited the file manually or copied a new version over it.

Important:

> Git stores snapshots. It does not think about replacement the same way a file manager does. Git compares the new committed content to the old committed content and records the new repository snapshot.

### Deleting a file

If you want to delete a tracked file, use:

```bash
git status
git rm old-notes.md
git commit -m "Remove old notes file"
git push
```

If you already deleted the file outside Git, stage the deletion:

```bash
git status
git add old-notes.md
git commit -m "Remove old notes file"
git push
```

A deletion is still a change. The next commit records that the file no longer exists in that snapshot.

### Renaming or moving a file

Preferred:

```bash
git mv old-name.md new-name.md
git commit -m "Rename guide file"
git push
```

Alternative:

```bash
mv old-name.md new-name.md
git add old-name.md new-name.md
git commit -m "Rename guide file"
git push
```

Git often detects renames by comparing content between snapshots. A rename is still represented as part of the change from one committed snapshot to the next.

### Why did the updated file just appear without a merge?

If you are the only person changing the repository, or if nobody else changed the remote branch since your last pull or clone, your history is usually linear:

```text
A -- B -- C
```

Where:

- `A` = original commit
- `B` = first update
- `C` = second update

When you push `C`, Git can simply move the remote branch forward.

This is called a fast-forward update.

No merge is needed because there are not two competing lines of history to combine.

The most important rule:

> Updating a file does not automatically mean merging. Merging is about combining different histories, not merely saving a newer local version of a file.

### Does Git check out files like older version-control systems?

Some older version-control systems use an exclusive checkout or locking model:

```text
User A checks out a file.
User B cannot edit or check in that same file until User A checks it back in.
```

Git usually does not work that way.

Git is distributed:

```text
User A has a local clone.
User B has a local clone.
Both can edit the same file locally at the same time.
Git resolves or reports conflicts later when histories are combined.
```

In Git, these terms matter:

| Term | Meaning |
|---|---|
| `git checkout` / `git switch` | Switches branches, commits, or working states. It does not normally lock a file for exclusive editing. |
| `git add` | Stages a file change for the next commit. |
| `git commit` | Saves staged changes into local Git history. |
| `git push` | Sends local commits to the remote repository. |
| `git pull` | Fetches remote changes and integrates them into the current branch. |
| `git merge` | Combines histories. |
| Merge conflict | Git could not safely combine changes automatically. |

`git add` does **not** mean “add this file back to the server.”

It means:

> Stage this file's current content for the next commit.

---

## 20. Fetch, Pull, Merge, Rebase, and Conflict Basics

`git fetch`, `git pull`, `git merge`, and `git rebase` are about synchronizing or combining Git history.

They are not the same as `git add` or `git commit`.

Quick model:

```text
git add      = stage local file content
git commit   = save staged content into local history
git fetch    = download remote history, but do not integrate it yet
git pull     = fetch remote history and integrate it into the current branch
git merge    = combine another branch/history into the current branch
git rebase   = replay current branch commits onto another base
```

### Quick comparison

| Command | What it does | Changes current branch? | Typical use |
|---|---|---:|---|
| `git fetch` | Downloads remote commits, branches, tags, and objects | No | Check what changed remotely before integrating |
| `git pull` | Fetches, then integrates into the current branch | Yes | Update your branch from its upstream |
| `git merge` | Combines another branch/history into the current branch | Yes | Bring a working branch into `main` or integrate fetched history |
| `git rebase` | Replays commits onto a new base | Yes, and rewrites local commit IDs | Update or clean up a private working branch |

Beginner rule:

> Use `git pull` for ordinary “get the latest remote changes” workflows. Use `git fetch` when you want to inspect remote changes before integrating them. Use `git merge` to combine branches. Use `git rebase` carefully, usually only on your own private working branch.

### `git fetch`

`git fetch` downloads remote history and updates remote-tracking branches such as:

```text
origin/main
origin/update-guide
```

It does not automatically change your current local branch.

Beginner wording:

> `git fetch` says, “Go see what changed on GitHub and bring that information down locally, but do not change my current branch yet.”

Common commands:

```bash
git fetch
git fetch origin
git fetch origin main
git fetch --all
git fetch --prune
```

Common optional parts:

| Syntax part | Required? | Meaning |
|---|---:|---|
| `git fetch` | Required | The command. |
| `origin` | Optional | The remote to fetch from. |
| `main` | Optional | A specific branch/ref to fetch. |
| `--all` | Optional | Fetch from all remotes. |
| `--prune` | Optional | Remove stale remote-tracking refs that no longer exist on the remote. |
| `--tags` | Optional | Fetch tags explicitly. |

Use `fetch` when you want to inspect before integrating:

```bash
git fetch origin
git log --oneline --decorate --graph --all
git diff main..origin/main
```

### `git pull`

`git pull` fetches remote changes and integrates them into the current branch.

Conceptually:

```text
git pull = git fetch + integrate
```

By default, that integration is commonly a merge. With `--rebase`, it integrates by rebasing.

Common commands:

```bash
git pull
git pull origin main
git pull --ff-only
git pull --rebase
git pull --no-rebase
```

Common optional parts:

| Syntax part | Required? | Meaning |
|---|---:|---|
| `git pull` | Required | The command. |
| `origin` | Optional | The remote to pull from. |
| `main` | Optional | The branch/ref to pull. |
| `--ff-only` | Optional | Only update if the result can be a fast-forward. |
| `--rebase` | Optional | Fetch, then rebase local commits on top of the remote branch. |
| `--no-rebase` | Optional | Fetch, then merge. |

Ordinary use:

```bash
git switch main
git pull
```

Use this when you want your local `main` to catch up to GitHub.

If your push is rejected because the remote has new commits, `git pull` is often the next beginner-friendly command:

```bash
git pull
git push
```

If conflicts appear, they happen during the integration part of `pull`.

### Push rejection is not the same as a merge conflict

A push rejection may look like this:

```text
! [rejected] main -> main (fetch first)
error: failed to push some refs
hint: Updates were rejected because the remote contains work that you do not have locally.
```

This means:

> The remote branch has commits that your local branch does not have.

That is not yet necessarily a merge conflict.

Next, you integrate the remote work:

```bash
git pull
```

Then one of two things happens:

1. Git integrates the remote changes automatically.
2. Git reports a merge or rebase conflict.

The conflict is discovered during pull, merge, or rebase, not merely because the file was edited.

### `git merge`

`git merge` combines another branch or commit history into your current branch.

Beginner wording:

> `git merge` says, “Take the changes from that branch and integrate them into the branch I am currently on.”

Common commands:

```bash
git merge branch-name
git merge origin/main
git merge --abort
git merge --continue
git merge --no-ff branch-name
git merge --ff-only branch-name
```

Common optional parts:

| Syntax part | Required? | Meaning |
|---|---:|---|
| `git merge` | Required | The command. |
| `branch-name` or commit | Usually required | What to merge into the current branch. |
| `--abort` | Optional recovery mode | Stop the merge and try to return to the pre-merge state. |
| `--continue` | Optional recovery mode | Continue after resolving conflicts. |
| `--no-ff` | Optional | Create a merge commit even if fast-forward is possible. |
| `--ff-only` | Optional | Only merge if fast-forward is possible. |
| `--squash` | Optional/advanced | Stage combined changes without a normal merge commit. |

Common workflow:

```bash
git switch main
git pull
git merge update-guide
git push
```

### `git rebase`

`git rebase` replays commits from one branch onto another base.

Beginner wording:

> `git rebase` says, “Take my local commits and replay them as if I had started from the latest version of another branch.”

Common commands:

```bash
git rebase origin/main
git rebase main
git rebase --continue
git rebase --abort
git rebase --skip
git rebase -i HEAD~3
```

Common optional parts:

| Syntax part | Required? | Meaning |
|---|---:|---|
| `git rebase` | Required | The command. |
| `origin/main` or another upstream | Usually recommended | The new base to replay commits onto. |
| branch name | Optional | Branch to rebase. If omitted, rebases the current branch. |
| `--continue` | Optional recovery mode | Continue after resolving a conflict. |
| `--abort` | Optional recovery mode | Stop rebase and return to the pre-rebase state. |
| `--skip` | Optional recovery mode | Skip the patch/commit that caused the conflict. |
| `-i` / `--interactive` | Optional/advanced | Edit, reorder, squash, or reword commits. |

Common private-branch workflow:

```bash
git switch update-guide
git fetch origin
git rebase origin/main
```

Important warning:

> Rebase rewrites commit IDs. That is why it is powerful, but also why it can confuse collaborators if used on shared history.

Recommended beginner rule:

> Merge is the safer beginner default. Rebase your own private branch if useful. Do not rebase shared branches unless you know exactly why you are doing it.

### When does merging come up?

Merging becomes relevant when there are two histories to combine.

Common examples:

- You are merging a working branch into `main`.
- You pulled from GitHub and your local branch also has commits.
- You opened a pull request and GitHub needs to combine branches.
- Two people changed the same branch from different local clones.
- You fetched remote changes and then manually ran `git merge origin/main`.

Updating a file by yourself is usually just:

```text
edit
add
commit
push
```

Merging appears when Git must combine:

```text
your local history
remote or other branch history
```

### Two users editing the same file does not always create a conflict

If User A edits line 10 and User B edits line 80, Git can often merge automatically.

If User A and User B both edit the same paragraph, Git may report a conflict.

Classic conflict markers look like this:

```text
<<<<<<< HEAD
your current version
=======
incoming version
>>>>>>> branch-name
```

Resolve the file so it contains the correct final content, then stage and continue:

```bash
git status
git add conflicted-file.md
git commit
```

For a conflicted rebase, use:

```bash
git add conflicted-file.md
git rebase --continue
```

Abort if needed:

```bash
git merge --abort
```

or:

```bash
git rebase --abort
```

### Conflict prevention habits

Good habits reduce conflicts:

- Pull before starting work:

```bash
git switch main
git pull
```

- Use short-lived branches.
- Keep changes small and focused.
- Communicate when multiple people edit the same file.
- Split large documents into smaller files when practical.
- Avoid formatting entire files unnecessarily.
- Review diffs before committing.
- Use pull requests for review.
- Merge or rebase working branches regularly.
- Use Git LFS or locking workflows for binary files when appropriate.

### Recommended tools for diffing, merging, and conflict resolution

For this guide, the recommended default is:

```text
VS Code built-in Git tools + VS Code merge editor + integrated terminal
```

Why:

- It is free.
- It is cross-platform.
- It is already used elsewhere in the guide.
- It handles staging, diffs, commits, branches, and merge conflicts.
- It keeps exact Git commands available in the terminal.

Ranked recommendations:

| Rank | Tool | Best for | Pros | Cons |
|---:|---|---|---|---|
| 1 | Visual Studio Code built-in Git and merge editor | Best default for this guide | Free, cross-platform, integrated diff/merge UI, good terminal support | Not as specialized as a dedicated Git client |
| 2 | VS Code + GitLens | Best VS Code enhancement | Strong history, blame, graph, and context features | Some advanced features may require account/sign-in or paid features |
| 3 | Sublime Merge | Best dedicated Git GUI for speed and clarity | Fast, polished, focused Git experience | Separate commercial tool |
| 4 | Visual Studio Git tools | Best for .NET/Visual Studio projects | Integrated with Visual Studio solutions | Heavier than needed for docs-only repos |
| 5 | GitKraken Desktop | Best polished visual Git client | Strong visual history and merge/conflict tooling | Commercial product; may require account/licensing |
| 6 | GitHub Desktop | Best simple GitHub-focused GUI | Beginner-friendly and official GitHub app | Less powerful for advanced merging |
| 7 | Git Extensions | Best open-source Windows-focused Git GUI | Mature, configurable, strong command coverage | Interface can feel less modern |
| 8 | Command line only | Best for precision and documentation | Universal, exact, scriptable | Harder for visual diff/merge conflict resolution |
| 9 | External diff/merge tools such as Beyond Compare, WinMerge, Meld, KDiff3, or Araxis Merge | Specialized comparison needs | Powerful side-by-side comparison | Extra setup and sometimes extra cost |



---

## 21. File and Folder Change Workflows

Section 19 explains the basic file workflow. This section expands that model to include folders, delete-and-replace cases, verification commands, and the practical choice between pushing directly to `main` and pushing a working branch.

The practical rule stays the same:

```text
make a change
verify what Git sees
stage the intended change
verify what is staged
commit
push
```

### Git tracks files and file paths, not empty folders

Git tracks files. A folder appears in the repository because tracked files exist inside it.

Example:

```text
docs/guide.md
```

Git tracks the file path:

```text
docs/guide.md
```

The `docs/` folder appears because a tracked file exists inside it.

If a folder is empty, Git normally does not track it. A common convention is to add a placeholder file:

```text
empty-folder/.gitkeep
```

or:

```text
empty-folder/.keep
```

`.gitkeep` is not a special Git feature. It is just a normal placeholder file that gives Git something to track inside an otherwise-empty folder.

Example:

```bash
mkdir empty-folder
touch empty-folder/.gitkeep
git add empty-folder/.gitkeep
git commit -m "Add empty folder placeholder"
git push
```

Windows PowerShell example:

```powershell
New-Item -ItemType Directory -Path empty-folder
New-Item -ItemType File -Path empty-folder/.gitkeep
git add empty-folder/.gitkeep
git commit -m "Add empty folder placeholder"
git push
```

### Adding a folder with files

Suppose you add this folder:

```text
docs/
├─ guide.md
└─ examples.md
```

Stage the folder path:

```bash
git status
git add docs/
git status
git commit -m "Add docs folder"
git push
```

`git add docs/` stages tracked changes under that folder. Git is not tracking the folder by itself; it is tracking the files inside the folder.

### Updating a tracked file with verification

For a tracked file:

```text
guide.md
```

A careful update workflow is:

```bash
git status
git diff guide.md
git add guide.md
git status
git diff --cached guide.md
git commit -m "Update guide"
git push
```

`git diff guide.md` shows unstaged changes. `git diff --cached guide.md` shows staged changes.

### Drop-in replacing a file with the same path

If you copy a newer file over an existing tracked file and the path stays the same, Git usually treats it like a modification.

Example:

```text
before: docs/guide.md
after:  docs/guide.md
```

Use:

```bash
git status
git diff --stat
git add docs/guide.md
git status
git diff --cached --stat
git commit -m "Replace guide with updated version"
git push
```

Git usually does not care whether the change came from hand-editing, copy/paste, exporting from another tool, or copying a newer file over the old file. Git compares the previous committed snapshot to the new staged snapshot.

### Delete then replace before staging or committing

Suppose you:

1. Delete `docs/guide.md`.
2. Copy a newer file back to `docs/guide.md`.
3. Then run `git status`.

If the final file exists at the same path, Git usually sees the final result as a modification:

```text
modified: docs/guide.md
```

Use:

```bash
git status
git add docs/guide.md
git commit -m "Replace guide with updated version"
git push
```

Git records the final staged snapshot. It does not record every temporary file-manager action you performed locally.

### Delete, commit, then add back later

This is different:

```bash
git rm docs/guide.md
git commit -m "Remove guide"

# Later
git add docs/guide.md
git commit -m "Add replacement guide"
git push
```

Now history contains a commit where the file did not exist, followed by a later commit where a file at that path exists again.

That is different from deleting and replacing the file before the next commit.

### Removing or deleting a file

Preferred Git-aware command:

```bash
git status
git rm old-notes.md
git status
git commit -m "Remove old notes file"
git push
```

If you already deleted the file outside Git, stage the deletion:

```bash
git status
git add old-notes.md
git status
git commit -m "Remove old notes file"
git push
```

You can also use:

```bash
git add -A
```

`git add -A` stages additions, modifications, and deletions across the repository. Use it only when you intend to stage all of those changes.

### Removing or deleting a folder

For a folder with tracked files:

```text
old-docs/
├─ draft.md
└─ notes.md
```

Use:

```bash
git status
git rm -r old-docs/
git status
git commit -m "Remove old docs folder"
git push
```

If you deleted the folder in File Explorer, VS Code, or another tool, stage the deletion:

```bash
git status
git add -A old-docs/
git status
git commit -m "Remove old docs folder"
git push
```

From the repository root, you can stage all additions, modifications, and deletions:

```bash
git add -A
```

### Stop tracking a file or folder but keep it locally

Sometimes you want Git to stop tracking something but keep it on your computer.

For one file:

```bash
git rm --cached local-notes.md
git commit -m "Stop tracking local notes"
git push
```

For a folder:

```bash
git rm -r --cached local-folder/
git commit -m "Stop tracking local folder"
git push
```

Usually also add it to `.gitignore`:

```gitignore
local-notes.md
local-folder/
```

`--cached` removes the file from Git's index but leaves the working copy on disk.

### Moving or renaming a file

Preferred Git-aware command:

```bash
git status
git mv old-name.md new-name.md
git status
git commit -m "Rename guide file"
git push
```

Alternative if you already moved it outside Git:

```bash
mv old-name.md new-name.md
git status
git add old-name.md new-name.md
git status
git commit -m "Rename guide file"
git push
```

PowerShell:

```powershell
Move-Item old-name.md new-name.md
git status
git add old-name.md new-name.md
git status
git commit -m "Rename guide file"
git push
```

`git mv` is usually cleaner because it moves or renames the file and stages the path change in one Git-aware step.

### Moving or renaming a folder

To rename a folder with tracked files:

```bash
git status
git mv old-docs docs
git status
git commit -m "Rename docs folder"
git push
```

Git does not track the folder as an independent object. This stages path changes for tracked files inside the folder.

If you already moved or renamed the folder outside Git:

```bash
mv old-docs docs
git status
git add -A old-docs docs
git status
git commit -m "Rename docs folder"
git push
```

PowerShell:

```powershell
Move-Item old-docs docs
git status
git add -A old-docs docs
git status
git commit -m "Rename docs folder"
git push
```

When in doubt, run:

```bash
git status
git diff --summary
git diff --stat
```

### Multiple ways to move or rename

| Method | Example | What it does | Best use |
|---|---|---|---|
| `git mv old new` | `git mv guide.md docs/guide.md` | Moves/renames and stages in one step | Best default for tracked files |
| Move in file manager, then `git add -A` | Move in VS Code/File Explorer, then `git add -A` | Stages old-path deletions and new-path additions | Good if move already happened |
| Move in file manager, then stage in VS Code | Use Source Control UI | Same idea, but visual | Good for VS Code users |
| Delete old file, add new file | `git rm old`; `git add new` | May appear as delete/add or rename depending on similarity | Use when replacement is intentionally different |
| Copy new file over same path | Overwrite `guide.md`; `git add guide.md` | Treats same path as modified | Best for updated versions with same filename |

### How Git decides whether something was a rename

Git often detects renames by comparing deleted files and added files. A rename is not always stored as a permanent separate event. Many Git commands infer it when showing history or diffs.

Useful commands:

```bash
git status
git diff --summary
git diff --stat
git log --follow -- path/to/file.md
```

`git log --follow -- path/to/file.md` can help follow a file's history across renames.

### Verify what Git thinks happened

Before committing a delete, move, rename, or drop-in replacement, verify what Git sees:

```bash
git status
git diff --stat
git diff --summary
git diff --cached --stat
git diff --cached --summary
```

Use:

- `git status` to see changed, deleted, new, renamed, or staged files;
- `git diff --stat` for a compact unstaged summary;
- `git diff --summary` for create/delete/rename summaries;
- `git diff --cached --stat` after staging;
- `git diff --cached --summary` after staging.

### Pushing directly to `main` vs. pushing a working branch

The guide starts with direct pushes to `main` because that is the simplest way to learn Git.

This is the first-time pattern:

```bash
git push -u origin main
```

After upstream tracking is set, later pushes from `main` usually use:

```bash
git push
```

Conceptually:

```text
local main -> remote main
```

or casually:

```text
main -> origin/main
```

But be precise:

> `main` is your local branch. `origin/main` is your local remote-tracking view of the remote `main` branch. You usually push with `git push origin main` or plain `git push`, not by typing `origin/main` as the destination.

Pushing directly to `main` is reasonable when:

- you are the only person using the repository;
- the repository is a learning project;
- the change is small and low-risk;
- you already reviewed the diff locally;
- `main` is not protected;
- breaking `main` temporarily is not a serious problem.

Risks:

- mistakes go straight to the primary branch;
- `main` may become unstable;
- collaborators may pull unfinished work;
- no pull request review happens first;
- branch protection may reject the push;
- automatic deployment from `main` may be triggered.

For safer real-world work, push a working branch:

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

Conceptually:

```text
local update-guide -> remote update-guide
```

or:

```text
update-guide -> origin/update-guide
```

This publishes the branch to GitHub without changing `main` yet.

Use a working branch when:

- you want review before changing `main`;
- you want to open a pull request;
- the change is large or experimental;
- you are collaborating with others;
- tests or checks should run before merge;
- `main` should stay stable;
- `main` is protected;
- deployment may be triggered from `main`.

Decision table:

| Situation | Recommended push target | Why |
|---|---|---|
| First time pushing a brand-new solo repo | `origin main` | You need to publish the initial primary branch. |
| Tiny solo typo fix | `main`, then `git push` | Simple and low risk. |
| Small private learning project | `main`, then `git push` | Direct workflow is easier to learn. |
| Important documentation update | Working branch | Allows review and comparison before changing `main`. |
| Code change that needs tests | Working branch | Tests/checks can run before merge. |
| Collaborative repository | Working branch | Avoids surprise changes on `main`. |
| Experimental work | Working branch | Easy to abandon or revise. |
| Repository with protected `main` | Working branch | Direct pushes may be blocked. |
| Deployment triggered from `main` | Working branch | Avoid accidental deployment. |
| Version release/tag | Merge to `main`, then tag | Version tags should usually mark the final merged state. |

Recommended rule:

> Start with direct-to-`main` for learning the basics. Use working branches once the project matters, the change is larger, or another person may need to review the work.



---

## 22. Commit Messages, Commit Bodies, and Repository Descriptions

A common source of confusion is the difference between a short commit message, a longer commit body, and the GitHub repository description.

The short answer:

> A Git commit needs a commit message summary. A longer commit body is optional.

A commit message can have two parts:

```text
Short summary line

Optional longer description/body
```

The first line is the **commit message summary**, also called the **commit title**.

The text below the blank line is the optional **commit body**, also called the **commit description**.

Git's `git commit` command supports the `-m` option for providing a commit message from the command line. [R20]

### Simple commit message only

This command is valid and complete:

```bash
git commit -m "docs: add AWS S3 static website quick start guide"
```

It creates a commit with only this short summary:

```text
docs: add AWS S3 static website quick start guide
```

That is enough for Git. You are not missing a second required command.

This is perfectly acceptable when the change is small, obvious, or already explained well in the changed files.

### Commit message with an optional body

To include both a short summary and a longer body from the command line, use multiple `-m` flags:

```bash
git commit -m "docs: add AWS S3 static website quick start guide" -m "Add the initial documentation set for hosting a simple static website on AWS.

Includes the main S3 static website quick start guide, repository README, and changelog. The guide covers a minimal S3-only testing path and a recommended production-style path using CloudFront, AWS Certificate Manager, Cloudflare DNS, and a private S3 bucket."
```

How to read that:

```text
First -m  = commit summary/title
Second -m = commit body/description
```

This pattern:

```bash
git commit -m "Summary" -m "Body"
```

creates this commit message:

```text
Summary

Body
```

Git separates the summary and body with a blank line.

### When to use only the summary

Use only the short commit message when the change is simple or self-explanatory.

Good cases:

- small commits;
- typo fixes;
- clear documentation edits;
- personal projects;
- fast initial setup;
- commits where the diff explains the change well.

Example:

```bash
git commit -m "docs: add AWS S3 static website quick start guide"
```

### When to include a body

Include a commit body when future readers would benefit from context.

Good cases:

- initial project setup;
- major documentation update;
- versioned release;
- architecture decision;
- change where the reason matters;
- change that affects future maintenance;
- change that includes several related files, such as the guide, README, and changelog.

Rule of thumb:

```text
Commit summary = what changed
Commit body    = why it changed, what is included, or anything future readers should know
```

### Commit body vs. repository description

A commit body and a repository description are different things.

| Thing | Where it lives | Purpose |
|---|---|---|
| Commit summary | Git history | Short title for one commit |
| Commit body | Git history | Optional longer explanation for one commit |
| Repository description | GitHub repository page/settings | Short public label for the whole repository |
| README | Repository file | Main project overview and usage documentation |
| CHANGELOG | Repository file | Human-readable version history |

The **commit body** belongs inside Git history.

The **repository description** belongs in the GitHub repository settings or repository header.

Example commit body:

```text
Add the initial documentation set for hosting a simple static website on AWS.

Includes the main S3 static website quick start guide, repository README, and changelog. The guide covers a minimal S3-only testing path and a recommended production-style path using CloudFront, AWS Certificate Manager, Cloudflare DNS, and a private S3 bucket.
```

Example repository description:

```text
Beginner-friendly guide for hosting a static website on AWS using S3, CloudFront, ACM, and Cloudflare DNS
```

The repository description should usually be shorter because it appears near the top of the GitHub repository page.

### Initial commit recommendation

For a well-documented first commit, use the two-part form:

```bash
git commit -m "docs: add AWS S3 static website quick start guide" -m "Add the initial documentation set for hosting a simple static website on AWS.

Includes the main S3 static website quick start guide, repository README, and changelog. The guide covers a minimal S3-only testing path and a recommended production-style path using CloudFront, AWS Certificate Manager, Cloudflare DNS, and a private S3 bucket."
```

For a simpler first commit, this is also valid:

```bash
git commit -m "docs: add AWS S3 static website quick start guide"
```

Both are correct.

The longer version is better when you want Git history to record the purpose and scope of the initial documentation set.


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


### `git commit -m "Summary" -m "Body"`

Purpose:

Creates a commit with a short summary and an optional longer body.

Example:

```bash
git commit -m "docs: add Git repository guide" -m "Add the initial guide, README, and changelog for creating Git repositories and managing versioned file sets."
```

Explanation:

```text
First -m  = commit summary/title
Second -m = commit body/description
```

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


### `git clone`

Purpose:

Copies an existing repository from a remote location to your computer.

Example:

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git
```

With a custom local folder name:

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git FOLDER-NAME
```

A cloned repository usually already has a remote named `origin`. [R34]

### `git fetch`

Purpose:

Downloads remote commits, branches, tags, and required objects without directly merging them into your current branch. [R40]

Example:

```bash
git fetch origin
```

This is often used before rebasing a private working branch:

```bash
git fetch origin
git rebase origin/main
```

### `git merge`

Purpose:

Combines changes from another branch into the current branch. [R38]

Example:

```bash
git switch main
git merge update-v1.2.0-guide
```

### `git pull`

Purpose:

Fetches changes from a remote repository and then integrates them into the current branch. Git’s documentation describes `git pull` as running `git fetch` first, then integrating the fetched branch into the current branch. [R41]

Example:

```bash
git pull
```

### `git rebase`

Purpose:

Replays commits from the current branch onto another base. [R39]

Example:

```bash
git switch update-v1.2.0-guide
git fetch origin
git rebase origin/main
```

Use carefully because rebasing rewrites commit IDs.

### `git ls-tree`

Purpose:

Lists the contents of a tree object, which is useful for seeing tracked files in a commit. [R37]

Example:

```bash
git ls-tree -r --name-only HEAD
```

### `git diff --cached --stat`

Purpose:

Shows a compact summary of staged changes before committing.

Example:

```bash
git diff --cached --stat
```


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


### `git clone`

See [Appendix G](#appendix-g-command-sequences-and-workflow-recipes) for clone workflow examples.

### `git fetch`

Use this to download remote updates without immediately integrating them.

### `git merge`

Use this to combine another branch into the current branch.

### `git pull`

Use this to fetch and integrate remote changes into the current branch.

### `git rebase`

Use this carefully to replay commits onto another base.

### `git ls-tree`

Use this to inspect tracked files in a commit or tree.


### `git rm`

Purpose:

Stages the removal of a tracked file.

Example:

```bash
git rm old-notes.md
git commit -m "Remove old notes file"
```

### `git mv`

Purpose:

Moves or renames a tracked file and stages that change.

Example:

```bash
git mv old-name.md new-name.md
git commit -m "Rename guide file"
```

### `git pull --ff-only`

Purpose:

Updates the current branch only if Git can fast-forward it. If histories have diverged, Git stops instead of creating a merge commit.

Example:

```bash
git pull --ff-only
```

### `git merge --continue`

Purpose:

Continues a merge after conflicts have been resolved and staged.

Example:

```bash
git add conflicted-file.md
git merge --continue
```

### `git rebase --continue`

Purpose:

Continues a rebase after conflicts have been resolved and staged.

Example:

```bash
git add conflicted-file.md
git rebase --continue
```

### `git mergetool`

Purpose:

Opens the configured merge tool for resolving conflicts. [R43]

Example:

```bash
git mergetool
```



### `git add -A`

Purpose:

Stages additions, modifications, and deletions across the repository.

Example:

```bash
git add -A
```

Use it carefully. It can stage more than you intended if unrelated files changed.

### `git rm -r`

Purpose:

Removes tracked files under a folder and stages the deletions.

Example:

```bash
git rm -r old-docs/
```

### `git rm --cached`

Purpose:

Stops tracking a file while keeping the local working copy on disk.

Example:

```bash
git rm --cached local-notes.md
```

For a folder:

```bash
git rm -r --cached local-folder/
```

### `git mv`

Purpose:

Moves or renames a tracked file or folder path and stages the path change.

Example:

```bash
git mv old-name.md new-name.md
```

Folder example:

```bash
git mv old-docs docs
```

### `git diff --summary`

Purpose:

Shows a summary of creates, deletes, renames, and mode changes.

Example:

```bash
git diff --summary
```

After staging:

```bash
git diff --cached --summary
```

### `git log --follow`

Purpose:

Follows file history across renames when possible.

Example:

```bash
git log --follow -- path/to/file.md
```


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


## B.6 Merge conflict support

VS Code supports reviewing changes, resolving merge conflicts, and using a 3-way merge editor. [R47]

For this guide, VS Code is the recommended default tool for merge conflicts because it combines:

- file editing;
- Source Control;
- inline diffing;
- merge conflict UI;
- integrated terminal commands.

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



## F.27 Should I keep renaming the guide file with each version?

Usually, no.

Inside a Git repository, use one stable filename, such as:

```text
git-repository-guide.md
```

Use Git commits, tags, GitHub Releases, and `CHANGELOG.md` to track versions.

Standalone downloads can include version numbers, but the active repository file should usually stay stable.

## F.28 What should I name this repository?

Recommended:

```text
git-repository-guide
```

That name is broad enough to cover first-time repository setup, GitHub setup, tags, versioned file sets, and common Git questions.

## F.29 What should the GitHub repository description be?

Recommended:

```text
A beginner-friendly guide to creating Git repositories and managing versioned file sets
```

Do not include a period at the end. GitHub descriptions are often short label-style phrases.

## F.30 Should I create a README?

Yes.

GitHub can display a README automatically when it exists, but GitHub does not write the meaningful project explanation for you. Create `README.md` yourself. [R36]

## F.31 Should I create a CHANGELOG?

Yes.

Use `CHANGELOG.md` to summarize notable changes by version.

The changelog does not replace commit history. It gives humans a clean version-by-version summary.

## F.32 Should the active file include the version number?

Usually, no.

Inside the repository, use:

```text
git-repository-guide.md
```

Do not use the active filename as the version tracker.

Use tags, releases, metadata, and `CHANGELOG.md` for version tracking.

## F.33 What version should a pre-release draft use?

For the first meaningful early draft, use:

```text
v0.1.0
```

That communicates “pre-1.0, but meaningful enough to label.”

## F.34 Are version-history descriptions commit messages?

No.

This is a version-history or changelog description:

```text
v1.1.0 = Additive expansion with expanded Git reference and Knowledge Base
```

A better commit message is:

```text
Expand guide with Git reference and Knowledge Base
```

## F.35 What should tag messages look like?

Preferred:

```bash
git tag -a v1.2.0 -m "Version 1.2.0"
```

Less preferred because it repeats the leading `v`:

```bash
git tag -a v1.2.0 -m "Version v1.2.0"
```

The tag name includes `v`. The message can simply say `Version 1.2.0`.

## F.36 Why did `git push` say “Enumerating objects: 3” when I committed one file?

Git was reporting Git objects, not project files.

A simple one-file first commit commonly involves:

```text
1 commit object
1 tree object
1 blob object
= 3 objects
```

See [Section 18](#18-git-push-object-counts-and-git-objects).

## F.37 Will Git push always say 3 objects?

No.

The object count depends on new commits, trees, blobs, tag objects, and what the remote already has.

## F.38 When does Git show file counts?

Use commands such as:

```bash
git status
git diff --cached --stat
git log --stat --oneline -1
git show --stat --oneline HEAD
```

Those commands are better for file-change summaries than `git push` output.

## F.39 What is `origin`?

`origin` is the conventional name for the remote repository.

It is not a branch.

## F.40 What is `main`?

`main` is the modern common name for the primary branch.

For new repositories, this guide recommends `main`.

## F.41 What is `master`?

`master` is the older traditional primary branch name.

Older repositories may still use it.

## F.42 Should I rename `master` to `main`?

For new repositories, use `main`.

For existing repositories, renaming can be reasonable, but be careful. Check for scripts, CI/CD workflows, branch protection rules, documentation, deployment settings, and collaborators before changing it.

## F.43 Should I work directly on `main`?

For a tiny solo project, it can be acceptable.

For safer habits, larger changes, shared work, or reviewed work, create a working branch, commit there, and merge into `main` when ready.

## F.44 What is a working branch?

A working branch is an ordinary Git branch used for active work.

Git does not technically treat it differently from any other branch.

## F.45 What is a temporary branch?

A temporary branch is an ordinary branch intended for short-lived work or experiments.

## F.46 What is merging?

Merging combines changes from one branch into another.

Example:

```bash
git switch main
git merge update-v1.2.0-guide
```

## F.47 What is a merge conflict?

A merge conflict happens when Git cannot automatically combine changes.

This often happens when two branches edit the same lines differently.

## F.48 What is rebasing?

Rebasing replays commits from one branch onto another base commit.

It is useful, but it rewrites commit IDs, so use it carefully.

## F.49 Should beginners merge or rebase?

Prefer merging as the safer beginner default.

Learn rebasing later for private branches and cleaner history.

## F.50 Should this guide say “repo” or “repository”?

Use `repository` for formal explanations and first mentions.

Introduce `repo` as a common abbreviation:

```text
A Git repository, often shortened to repo, is the folder/project that Git tracks.
```

After that, both are acceptable depending on clarity and tone.



---


## F.51 Is adding a file the same as checking it in?

No.

In Git:

```text
git add    = stage the file
git commit = save the staged change in local history
git push   = send the commit to the remote
```

## F.52 If I replace a file locally, is it still the same file?

If the path is the same, Git normally treats it as the same tracked file path with changed contents.

Example:

```text
guide.md before
guide.md after
```

The next commit records the new content.

## F.53 Why did the updated file just appear on GitHub?

Because your push was a fast-forward update. The remote branch had not diverged from your local branch.

## F.54 Why did Git not ask me to merge?

Because there was no competing history to combine.

Merging is about combining histories, not merely saving a newer local file.

## F.55 When does merging happen?

Merging happens when Git combines histories, commonly during:

```text
git pull
git merge
pull request merge
some rebase workflows
```

## F.56 Is `git add` checking the file back into the repository?

No.

`git add` stages the current file content for the next commit.

## F.57 Can two people edit the same file?

Yes.

Git usually allows it. Conflicts are detected later when histories are combined.

## F.58 Does two people editing the same file always cause a conflict?

No.

If the edits are in different parts of the file, Git may merge them automatically.

## F.59 What causes a merge conflict?

A merge conflict happens when Git cannot safely combine changes automatically.

The classic case is two histories changing the same lines in the same file.

## F.60 What should I do before resolving a conflict?

Run:

```bash
git status
```

Then inspect the conflicted files and decide the correct final content.

## F.61 What if I am not sure which version is correct?

Ask the other person or review the project intent. Do not blindly choose “ours” or “theirs.”

## F.62 What is `git fetch`?

`git fetch` downloads remote history and updates remote-tracking branches, but does not integrate those changes into your current branch.

## F.63 What is `git pull`?

`git pull` fetches remote changes and integrates them into your current branch.

## F.64 Is `git pull` the same as `git fetch` plus `git merge`?

Conceptually, often yes.

By default, `git pull` fetches first, then integrates, commonly by merge. With `--rebase`, it fetches and rebases instead.

## F.65 When should I use `git fetch` instead of `git pull`?

Use `git fetch` when you want to inspect remote changes before integrating them.

## F.66 Should beginners use merge or rebase?

Use merge as the safer beginner default. Use rebase later, mostly on private branches.

## F.67 Is a push rejection the same as a merge conflict?

No.

A push rejection means the remote has commits you do not have locally. A merge conflict may happen later when you pull, merge, or rebase.

## F.68 What tool should I use to resolve merge conflicts?

Start with VS Code's built-in Git tools and merge editor.

Use a dedicated Git GUI later if you want a more specialized visual Git experience.



## F.69 Does Git track folders?

Git tracks files and file paths. Empty folders are not tracked unless they contain a tracked placeholder file such as `.gitkeep`.

## F.70 How do I add a folder to Git?

Add files inside the folder:

```bash
git add docs/
git commit -m "Add docs folder"
git push
```

## F.71 How do I add an empty folder?

Add a placeholder file:

```bash
mkdir empty-folder
touch empty-folder/.gitkeep
git add empty-folder/.gitkeep
git commit -m "Add empty folder placeholder"
git push
```

## F.72 How do I delete a folder from Git?

Use:

```bash
git rm -r old-folder/
git commit -m "Remove old folder"
git push
```

## F.73 How do I stop tracking a file but keep it locally?

Use:

```bash
git rm --cached local-file.txt
git commit -m "Stop tracking local file"
```

Then add it to `.gitignore` if needed.

## F.74 How do I stop tracking a folder but keep it locally?

Use:

```bash
git rm -r --cached local-folder/
git commit -m "Stop tracking local folder"
```

Then add it to `.gitignore` if needed.

## F.75 Is moving a file different from renaming it?

In Git, both are path changes. A rename is a move where only the filename changes. A move may also change folders.

## F.76 Is `git mv` required?

No, but it is often the cleanest command for tracked files because it moves or renames the file and stages the change in one step.

## F.77 What if I already moved the file in File Explorer or VS Code?

Use:

```bash
git status
git add -A
git status
git commit -m "Move files"
```

or stage the old and new paths specifically.

## F.78 If I delete and replace a file before committing, does Git remember both actions?

No. Git records the final staged snapshot, not every intermediate local action.

## F.79 If I delete and commit, then add a replacement later, is that different?

Yes. The history now has one commit where the file was removed and a later commit where a file at that path was added again.

## F.80 Should I push directly to `main`?

Sometimes. It is acceptable for first-time setup, solo learning, tiny changes, and low-risk private projects.

## F.81 When should I avoid pushing directly to `main`?

Avoid direct pushes to `main` for shared repositories, important projects, protected branches, deployment-triggering branches, large changes, and changes needing review.

## F.82 What does `git push -u origin main` do?

It pushes local `main` to the remote named `origin` and sets upstream tracking so later `git push` and `git pull` can infer the branch.

## F.83 What does `git push -u origin update-guide` do?

It pushes your local `update-guide` branch to the remote named `origin` and sets upstream tracking for that branch.

## F.84 Is `origin/main` the same as `main`?

No.

`main` is your local branch. `origin/main` is your local remote-tracking reference representing the last fetched state of the remote `main` branch.

## F.85 Should I tag on a working branch or on `main`?

Usually tag on `main` after the working branch has been merged and the final result is correct.

## F.86 Is a remote working branch permanent?

No. It can be deleted after the pull request is merged or the work is abandoned.



## F.87 Do I need a commit body?

No.

A Git commit needs a commit message summary. A longer commit body is optional.

## F.88 What is the difference between a commit message and commit body?

The commit message summary is the first line. The commit body is the optional longer explanation below a blank line.

## F.89 Is the commit summary the same as the commit title?

Yes. People often use commit summary, commit title, and short commit message to mean the first line of the commit message.

## F.90 How do I create a commit with both a summary and body?

Use multiple `-m` flags:

```bash
git commit -m "Summary" -m "Body"
```

## F.91 What does the first `-m` mean?

The first `-m` provides the short commit summary or title.

## F.92 What does the second `-m` mean?

The second `-m` provides the optional longer commit body or description.

## F.93 Is a repository description the same as a commit body?

No.

The repository description appears on the GitHub repository page. The commit body is stored in Git history for one commit.

## F.94 Should the initial commit have a body?

It is optional.

A body is useful when the first commit establishes the project structure, documentation purpose, or important context for future readers.

## F.95 When is a one-line commit enough?

A one-line commit is enough for small, obvious, or self-explanatory changes.

## F.96 When should I include a commit body?

Include a body when the reason, scope, or context of the change matters.

Good examples include initial project setup, major documentation updates, architecture decisions, versioned releases, and changes that affect future maintenance.

## F.97 Does the README replace the commit body?

No.

The README explains the project. The commit body explains one commit.

## F.98 Does the CHANGELOG replace the commit body?

No.

The changelog summarizes notable changes by version. The commit body explains a specific commit when extra context is useful.

## F.99 What is the practical rule for commit summaries and bodies?

Use this rule:

```text
Commit summary = what changed
Commit body    = why it changed, what is included, or anything future readers should know
```

## F.100 What is a good commit message for adding this Git guide?

A concise option is:

```bash
git commit -m "docs: add Git repository guide"
```

A more documented option is:

```bash
git commit -m "docs: add Git repository guide" -m "Add the initial guide, README, and changelog for creating Git repositories and managing versioned file sets."
```


# Appendix G: Command Sequences and Workflow Recipes

This appendix is intentionally workflow-oriented.

It answers:

> “What commands do I run, and in what order?”

For explanations of individual commands, see [Appendix A](#appendix-a-expanded-git-command-reference).

## G.1 Variables used in command examples

| Placeholder | Meaning | Example |
|---|---|---|
| `YOUR-USERNAME` | GitHub username or organization | `jefsko` |
| `YOUR-REPO` | Repository name | `git-repository-guide` |
| `origin` | Conventional remote name | `origin` |
| `main` | Primary branch name | `main` |
| `master` | Older primary branch name | `master` |
| `vX.Y.Z` | Version tag placeholder | `v1.2.0` |
| `X.Y.Z` | Version number without leading `v` | `1.2.0` |
| `work-branch-name` | Branch for active work | `update-v1.2.0-guide` |
| `"Describe what changed"` | Commit message | `"Add branch workflow guidance"` |

## G.2 Common options used in command examples

| Option | Used in | Meaning |
|---|---|---|
| `-b main` | `git init -b main` | Creates the repository using `main` as the initial branch name. |
| `-m "message"` | `git commit -m`, `git tag -m` | Supplies the message inline. |
| `-a` | `git tag -a` | Creates an annotated tag. |
| `-u` | `git push -u origin main` | Sets upstream tracking. |
| `--set-upstream` | `git push --set-upstream origin main` | Long form of `-u`. |
| `--follow-tags` | `git push --follow-tags` | Pushes annotated tags reachable from pushed commits. |
| `-d` | `git branch -d branch-name` | Deletes a local branch if safely merged. |
| `-D` | `git branch -D branch-name` | Force-deletes a local branch. Use carefully. |
| `--delete` | `git push origin --delete branch-name` | Deletes a remote branch. |

## G.3 New repository, minimal setup with initial tag

```bash
git init -b main
git add .
git commit -m "Add original pre-release draft"

git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git push -u origin main

git tag -a v0.1.0 -m "Version 0.1.0"
git push origin v0.1.0
```

## G.4 New repository, recommended setup with initial tag

```bash
git init -b main
git status
git add .
git status
git commit -m "Add original pre-release draft"

git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git remote -v
git push -u origin main

git tag -a v0.1.0 -m "Version 0.1.0"
git push origin v0.1.0
```

## G.5 Existing local repository, minimal later update

```bash
git add .
git commit -m "Describe what changed"
git push
```

## G.6 Existing local repository, recommended later update

```bash
git status
git add .
git status
git commit -m "Describe what changed"
git push
```

## G.7 Existing local repository, later update with new version tag

```bash
git status
git add .
git status
git commit -m "Describe what changed"
git push

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

## G.8 Existing remote repository, clone first

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git
cd YOUR-REPO
```

With a custom local folder name:

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git FOLDER-NAME
cd FOLDER-NAME
```

Then use the normal later update workflow:

```bash
git status
git add .
git status
git commit -m "Describe what changed"
git push
```

A cloned repository already has a remote named `origin`, so `git remote add origin ...` is not needed after cloning. [R34]

## G.9 Branch-based workflow

```bash
git status
git switch -c work-branch-name

git status
git add .
git status
git commit -m "Describe what changed"
git push -u origin work-branch-name
```

Then merge:

```bash
git switch main
git pull
git merge work-branch-name
git push
```

If the merged result is a new version:

```bash
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Optional cleanup:

```bash
git branch -d work-branch-name
git push origin --delete work-branch-name
```

## G.10 Pull Request workflow

```bash
git switch -c work-branch-name
git add .
git commit -m "Describe what changed"
git push -u origin work-branch-name
```

Then open a Pull Request on GitHub from `work-branch-name` into `main`.

After the Pull Request is merged:

```bash
git switch main
git pull
```

If the merged result is a new version:

```bash
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

## G.11 Merge workflow

```bash
git switch main
git pull
git merge branch-name
git push
```

If there is a conflict:

```bash
git status
```

Fix the conflicted files, then:

```bash
git add conflicted-file.md
git commit
```

Abort if needed:

```bash
git merge --abort
```

## G.12 Rebase workflow for a private branch

```bash
git switch work-branch-name
git fetch origin
git rebase origin/main
```

If there is a conflict:

```bash
git status
```

Fix the conflicted files, then:

```bash
git add conflicted-file.md
git rebase --continue
```

Abort if needed:

```bash
git rebase --abort
```

## G.13 Inspect files, changes, and Git objects

Tracked files in the current commit:

```bash
git ls-tree -r --name-only HEAD
```

Commit history with file-change statistics:

```bash
git log --stat --oneline
```

Latest commit with file-change statistics:

```bash
git log --stat --oneline -1
```

Object IDs and paths:

```bash
git rev-list --objects --all
```

Latest commit details:

```bash
git show --stat --oneline HEAD
```

Staged-change summary before committing:

```bash
git diff --cached --stat
```



---

# Appendix H: File Update, Merge, and Conflict Scenarios

This appendix expands the main guide with detailed scenarios.

The goal is to make the difference clear between:

```text
updating a file
adding a file
replacing a file
pushing a commit
pulling remote work
merging histories
resolving merge conflicts
```

## H.1 Scenario A: one user adds a new file

Starting state:

```text
remote/main: A
local/main:  A
```

You create:

```text
notes.md
```

Commands:

```bash
git status
git add notes.md
git status
git commit -m "Add notes file"
git push
```

Result:

```text
remote/main: A -- B
```

No merge conflict.

Why:

> Nobody else changed the remote branch. Git can move the branch forward.

## H.2 Scenario B: one user updates an existing file

Starting state:

```text
remote/main: A
local/main:  A
```

You edit:

```text
guide.md
```

Commands:

```bash
git status
git add guide.md
git status
git commit -m "Update guide"
git push
```

Result:

```text
remote/main: A -- B
```

No merge conflict.

Why:

> This is the same tracked file path with newer content in a newer commit.

## H.3 Scenario C: one user replaces an existing file with the same filename

Starting state:

```text
guide.md exists in commit A
```

You copy a newer local file over the old local file:

```text
guide.md
```

Commands:

```bash
git status
git add guide.md
git status
git commit -m "Replace guide with updated version"
git push
```

Result:

```text
remote/main: A -- B
```

No merge conflict.

Why:

> Git sees a tracked file path with changed content. Since there is no competing remote update, Git commits and pushes normally.

## H.4 Scenario D: two users edit different files

Starting state:

```text
remote/main: A
User A local: A
User B local: A
```

User A edits:

```text
chapter-1.md
```

User A commits and pushes:

```bash
git add chapter-1.md
git commit -m "Update chapter 1"
git push
```

Remote becomes:

```text
remote/main: A -- B
```

User B edits:

```text
chapter-2.md
```

User B commits locally:

```bash
git add chapter-2.md
git commit -m "Update chapter 2"
```

User B tries:

```bash
git push
```

Possible result:

```text
rejected because remote contains work that you do not have
```

User B should run:

```bash
git pull
```

If there is no conflict, Git integrates User A's change and User B can push:

```bash
git push
```

Why no conflict:

> The users changed different files, so Git can usually combine the changes automatically.

Important distinction:

> User B may still have to pull before pushing, but that is not necessarily a merge conflict. It may just be Git requiring User B to include the remote commit before pushing.

## H.5 Scenario E: two users edit different lines in the same file

Starting state:

```text
remote/main: A
User A local: A
User B local: A
```

Both edit:

```text
guide.md
```

User A edits line 10.

User B edits line 80.

User A pushes first:

```text
remote/main: A -- B
```

User B commits locally:

```text
User B local: A -- C
```

User B pushes and gets rejected because remote has `B`.

User B runs:

```bash
git pull
```

Possible result:

> Git automatically merges because the changes are in different parts of the file.

Then User B pushes:

```bash
git push
```

No manual conflict resolution may be needed.

Key wording:

> Two users editing the same file does not always mean a conflict. Git may merge automatically if the edits do not overlap.

## H.6 Scenario F: two users edit the same lines in the same file

Starting state:

```text
remote/main: A
User A local: A
User B local: A
```

Both edit the same paragraph in:

```text
guide.md
```

User A pushes first:

```text
remote/main: A -- B
```

User B commits locally:

```text
User B local: A -- C
```

User B tries:

```bash
git push
```

Push is rejected because the remote has new work.

User B runs:

```bash
git pull
```

Git tries to merge `B` and `C`, but cannot safely combine the same changed lines.

Conflict markers appear:

```text
<<<<<<< HEAD
User B's local version
=======
User A's remote version
>>>>>>> origin/main
```

User B must edit the file to the correct final version.

Then:

```bash
git add guide.md
git commit
git push
```

Key wording:

> This is the classic merge conflict scenario: two histories changed overlapping parts of the same file.

## H.7 Scenario G: one user deletes a file while another edits it

Starting state:

```text
remote/main: A
User A local: A
User B local: A
```

User A deletes:

```text
old-guide.md
```

User B edits:

```text
old-guide.md
```

When histories are combined, Git may report a delete/modify conflict.

Resolution options:

1. Keep the deletion.
2. Keep the edited file.
3. Restore part of the file elsewhere.
4. Rename the edited file.
5. Ask the team which intent is correct.

If the file should remain, stage the resolved file:

```bash
git status
git add old-guide.md
git commit
```

If the file should remain deleted:

```bash
git rm old-guide.md
git commit
```

## H.8 Scenario H: both users add a file with the same name

Example:

```text
User A adds notes.md
User B also adds notes.md
```

If the file contents differ, Git may report an add/add conflict.

Resolution options:

1. Keep User A's version.
2. Keep User B's version.
3. Combine both.
4. Rename one file.
5. Create two separate files.

## H.9 Scenario I: one user renames a file while another edits it

Example:

```text
User A renames guide.md to git-guide.md
User B edits guide.md
```

Git may detect the rename and apply User B's edit to the renamed file, or it may need help if the file changed heavily.

Resolution options:

1. Keep the rename and include the edit.
2. Undo the rename.
3. Keep both files temporarily and reconcile manually.
4. Use a merge tool to inspect both sides.

## H.10 Scenario J: binary files

Binary files include:

```text
images
PDFs
Word documents
compiled assets
some design files
```

Git usually cannot merge binary files line-by-line.

If two users change the same binary file, resolution often means choosing one version or manually recreating a combined file outside Git.

For frequently edited binary files, consider Git LFS, locking workflows, or clearer team coordination. [R54]

## H.11 Types of merge conflicts

| Conflict type | Example | Typical resolution |
|---|---|---|
| Same-line edit | Two users edit the same sentence | Manually choose or combine text |
| Nearby edit | Two users edit adjacent paragraphs | Review context carefully |
| Different-file changes | User A edits A.md, User B edits B.md | Usually auto-merges |
| Same file, different lines | User A edits top, User B edits bottom | Usually auto-merges, but review |
| Delete/modify | One deletes file, one edits it | Decide whether file should exist |
| Add/add | Two users create same filename differently | Combine, choose one, or rename |
| Rename/edit | One renames, one edits old path | Keep rename and apply edit, or decide manually |
| Rename/rename | Two users rename same file differently | Pick final name |
| Binary conflict | Two users edit same image/PDF/DOCX | Choose one, manually combine, or coordinate |
| Semantic/logical conflict | Git merges text cleanly but meaning is wrong | Review, test, and proofread manually |

Not all bad merges produce visible conflict markers. Git can merge text successfully while still producing a logically wrong document or program. Always review important merges.

## H.12 Ways to reduce merge conflicts

- Pull before starting work:

```bash
git switch main
git pull
```

- Use short-lived branches.
- Keep changes small and focused.
- Avoid long-running branches when possible.
- Communicate when editing the same file.
- Split large documents into multiple files when practical.
- Avoid multiple people editing generated files.
- Avoid repeatedly reformatting entire files.
- Commit logical chunks.
- Use pull requests for review.
- Merge or rebase your branch regularly.
- Use Git LFS or locking for binary files when appropriate. [R54]
- Review diffs before committing.

## H.13 Ways to resolve merge conflicts

### Manual text editing

Use the conflict markers:

```text
<<<<<<< HEAD
your current version
=======
incoming version
>>>>>>> branch-name
```

Edit to the correct final content.

Then:

```bash
git add conflicted-file.md
git commit
```

### VS Code merge editor

VS Code supports inline conflict actions and a 3-way merge editor. [R47]

This is the recommended default for most readers of this guide.

### Dedicated Git GUI

A dedicated Git GUI can make history, staging, diffing, and conflicts easier to visualize.

Examples:

- Sublime Merge [R50]
- GitKraken Desktop [R52]
- Git Extensions [R51]
- GitHub Desktop [R49]

### Git mergetool

Use:

```bash
git mergetool
```

This opens the configured merge tool. [R43]

### Choose one side

Sometimes one side is clearly correct.

Keep the current branch version:

```bash
git checkout --ours conflicted-file.md
git add conflicted-file.md
git commit
```

Keep the incoming version:

```bash
git checkout --theirs conflicted-file.md
git add conflicted-file.md
git commit
```

Use `--ours` and `--theirs` carefully. Their meaning can feel reversed during rebase compared with merge.

### Abort and try again

Abort a merge:

```bash
git merge --abort
```

Abort a rebase:

```bash
git rebase --abort
```

Then inspect, pull, coordinate, or retry.

### Resolve on GitHub

GitHub can resolve some simple line-based conflicts in the web UI. More complex conflicts must be resolved locally. [R45] [R46]

### Ask before resolving

For team work:

> If the conflict involves another person's intent, ask them before guessing.

## H.14 Fetch, pull, merge, and rebase decision guide

### I just want the latest remote changes on my current branch

Use:

```bash
git pull
```

If you want to avoid automatic merge commits:

```bash
git pull --ff-only
```

### I want to see what changed on GitHub before integrating

Use:

```bash
git fetch origin
git log --oneline --decorate --graph --all
git diff main..origin/main
```

Then decide whether to merge or rebase.

### I want to combine my working branch into `main`

Use:

```bash
git switch main
git pull
git merge work-branch-name
git push
```

### I want to update my private working branch with the latest `main`

Use:

```bash
git switch work-branch-name
git fetch origin
git rebase origin/main
```

Safer beginner alternative:

```bash
git switch work-branch-name
git fetch origin
git merge origin/main
```

### My push was rejected because the remote has new commits

Simple beginner path:

```bash
git pull
git push
```

More careful path:

```bash
git fetch origin
git log --oneline --decorate --graph --all
git diff main..origin/main
```

Then:

```bash
git merge origin/main
```

Or, for a private branch:

```bash
git rebase origin/main
```

### My pull request branch is out of date

Beginner merge-based path:

```bash
git switch work-branch-name
git fetch origin
git merge origin/main
git push
```

Linear-history path:

```bash
git switch work-branch-name
git fetch origin
git rebase origin/main
git push --force-with-lease
```

`git push --force-with-lease` is safer than plain `--force`, but it is still a history-rewriting push. Do not use it casually.

## H.15 Diff, comparison, merge, and conflict-resolution tools

Recommended ranking for this guide:

| Rank | Tool | Best for | Pros | Cons |
|---:|---|---|---|---|
| 1 | Visual Studio Code built-in Git and merge editor | Best default for this guide | Free, cross-platform, integrated diff/merge UI, good terminal support | Not as specialized as a dedicated Git client |
| 2 | VS Code + GitLens | Best VS Code enhancement | Strong history, blame, graph, and context features | Some advanced features may require account/sign-in or paid features |
| 3 | Sublime Merge | Best dedicated Git GUI for speed and clarity | Fast, polished, focused Git experience | Separate commercial tool |
| 4 | Visual Studio Git tools | Best for .NET/Visual Studio projects | Integrated with Visual Studio solutions | Heavier than needed for docs-only repositories |
| 5 | GitKraken Desktop | Best polished visual Git client | Strong visual history and merge/conflict tooling | Commercial product; may require account/licensing |
| 6 | GitHub Desktop | Best simple GitHub-focused GUI | Beginner-friendly and official GitHub app | Less powerful for advanced merging |
| 7 | Git Extensions | Best open-source Windows-focused Git GUI | Mature, configurable, strong command coverage | Interface can feel less modern |
| 8 | Command line only | Best for precision and documentation | Universal, exact, scriptable | Harder for visual diff/merge conflict resolution |
| 9 | External diff/merge tools such as Beyond Compare, WinMerge, Meld, KDiff3, or Araxis Merge | Specialized comparison needs | Powerful side-by-side comparison | Extra setup and sometimes extra cost |

Best default recommendation:

> Use VS Code built-in Git tools and the VS Code merge editor, plus the integrated terminal for exact Git commands.

Why:

- The guide already teaches VS Code.
- It is free and widely available.
- It is visual enough for merge conflicts.
- It still lets you run exact Git commands.
- It avoids making a beginner install a separate Git GUI too early.



---

# Appendix I: File and Folder Operation Scenarios

This appendix expands [Section 21](#21-file-and-folder-change-workflows) with scenario-based command recipes.

## I.1 Add one file

```bash
git status
git add notes.md
git status
git commit -m "Add notes file"
git push
```

## I.2 Add a folder with files

```bash
git status
git add docs/
git status
git commit -m "Add docs folder"
git push
```

Git tracks the files inside `docs/`, not the empty folder itself.

## I.3 Add an empty folder with a placeholder

```bash
mkdir empty-folder
touch empty-folder/.gitkeep
git add empty-folder/.gitkeep
git commit -m "Add empty folder placeholder"
git push
```

PowerShell:

```powershell
New-Item -ItemType Directory -Path empty-folder
New-Item -ItemType File -Path empty-folder/.gitkeep
git add empty-folder/.gitkeep
git commit -m "Add empty folder placeholder"
git push
```

## I.4 Update one tracked file

```bash
git status
git diff guide.md
git add guide.md
git status
git diff --cached guide.md
git commit -m "Update guide"
git push
```

## I.5 Overwrite same path with a newer version

```bash
git status
git diff --stat
git add docs/guide.md
git status
git diff --cached --stat
git commit -m "Replace guide with updated version"
git push
```

If the path is the same, Git usually treats the drop-in replacement like a modification.

## I.6 Delete then replace same path before staging

If you delete `docs/guide.md`, copy a newer file back to `docs/guide.md`, and then stage the final result:

```bash
git status
git add docs/guide.md
git commit -m "Replace guide with updated version"
git push
```

Git records the final staged snapshot.

## I.7 Delete, commit, then add back later

```bash
git rm docs/guide.md
git commit -m "Remove guide"

git add docs/guide.md
git commit -m "Add replacement guide"
git push
```

This creates a history where the file was removed in one commit and added back in a later commit.

## I.8 Delete a file with `git rm`

```bash
git status
git rm old-notes.md
git status
git commit -m "Remove old notes file"
git push
```

## I.9 Delete a folder with `git rm -r`

```bash
git status
git rm -r old-docs/
git status
git commit -m "Remove old docs folder"
git push
```

## I.10 Stop tracking a file but keep it locally

```bash
git rm --cached local-notes.md
git commit -m "Stop tracking local notes"
git push
```

Usually add it to `.gitignore` too:

```gitignore
local-notes.md
```

## I.11 Stop tracking a folder but keep it locally

```bash
git rm -r --cached local-folder/
git commit -m "Stop tracking local folder"
git push
```

Usually add it to `.gitignore` too:

```gitignore
local-folder/
```

## I.12 Move or rename a file with `git mv`

```bash
git status
git mv old-name.md new-name.md
git status
git commit -m "Rename guide file"
git push
```

## I.13 Move a file into a folder

```bash
mkdir docs
git mv guide.md docs/guide.md
git commit -m "Move guide into docs folder"
git push
```

## I.14 Move or rename a folder with `git mv`

```bash
git status
git mv old-docs docs
git status
git commit -m "Rename docs folder"
git push
```

## I.15 Move outside Git and stage with `git add -A`

```bash
mv old-docs docs
git status
git add -A old-docs docs
git status
git commit -m "Rename docs folder"
git push
```

PowerShell:

```powershell
Move-Item old-docs docs
git status
git add -A old-docs docs
git status
git commit -m "Rename docs folder"
git push
```

## I.16 Compare `git mv` with file-manager moves

| Method | Command pattern | Notes |
|---|---|---|
| Git-aware move | `git mv old new` | Moves and stages in one step. |
| File-manager move | Move in Explorer/VS Code, then `git add -A` | Works well if staged correctly. |
| Delete/add | `git rm old`, then `git add new` | May appear as delete/add or rename depending on similarity. |

## I.17 Verify changes before committing

Before committing, check:

```bash
git status
git diff --stat
git diff --summary
git diff --cached --stat
git diff --cached --summary
```

## I.18 Direct-to-`main` push workflow

```bash
git switch main
git pull
git status
git add .
git status
git commit -m "Describe what changed"
git push
```

Best for solo learning, tiny low-risk changes, private repositories, and first-time repository setup.

## I.19 Working-branch push workflow

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

Then open a pull request or merge later.

After merge:

```bash
git switch main
git pull
```

If the merged result is a version:

```bash
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Optional cleanup:

```bash
git branch -d update-guide
git push origin --delete update-guide
```

## I.20 Direct-to-`main` vs. working branch

| Situation | Recommended workflow |
|---|---|
| First push of a new solo repo | Direct to `main` |
| Tiny solo typo fix | Direct to `main` |
| Learning project | Direct to `main` |
| Large documentation update | Working branch |
| Code change needing tests | Working branch |
| Collaborative repository | Working branch |
| Protected `main` branch | Working branch |
| Deployment from `main` | Working branch |
| Version release | Merge to `main`, then tag |



---

# Appendix J: Commit Message and Commit Body Examples

This appendix expands [Section 22](#22-commit-messages-commit-bodies-and-repository-descriptions) with copyable examples.

## J.1 Minimal one-line commit

Use this when the change is clear enough from the summary:

```bash
git commit -m "docs: add AWS S3 static website quick start guide"
```

Resulting commit message:

```text
docs: add AWS S3 static website quick start guide
```

This is valid and complete.

## J.2 Two-part commit with summary and body

Use this when the change benefits from context:

```bash
git commit -m "docs: add AWS S3 static website quick start guide" -m "Add the initial documentation set for hosting a simple static website on AWS.

Includes the main S3 static website quick start guide, repository README, and changelog. The guide covers a minimal S3-only testing path and a recommended production-style path using CloudFront, AWS Certificate Manager, Cloudflare DNS, and a private S3 bucket."
```

Resulting commit message:

```text
docs: add AWS S3 static website quick start guide

Add the initial documentation set for hosting a simple static website on AWS.

Includes the main S3 static website quick start guide, repository README, and changelog. The guide covers a minimal S3-only testing path and a recommended production-style path using CloudFront, AWS Certificate Manager, Cloudflare DNS, and a private S3 bucket.
```

## J.3 Generic pattern

Use this pattern:

```bash
git commit -m "Summary" -m "Body"
```

That creates:

```text
Summary

Body
```

## J.4 Recommended initial commit for this guide project

For this Git Repository Guide project, a good initial commit could be:

```bash
git commit -m "docs: add Git repository guide" -m "Add the initial guide, README, and changelog for creating Git repositories and managing versioned file sets.

Includes beginner-friendly command-line workflows, VS Code guidance, annotated tag examples, repository packaging recommendations, and version-history documentation."
```

A shorter version is also fine:

```bash
git commit -m "docs: add Git repository guide"
```

## J.5 Recommended commit for a versioned guide update

For a meaningful guide update, a one-line commit is usually enough if the changelog explains the details:

```bash
git commit -m "Expand guide with commit message and body guidance"
```

A longer version can include a body:

```bash
git commit -m "Expand guide with commit message and body guidance" -m "Add guidance explaining the difference between a commit summary, optional commit body, repository description, README summary, and changelog entry.

Includes examples for one-line commits, two-part commits using multiple -m flags, and initial documentation commits."
```

## J.6 Summary vs. body vs. changelog

| Item | Example | Best use |
|---|---|---|
| Commit summary | `Expand guide with commit message and body guidance` | One-commit summary |
| Commit body | Longer optional explanation below the summary | Context for future Git history readers |
| CHANGELOG entry | Bullets under `v1.5.0` | Version-level summary of notable changes |
| README version history | `v1.5.0 = ...` | Very short release/version summary |

The commit body is not a replacement for the changelog.

The changelog is not a replacement for a useful commit summary.

Use each one for its own purpose.


# Appendix K: References

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

[R37] Git documentation, `git-ls-tree`.  
https://git-scm.com/docs/git-ls-tree

[R38] Git documentation, `git-merge`.  
https://git-scm.com/docs/git-merge

[R39] Git documentation, `git-rebase`.  
https://git-scm.com/docs/git-rebase

[R40] Git documentation, `git-fetch`.  
https://git-scm.com/docs/git-fetch

[R41] Git documentation, `git-pull`.  
https://git-scm.com/docs/git-pull

[R42] GitHub Docs, “Creating a pull request.”  
https://docs.github.com/articles/creating-a-pull-request


[R43] Git documentation, `git-mergetool`.  
https://git-scm.com/docs/git-mergetool

[R44] GitHub Docs, “About merge conflicts.”  
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts

[R45] GitHub Docs, “Resolving a merge conflict using the command line.”  
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line

[R46] GitHub Docs, “Resolving a merge conflict on GitHub.”  
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-on-github

[R47] Visual Studio Code Docs, “Source Control: Merge conflicts.”  
https://code.visualstudio.com/docs/sourcecontrol/overview#_merge-conflicts

[R48] Microsoft Learn, “Use Git and GitHub in Visual Studio.”  
https://learn.microsoft.com/en-us/visualstudio/version-control/git-with-visual-studio

[R49] GitHub Docs, “Committing and reviewing changes to your project in GitHub Desktop.”  
https://docs.github.com/en/desktop/making-changes-in-a-branch/committing-and-reviewing-changes-to-your-project-in-github-desktop

[R50] Sublime Merge.  
https://www.sublimemerge.com/

[R51] Git Extensions documentation, “Merge Conflicts.”  
https://git-extensions-documentation.readthedocs.io/

[R52] GitKraken, “Merge Conflict Resolution Tool.”  
https://www.gitkraken.com/features/merge-conflict-resolution-tool

[R53] GitLens documentation.  
https://help.gitkraken.com/gitlens/gitlens-home/

[R54] Git Large File Storage documentation.  
https://git-lfs.com/


[R55] Git documentation, `git-rm`.  
https://git-scm.com/docs/git-rm

[R56] Git documentation, `git-mv`.  
https://git-scm.com/docs/git-mv

---

# Index


## File and folder operations

See [21. File and Folder Change Workflows](#21-file-and-folder-change-workflows) and [Appendix I](#appendix-i-file-and-folder-operation-scenarios).

## Empty folders

See [21. File and Folder Change Workflows](#21-file-and-folder-change-workflows).

## Drop-in replacement

See [21. File and Folder Change Workflows](#21-file-and-folder-change-workflows) and [Appendix I](#appendix-i-file-and-folder-operation-scenarios).

## Delete then replace

See [21. File and Folder Change Workflows](#21-file-and-folder-change-workflows) and [Appendix I](#appendix-i-file-and-folder-operation-scenarios).

## Stop tracking

See [21. File and Folder Change Workflows](#21-file-and-folder-change-workflows).

## Direct push to main

See [21. File and Folder Change Workflows](#21-file-and-folder-change-workflows).

## Working branch push

See [21. File and Folder Change Workflows](#21-file-and-folder-change-workflows), [17. Branching, Merging, and Rebasing](#17-branching-merging-and-rebasing), and [Appendix I](#appendix-i-file-and-folder-operation-scenarios).


## Adding files

See [19. Adding, Updating, and Replacing Files](#19-adding-updating-and-replacing-files) and [Appendix H](#appendix-h-file-update-merge-and-conflict-scenarios).

## Updating files

See [19. Adding, Updating, and Replacing Files](#19-adding-updating-and-replacing-files) and [Appendix H](#appendix-h-file-update-merge-and-conflict-scenarios).

## Replacing files

See [19. Adding, Updating, and Replacing Files](#19-adding-updating-and-replacing-files) and [Appendix H](#appendix-h-file-update-merge-and-conflict-scenarios).

## Fetch

See [20. Fetch, Pull, Merge, Rebase, and Conflict Basics](#20-fetch-pull-merge-rebase-and-conflict-basics) and [Appendix H](#appendix-h-file-update-merge-and-conflict-scenarios).

## Pull

See [20. Fetch, Pull, Merge, Rebase, and Conflict Basics](#20-fetch-pull-merge-rebase-and-conflict-basics) and [Appendix H](#appendix-h-file-update-merge-and-conflict-scenarios).

## Merge conflict

See [20. Fetch, Pull, Merge, Rebase, and Conflict Basics](#20-fetch-pull-merge-rebase-and-conflict-basics), [Appendix B](#appendix-b-expanded-vs-code-reference), and [Appendix H](#appendix-h-file-update-merge-and-conflict-scenarios).

## Git tools

See [20. Fetch, Pull, Merge, Rebase, and Conflict Basics](#20-fetch-pull-merge-rebase-and-conflict-basics) and [Appendix H.15](#h15-diff-comparison-merge-and-conflict-resolution-tools).

## Branch workflow

See [17. Branching, Merging, and Rebasing](#17-branching-merging-and-rebasing) and [Appendix G](#appendix-g-command-sequences-and-workflow-recipes).

## Command sequences

See [Appendix G: Command Sequences and Workflow Recipes](#appendix-g-command-sequences-and-workflow-recipes).

## Git objects

See [18. Git Push Object Counts and Git Objects](#18-git-push-object-counts-and-git-objects).

## Merge

See [17. Branching, Merging, and Rebasing](#17-branching-merging-and-rebasing).

## Rebase

See [17. Branching, Merging, and Rebasing](#17-branching-merging-and-rebasing).

## README

See [15. Repository Packaging and Stable Filenames](#15-repository-packaging-and-stable-filenames).

## CHANGELOG

See [15. Repository Packaging and Stable Filenames](#15-repository-packaging-and-stable-filenames).

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
