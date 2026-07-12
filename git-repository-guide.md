# Creating a Git Repository and Marking File Sets as Versions

Document version: v1.19.0  
Previous locked version: v1.18.0  
Version status: Locked standalone Markdown version  
Update type: Additive update  
Versioning method: Document metadata only; no Git repository package required  
Future edit policy: Do not overwrite this `v1.19.0` file. Save future changes as a new version, such as `v1.19.1` or `v1.20.0`.  
Current as of: 2026-07-06

Revision note: This `v1.19.0` edition preserves the `v1.18.0` guide and additively incorporates guidance for GitHub Releases, annotated tags, release titles and notes, generated release notes, previous-tag comparisons, release assets, draft and pre-release states, tag/release correction workflows, and practical `.gitignore` usage.

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
- [23. Practical Staging and Tag Snapshot Example](#23-practical-staging-and-tag-snapshot-example)
- [24. Comparing Version Tags and Changed Files](#24-comparing-version-tags-and-changed-files)
- [25. Pull Requests from Basic to Advanced](#25-pull-requests-from-basic-to-advanced)
- [26. Renaming Files in a Git Repository](#26-renaming-files-in-a-git-repository)
- [27. Reconstructing a Repository from Historical Snapshots](#27-reconstructing-a-repository-from-historical-snapshots)
- [28. Correcting Tag Mistakes and Understanding Tag Messages](#28-correcting-tag-mistakes-and-understanding-tag-messages)
- [29. Line Endings, LF, CRLF, and `.gitattributes`](#29-line-endings-lf-crlf-and-gitattributes)
- [30. Correcting Commit Message Mistakes](#30-correcting-commit-message-mistakes)
- [31. Commit Message Prefixes and When to Use Them](#31-commit-message-prefixes-and-when-to-use-them)
- [32. Push, Tag, Branch, and Repository Hygiene Workflows](#32-push-tag-branch-and-repository-hygiene-workflows)
- [33. GitHub File Search, Tag Inspection, and Commit History Lookup](#33-github-file-search-tag-inspection-and-commit-history-lookup)
- [34. Linking Related Repositories and Multi-Repo Release Workflows](#34-linking-related-repositories-and-multi-repo-release-workflows)
- [35. Renaming Repositories, Local Folders, Project Names, and Remotes](#35-renaming-repositories-local-folders-project-names-and-remotes)
- [36. Consolidated Git Workflow Defaults and Verification Checklists](#36-consolidated-git-workflow-defaults-and-verification-checklists)
- [37. Staging, Rename Review, Status Checks, and Precise `origin` Wording](#37-staging-rename-review-status-checks-and-precise-origin-wording)
- [38. GitHub Releases, `.gitignore`, and Release-Ready Version Notes](#38-github-releases-gitignore-and-release-ready-version-notes)
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
- [Appendix K: Practical Staging, Tag, and Download Scenarios](#appendix-k-practical-staging-tag-and-download-scenarios)
- [Appendix L: Compare, Diff, and Tag Inspection Scenarios](#appendix-l-compare-diff-and-tag-inspection-scenarios)
- [Appendix M: Pull Request Scenarios](#appendix-m-pull-request-scenarios)
- [Appendix N: File Rename and Move Scenarios](#appendix-n-file-rename-and-move-scenarios)
- [Appendix P: Historical Repository Reconstruction Scenario](#appendix-p-historical-repository-reconstruction-scenario)
- [Appendix Q: Tag Correction and Release Repair Scenarios](#appendix-q-tag-correction-and-release-repair-scenarios)
- [Appendix R: Line-Ending and `.gitattributes` Scenarios](#appendix-r-line-ending-and-gitattributes-scenarios)
- [Appendix S: Commit Message Correction Scenarios](#appendix-s-commit-message-correction-scenarios)
- [Appendix T: Commit Message Prefix Scenarios](#appendix-t-commit-message-prefix-scenarios)
- [Appendix U: Push, Tag, Branch, and Repository Hygiene Scenarios](#appendix-u-push-tag-branch-and-repository-hygiene-scenarios)
- [Appendix V: GitHub File Search, Tag Inspection, and Commit History Scenarios](#appendix-v-github-file-search-tag-inspection-and-commit-history-scenarios)
- [Appendix W: Multi-Repository Linking and Release Workflow Scenarios](#appendix-w-multi-repository-linking-and-release-workflow-scenarios)
- [Appendix Y: Repository Renaming and Rename Workflow Scenarios](#appendix-y-repository-renaming-and-rename-workflow-scenarios)
- [Appendix Z: References](#appendix-z-references)
- [Index](#index)

---

## 1. Purpose of This Guide

You already have:

- Git installed.
- A GitHub account.
- A folder of files you want to track.
- A desire to mark one file set as `v1.0.0`, then later mark newer file sets as `v1.1.0`, `v1.2.0`, `v1.3.0`, `v1.4.0`, `v1.5.0`, `v1.6.0`, `v1.7.0`, `v1.8.0`, `v1.9.0`, `v1.10.0`, `v1.11.0`, `v1.11.1`, `v1.12.0`, `v1.13.0`, `v1.14.0`, `v1.15.0`, `v1.16.0`, `v1.17.0`, `v1.18.0`, `v1.19.0`, or another version.

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


### Rename a tracked file

```bash
git mv old-name.md new-name.md
git add -A
git diff --cached --summary
git diff --cached --name-status --find-renames
git commit -m "Rename file"
```

### Export a version

```bash
git archive --format=zip --output project-v1.0.0.zip v1.0.0
```


### Correct an older pushed tag safely

```powershell
$commit = git rev-list -n 1 vX.Y.Z
git push origin --delete vX.Y.Z
git tag -d vX.Y.Z
git tag -a vX.Y.Z $commit -m "Version X.Y.Z"
git push origin vX.Y.Z
```

### Inspect line endings

```powershell
git ls-files --eol
```



### Choose a commit-message prefix

```bash
git commit -m "docs: document commit message prefixes"
git commit -m "fix: correct canonical domain"
git commit -m "feat: add web applications section"
git commit -m "chore: prepare v2.1.0 release"
```

Basic rule:

```text
feat   = user-visible addition or expansion
fix    = correction
docs   = documentation-only change
chore  = routine maintenance
style  = formatting-only change
```

### Search and fix commit-message typos

```bash
git log --all --grep="Ve0sion" --oneline
git log -1 --oneline
git commit --amend -m "Corrected commit message"
```

For an older commit:

```bash
git rebase -i <bad-commit-sha>~1
```

Change `pick` to `reword`.

If rewritten history was already pushed and it is safe to rewrite that branch:

```bash
git push --force-with-lease
```


### Explicit branch and tag push

```powershell
git status
git add -A
git status
git commit -m "docs: update guide"
git push origin main
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

### Check branch/tag push state

```powershell
git status
git branch -vv
git log --oneline origin/main..main
git log --oneline main..origin/main
git log --oneline --decorate --graph --all
```


### Search GitHub files, tags, and commit history

```text
Search current GitHub file: Ctrl+F or Cmd+F
Open GitHub web editor: .
Search specific path: keyword path:git-repository-guide.md
```

```bash
git tag --sort=-v:refname
git log --tags --simplify-by-decoration --oneline
git describe --tags
git show-ref --tags
git log --format=%B
git log --all --grep="keyword" --oneline
```

Press `q` to exit the Git pager.


### Link related repositories

For a hub-and-example repo series:

```text
Use README links as the primary connection.
Use GitHub topics for grouping and discovery.
Use GitHub About / website links for quick context.
Use tags and releases consistently within each repo.
Avoid submodules or subtree unless there is a real technical need.
```

Same-repo links:

```markdown
[Changelog](CHANGELOG.md)
[Learning path](docs/learning-path.md)
```

Cross-repo links:

```markdown
[Series hub](https://github.com/YOUR-USERNAME/simple-website-examples)
[Example 02](https://github.com/YOUR-USERNAME/simple-website-example-02-basic-site-files)
```


### Rename repositories, folders, and remotes

```text
Local parent folder rename: usually no Git commit.
Tracked file/folder rename: Git commit required.
GitHub repo rename: rename in GitHub settings, then update local remote.
Project/app name rename: search files, update references, then commit.
```

Tracked rename:

```bash
git mv old-path new-path
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
git commit -m "chore: rename project paths"
```

Update remote after GitHub repo rename:

```bash
git remote -v
git remote set-url origin https://github.com/USERNAME/new-repo-name.git
git remote -v
git fetch origin
```

Search old references:

```bash
git grep "old-name"
```




### GitHub Release and `.gitignore` quick checks

```bash
git status --short
git diff --cached --stat
git push origin main

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z

git show vX.Y.Z
git ls-remote --tags origin vX.Y.Z
```

Release-note reminder:

```text
Commit = record the work
Tag = name the version
Release = explain and distribute the version
```

Check ignore behavior:

```bash
git status --ignored
git check-ignore -v path/to/file
```

Stop tracking an already tracked file while keeping it locally:

```bash
git rm --cached path/to/file
```

Stop tracking an already tracked folder while keeping it locally:

```bash
git rm -r --cached path/to/folder
```

### Staging and rename review

```bash
git status --short
git diff --stat
git add -A
git status --short
git status --short --renames
git diff --cached --stat
git diff --cached --name-status --find-renames
```

Check the repo root:

```bash
git rev-parse --show-toplevel
```

Check for `.gitattributes` in PowerShell:

```powershell
Test-Path .\.gitattributes
```

Create a folder safely in PowerShell:

```powershell
New-Item -ItemType Directory -Force ".\docs\reference"
```

Prefer this wording:

```text
committed locally and pushed to origin
```

Avoid this wording:

```text
checked into origin
```

### Consolidated defaults and verification

```text
Primary branch: main
Primary remote: origin
Version tags: vMAJOR.MINOR.PATCH
Meaningful version tags: annotated tags
Push tags: one intentional tag at a time
```

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

### Internal links vs. standalone download filenames

Use this rule for this guide's file set:

> Internal repo links and active file references should use stable filenames. Standalone download filename examples and historical changelog entries may still use versioned filenames when that is the point being explained.

Inside the repository, link to active files like this:

```text
git-repository-guide.md
git-repository-guide-quick-start-guide.md
git-repository-guide-cheat-sheet.md
git-command-quick-reference.md
README.md
CHANGELOG.md
```

For downloadable copies created outside the repository, versioned filenames are still useful:

```text
git-repository-guide-v1.11.1.md
README-v1.11.1.md
CHANGELOG-v1.11.1.md
```

Historical changelog entries may also mention the versioned standalone filenames that were created at that time. Do not rewrite those historical examples unless they are inaccurate or confusing in context.


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
| `v1.6.0` | Additive expansion covering practical staging, unchanged tracked files, tag snapshot downloads, and source ZIP vs. release asset ZIP behavior |
| `v1.7.0` | Additive expansion covering GitHub.com tag comparison, version-diff workflows, and Pull Request workflows |
| `v1.8.0` | Additive expansion covering tracked-file rename workflows, `git mv`, rename detection, and Markdown reference updates |
| `v1.9.0` | Additive expansion covering historical repository reconstruction, production tags, tag correction workflows, GitHub Releases, and LF/CRLF line-ending guidance |
| `v1.10.0` | Additive expansion covering project identity, canonical URL, GitHub Release notes, release documentation files, and import-note examples for reconstructed repositories |
| `v1.11.0` | Additive expansion covering commit-message typo detection, commit-message correction, amend/rebase workflows, pushed-history safety, and force-with-lease guidance |
| `v1.12.0` | Additive expansion covering commit-message prefixes, prefix selection, Conventional Commit-style examples, scopes, breaking changes, and tag-message distinctions |
| `v1.11.1` | Patch correction clarifying stable internal repository filenames while preserving versioned standalone download filename examples and historical changelog entries when intentional |

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

# Option A: normal later push after upstream is configured
git push

# Option B: explicit push to the main branch on origin
git push origin main
```

Use one of the push options above, not both every time. They are shown together to make the choice visible.

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

# Push the branch first so GitHub's normal/default branch view is current.
git push origin main

# Then create and push the version tag.
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Example:

```bash
git status
git add .
git status
git commit -m "Expand guide with repository packaging and branch workflow guidance"

git push origin main

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



---

## 23. Practical Staging and Tag Snapshot Example

This section shows a realistic update where some files are modified, some files are new, and other tracked files are unchanged.

The key lesson:

> Staging only changed or new files does not mean the tag contains only those files. A commit records the full tracked repository snapshot. A tag points to that commit.

### Example repository

Suppose a repository named:

```text
aws-live-streaming-guide
```

currently has four tracked files and is tagged `v1.1.0`:

```text
README.md
CHANGELOG.md
aws-live-streaming-guide-obs-ivs.md
aws-live-streaming-guide-obs-medialive.md
```

Then you update two existing files:

```text
README.md
CHANGELOG.md
```

And you create four new files:

```text
aws-live-streaming-cheat-sheet-obs-ivs.md
aws-live-streaming-cheat-sheet-obs-medialive.md
aws-live-streaming-quick-start-guide-obs-ivs.md
aws-live-streaming-quick-start-guide-obs-medialive.md
```

The two original full guide files are unchanged:

```text
aws-live-streaming-guide-obs-ivs.md
aws-live-streaming-guide-obs-medialive.md
```

### Expected `git status`

Before staging, `git status` should show the two modified files and four untracked files.

Example:

```text
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  modified:   CHANGELOG.md
  modified:   README.md

Untracked files:
  aws-live-streaming-cheat-sheet-obs-ivs.md
  aws-live-streaming-cheat-sheet-obs-medialive.md
  aws-live-streaming-quick-start-guide-obs-ivs.md
  aws-live-streaming-quick-start-guide-obs-medialive.md

no changes added to commit
```

The unchanged full guide files do not appear in `git status` because Git sees no changes to them.

That is good.

They are still tracked. They are still part of the repository.

### Safe `git add .` workflow

From the repository root, this is a valid workflow:

```bash
git status
git add .
git status
git commit -m "Add quick-start guides and cheat sheets"
git push

git tag -a v1.1.1 -m "Version 1.1.1"
git push origin v1.1.1
```

The first `git status` verifies what changed before staging.

`git add .` stages new files, modified files, and deleted tracked files under the current folder.

The second `git status` confirms exactly what is staged before committing.

The commit records the new full tracked repository snapshot.

The tag marks that full repository snapshot as `v1.1.1`.

### More explicit staging alternative

If you know exactly which files should be included, you can stage them explicitly:

```bash
git status
git add README.md CHANGELOG.md aws-live-streaming-cheat-sheet-obs-ivs.md aws-live-streaming-cheat-sheet-obs-medialive.md aws-live-streaming-quick-start-guide-obs-ivs.md aws-live-streaming-quick-start-guide-obs-medialive.md
git status
git commit -m "Add quick-start guides and cheat sheets"
git push

git tag -a v1.1.1 -m "Version 1.1.1"
git push origin v1.1.1
```

Explicit paths are safer when you want maximum control.

`git add .` is convenient when `git status` confirms that only intended changes are present.

### Do not delete unchanged files just to simplify `git add .`

Do not delete unchanged tracked files just to make staging feel simpler.

If a tracked file is deleted locally, Git sees that as a deletion.

If you then run:

```bash
git add .
git commit -m "Add quick-start guides and cheat sheets"
```

the deletion can be included in the commit.

That means the deleted files would be removed from the new repository snapshot and from the new tag.

Correct approach:

> Leave unchanged tracked files in the folder. If `git status` does not mention them, that means Git sees no change.

### If you accidentally delete tracked files

If you deleted tracked files locally but have not staged the deletion yet, restore them:

```bash
git restore aws-live-streaming-guide-obs-ivs.md
git restore aws-live-streaming-guide-obs-medialive.md
git status
```

If you already staged the deletion, unstage and restore:

```bash
git restore --staged aws-live-streaming-guide-obs-ivs.md
git restore --staged aws-live-streaming-guide-obs-medialive.md

git restore aws-live-streaming-guide-obs-ivs.md
git restore aws-live-streaming-guide-obs-medialive.md

git status
```

`git restore --staged` removes the deletion from the staging area.

`git restore` restores the file in the working tree from the current commit.

### If you intentionally want to remove files from the repository

If your goal is to remove the two full guide files from the repository, use `git rm` intentionally:

```bash
git status
git rm aws-live-streaming-guide-obs-ivs.md
git rm aws-live-streaming-guide-obs-medialive.md
git status
git commit -m "Remove full guides"
git push

git tag -a v1.1.1 -m "Version 1.1.1"
git push origin v1.1.1
```

That makes the new tag point to a repository snapshot that no longer includes those files.

Consider the version number carefully when removing files. Removing tracked files may be more significant than a small patch update.

### Does `git add .` check subfolders?

Yes.

`git add .` stages changes under the current directory, including subfolders, subject to `.gitignore`.

If the terminal is at the repository root:

```text
C:\git\aws-live-streaming-guide
```

then:

```bash
git add .
```

will stage changes under the repository root and its subfolders.

It can stage:

- new files;
- modified tracked files;
- deleted tracked files;
- changes in subfolders.

It will not stage ignored files unless forced.

### What should the tag contain?

If you commit the two modified files and four new files while leaving the two original full guide files tracked and unchanged, then tag `v1.1.1` should identify a repository snapshot containing eight tracked files:

```text
README.md
CHANGELOG.md
aws-live-streaming-guide-obs-ivs.md
aws-live-streaming-guide-obs-medialive.md
aws-live-streaming-cheat-sheet-obs-ivs.md
aws-live-streaming-cheat-sheet-obs-medialive.md
aws-live-streaming-quick-start-guide-obs-ivs.md
aws-live-streaming-quick-start-guide-obs-medialive.md
```

The tag is not limited to the six files that were added or modified.

A tag points to a commit, and the commit represents the full tracked repository snapshot.

### GitHub source ZIP vs. custom release asset ZIP

A GitHub automatic source archive for a tag, such as:

```text
Source code (zip)
```

is generated from the tagged repository snapshot.

So if the repository snapshot at `v1.1.1` contains eight tracked files, the automatic source ZIP for `v1.1.1` should contain those eight tracked files.

A `git archive` command also exports the tracked repository snapshot at the tag:

```bash
git archive --format=zip --output aws-live-streaming-guide-v1.1.1.zip v1.1.1
```

A custom GitHub Release asset ZIP is different.

If you manually create and upload a ZIP file as a release asset, that ZIP contains whatever you put into it. It could contain six files, eight files, PDFs, quick-start guides only, or any other custom package contents.

Important distinction:

> A GitHub automatic source ZIP is generated from the tagged repository snapshot. A custom release asset ZIP is manually created and can contain any selected files.



---

## 24. Comparing Version Tags and Changed Files

After you create version tags, you often need to answer two different questions:

1. What files exist in tag `v1.1.1`?
2. What files changed between `v1.1.0` and `v1.1.1`?

For version-to-version review, you usually want the second question.

### Best command for changed files between tags

Use:

```bash
git diff --name-status v1.1.0..v1.1.1
```

Example output:

```text
M       README.md
M       CHANGELOG.md
A       git-repository-guide-quick-start-guide-v1.6.0.md
A       git-repository-guide-cheat-sheet-v1.6.0.md
```

Status meanings:

| Status | Meaning |
|---|---|
| `A` | Added |
| `M` | Modified |
| `D` | Deleted |
| `R` | Renamed |
| `C` | Copied |

This answers:

> What files were added, modified, deleted, renamed, or copied between these two tags?

### Show only added files

```bash
git diff --name-status --diff-filter=A v1.1.0..v1.1.1
```

### Show only modified files

```bash
git diff --name-status --diff-filter=M v1.1.0..v1.1.1
```

### Show added and modified files only

```bash
git diff --name-status --diff-filter=AM v1.1.0..v1.1.1
```

### Show a summary with line counts

```bash
git diff --stat v1.1.0..v1.1.1
```

Use this when you want a quick summary of how much changed.

### Show the actual content differences

```bash
git diff v1.1.0..v1.1.1
```

Use this when you need the full patch/diff.

### Show commits between two tags

```bash
git log --oneline v1.1.0..v1.1.1
```

This answers:

> What commits are included between the old version tag and the new version tag?

### Show all tracked files contained in a tag

This is a different question.

Use:

```bash
git ls-tree -r --name-only v1.1.1
```

This answers:

> What files are in the repository snapshot at `v1.1.1`?

It does not answer:

> What files changed from `v1.1.0` to `v1.1.1`?

### Compare tags on GitHub.com

GitHub's Compare view can compare repository states across branches, tags, commits, forks, and dates. [R57]

Direct URL pattern:

```text
https://github.com/OWNER/REPO/compare/v1.1.0...v1.1.1
```

Example pattern:

```text
https://github.com/YOUR-USERNAME/YOUR-REPO/compare/v1.1.0...v1.1.1
```

Replace `OWNER` and `REPO` with the actual GitHub owner and repository name.

### Manual navigation to GitHub Compare

If the direct URL does not work, navigate manually:

1. Open the repository home page on GitHub.
2. Click in the browser address bar.
3. Add `/compare` to the end of the repository URL.
4. Press Enter.
5. On the Compare page, use the selectors near the top.
6. Set the earlier tag as the base.
7. Set the newer tag as the compare target.
8. Review the commits and file changes.

Example:

```text
base: v1.1.0
compare: v1.1.1
```

Then look for the commit list and changed-files/diff area.

### Explicit tag comparison when names are ambiguous

If a branch and a tag have the same name, GitHub may interpret the name as a branch by default. Use `tags/` to force tag comparison:

```text
https://github.com/OWNER/REPO/compare/tags/v1.1.0...tags/v1.1.1
```

### Compare releases from GitHub Releases

If you created GitHub Releases, you can compare releases from the Releases page. GitHub's release comparison documentation says to use the Compare dropdown next to the release you want as the base, then choose the tag you want to compare. [R58]

This works best when actual GitHub Releases exist, not just bare Git tags.

### Why a GitHub compare URL might not work

| Problem | Likely cause | Fix |
|---|---|---|
| Page says not found | Owner or repo name is wrong | Open the repo first, then add `/compare` manually |
| Tag is missing | Tag was not pushed to GitHub | Run `git push origin vX.Y.Z` |
| Tag name is wrong | Typo, or `1.1.1` used instead of `v1.1.1` | Check the tag list |
| Private repo cannot be viewed | You are not signed in or lack permission | Sign in with an account that has access |
| Branch and tag have same name | GitHub may interpret the branch first | Use `tags/vX.Y.Z` in the compare URL |
| Releases comparison is missing | Tags exist but GitHub Releases do not | Use the normal Compare page instead |

### Verify tags exist on GitHub

1. Open the repository on GitHub.
2. Find the branch/tag selector near the file list.
3. Switch from **Branches** to **Tags**.
4. Confirm both tags appear.
5. If a tag is missing, push it:

```bash
git push origin v1.1.1
```

### Practical rule

Use this command when you want to know which files changed between versions:

```bash
git diff --name-status old-tag..new-tag
```

Use this command when you want to know which files exist in a tag:

```bash
git ls-tree -r --name-only tag-name
```



---

## 25. Pull Requests from Basic to Advanced

A Pull Request, often abbreviated **PR**, is a GitHub workflow for proposing that changes from one branch should be merged into another branch. Most commonly, a working branch is proposed for merge into `main`.

Despite the name, a Pull Request is not mainly about running the `git pull` command.

A Pull Request is a review, discussion, comparison, and merge workflow on GitHub. GitHub describes Pull Requests as a way to propose, review, and merge code changes. [R59]

### Why use a Pull Request?

Use a Pull Request when:

- you want to review changes before they land on `main`;
- you want to see a GitHub diff before merging;
- you want comments, suggestions, or approval;
- you want checks or automated tests to run before merging;
- you want to keep `main` stable;
- you are collaborating with other people;
- you are making a larger documentation update;
- you want a clear review record.

Direct commits to `main` may be acceptable when:

- you are working alone;
- the change is tiny;
- the repository is low-risk;
- no review is needed;
- the project does not use branch protection.

### Basic Pull Request workflow

Start from an up-to-date `main`:

```bash
git switch main
git pull
```

Create a working branch:

```bash
git switch -c update-v1.7.0-guide
```

Make changes, then stage and commit them:

```bash
git status
git add .
git status
git commit -m "Expand guide with compare and pull request workflows"
```

Push the branch:

```bash
git push -u origin update-v1.7.0-guide
```

Then on GitHub:

1. Open the repository.
2. GitHub may show a banner for the recently pushed branch.
3. Click **Compare & pull request**, or go to **Pull requests** > **New pull request**.
4. Set the base branch to `main`.
5. Set the compare branch to `update-v1.7.0-guide`.
6. Review the diff.
7. Add a clear Pull Request title and description.
8. Create the Pull Request.
9. Review or request review.
10. Resolve comments or make follow-up commits if needed.
11. Merge when ready.
12. Pull the updated `main` locally.
13. Tag the final version from `main` if appropriate.

GitHub's Pull Request creation flow uses a base branch and a compare branch. [R60]

### Pull Request title and description

The Pull Request title should summarize what the change does.

The Pull Request description should explain:

- what changed;
- why it changed;
- what reviewers should check;
- whether the update is additive;
- what verification was performed;
- any known limitations.

Example title:

```text
Expand Git guide with compare and pull request workflows
```

Example description:

```markdown
## Summary

Adds v1.7.0 guidance for comparing version tags locally and on GitHub.com, plus expanded Pull Request workflows.

## Changes

- Adds Git command examples for changed files between tags.
- Adds GitHub Compare UI navigation.
- Adds Pull Request workflow guidance from branch creation through merge and tagging.
- Updates README and CHANGELOG.

## Verification

- Checked Markdown formatting.
- Confirmed links and version references.
- Confirmed additive structure.
```

### Reviewing a Pull Request

On GitHub, use the Pull Request's **Files changed** tab to inspect the diff.

GitHub's review documentation says Pull Requests let you review and discuss commits, changed files, and differences between files in the base and compare branches. [R61]

Review actions may include:

- leaving comments;
- requesting changes;
- approving;
- asking questions;
- making suggestions;
- pushing follow-up commits to the same branch.

### Updating a Pull Request after review comments

If edits are needed, keep working on the same branch:

```bash
git switch update-v1.7.0-guide
# edit files
git status
git add .
git status
git commit -m "Address review feedback"
git push
```

The existing Pull Request updates automatically because the branch received a new commit.

### Updating an out-of-date Pull Request branch

Beginner merge-based path:

```bash
git switch update-v1.7.0-guide
git fetch origin
git merge origin/main
git push
```

Alternative rebase path for a private branch:

```bash
git switch update-v1.7.0-guide
git fetch origin
git rebase origin/main
git push --force-with-lease
```

Warning:

> Use `git push --force-with-lease` only when you understand that rebasing rewrites commit history. Avoid rebasing shared branches unless everyone agrees.

### Pull Request merge options

GitHub supports different Pull Request merge methods, depending on repository settings. GitHub's merge documentation describes retaining commits with a merge commit, squashing commits into one commit, or rebasing commits. [R62]

| Option | What it means | Beginner guidance |
|---|---|---|
| Create a merge commit | Preserves branch history and adds a merge commit | Good default when you want full history |
| Squash and merge | Combines all PR commits into one commit on `main` | Useful for cleaning up many small commits |
| Rebase and merge | Replays PR commits onto `main` without a merge commit | Cleaner linear history, but more advanced |

Available merge options depend on repository settings.

### When to tag after a Pull Request

Usually tag the final merged result on `main`, not the temporary working branch.

After the Pull Request is merged:

```bash
git switch main
git pull

git tag -a v1.7.0 -m "Version 1.7.0"
git push origin v1.7.0
```

Reason:

> The version tag should identify the final accepted repository snapshot.

### Cleanup after merging

After the Pull Request is merged and local `main` is updated, you can usually delete the working branch.

Delete the local branch:

```bash
git branch -d update-v1.7.0-guide
```

Delete the remote branch:

```bash
git push origin --delete update-v1.7.0-guide
```

Do not delete a branch before you are sure the work was merged or is no longer needed.

### Draft Pull Requests

A draft Pull Request is useful when you want early visibility or feedback but the work is not ready to merge.

GitHub documents that a draft Pull Request cannot be merged until it is marked ready for review again. [R63]

Use a draft PR when:

- you want feedback before the work is complete;
- you want CI/checks to run early;
- you want to show progress without requesting final review.

### Pull Requests and branch protection

Repositories can use branch protection rules to require Pull Requests, reviews, passing checks, or up-to-date branches before merging into `main`.

Do not treat branch protection as a beginner requirement. Treat it as a useful safety feature for more important, shared, or production-connected repositories.

### Pull Request decision table

| Situation | Recommended workflow |
|---|---|
| Tiny solo edit | Direct commit to `main` can be fine |
| Solo but meaningful guide update | Branch + Pull Request is safer |
| Team project | Pull Requests by default |
| Risky change | Pull Request with review |
| Protected `main` branch | Pull Request required |
| Versioned documentation release | Pull Request first, tag after merge |



---

## 26. Renaming Files in a Git Repository

Renaming a file in Git is a normal file-change workflow.

The most important idea is:

> Git stores snapshots. A rename is usually inferred later by comparing a deleted path and an added path for content similarity.

That means Git can often show a rename, but the commit itself is still a before-and-after repository snapshot.

### When to rename a file

Rename a file when the existing name is misleading, outdated, too generic, or conflicts with newer companion files.

Example:

```text
aws-s3-static-website-quick-start.md
```

This may have been fine when it was the only guide-like file. But after the repository gains a true quick-start companion, the old full-guide filename can become confusing:

```text
aws-s3-static-website-quick-start-guide-v1.2.2.md
aws-s3-static-website-cheat-sheet-v1.2.2.md
```

A clearer full-guide filename might be:

```text
aws-s3-static-website-setup.md
```

This distinguishes the full setup guide from the shorter quick-start companion.

### Recommended rename workflow

Use `git mv` when you are intentionally renaming or moving a tracked file. Git's `git mv` documentation describes it as moving or renaming a file, directory, or symbolic link; after a successful move, the index is updated, but the change still needs to be committed. [R56]

PowerShell example:

```powershell
git mv aws-s3-static-website-quick-start.md aws-s3-static-website-setup.md
```

Then update Markdown links and references from the old filename to the new filename.

Likely files to check:

```text
README.md
CHANGELOG.md
the renamed full guide
quick-start companion guide
cheat sheet
other Markdown files that link to the old file
```

Stage all rename-related changes:

```powershell
git add -A
```

`git add -A` is useful here because it stages additions, modifications, and removals across the working tree. [R19]

Check the staged result:

```powershell
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
```

Then commit:

```powershell
git commit -m "docs: update full guide filename references"
```

### `git mv` vs. manual PowerShell rename

`git mv` is recommended because it makes your intent obvious and stages the move cleanly.

This is preferred:

```powershell
git mv old-name.md new-name.md
```

But `git mv` is not strictly required.

This manual PowerShell approach can also work:

```powershell
Rename-Item old-name.md new-name.md
git add -A
```

The shorter PowerShell alias can also work:

```powershell
ren old-name.md new-name.md
git add -A
```

The important part is that the final staged snapshot must show the old path removed and the new path added.

### Why use `git add -A` after a rename?

For rename workflows, prefer:

```powershell
git add -A
```

over only:

```powershell
git add .
```

`git add .` often works when you run it from the repository root, but `git add -A` is the safer beginner-friendly command when a change may include deletions, additions, and renamed paths across the repository.

### Will Git recognize the rename?

Usually, yes, if the file content remains substantially similar.

Check the staged rename summary:

```powershell
git diff --cached --summary
```

Example output:

```text
rename aws-s3-static-website-quick-start.md => aws-s3-static-website-setup.md (98%)
```

Check name status with rename detection:

```powershell
git diff --cached --name-status --find-renames
```

Example output:

```text
R098    aws-s3-static-website-quick-start.md    aws-s3-static-website-setup.md
```

`R098` means Git detected a rename with about 98% similarity.

Git's diff options include rename-detection behavior, including similarity thresholds for rename detection. [R25]

### Rename vs. delete plus unrelated new file

Git may show the change as a rename or as a delete plus add depending on similarity.

Likely shown as a rename:

```text
old file removed
new file added
new file content is almost the same
```

More likely shown as delete plus add:

```text
old file removed
new file added
new file content is heavily rewritten
```

Best practice:

> Rename first, commit the rename if it is important, then make large content changes in a separate commit.

For small documentation rename updates, it is also reasonable to rename the file and update links in one commit.

### How to view history after a rename

To follow file history across a rename, use:

```bash
git log --follow -- new-name.md
```

To see patches too:

```bash
git log --follow -p -- new-name.md
```

Git's `git log` documentation supports history inspection, and `--follow` is commonly used to continue listing file history beyond renames. [R26]

### Troubleshooting: deleted old file and copied in renamed file

Sometimes you may delete the old file and drop in a new file with the new filename before using `git mv`.

That is not automatically wrong.

First, try:

```powershell
git add -A
git diff --cached --summary
git diff --cached --name-status --find-renames
```

If Git detects the rename, you can usually continue.

If Git still shows a delete plus add and you care about clean rename display, redo the rename more explicitly.

One possible cleanup workflow:

```powershell
git reset
Copy-Item new-name.md new-name-temp.md
git restore old-name.md
Remove-Item new-name.md
git mv old-name.md new-name.md
Copy-Item new-name-temp.md new-name.md
Remove-Item new-name-temp.md
git add -A
git diff --cached --summary
git diff --cached --name-status --find-renames
```

What this does:

1. Unstages the current delete/add state.
2. Saves the updated renamed file as a temporary copy.
3. Restores the old tracked file.
4. Removes the manually copied renamed file.
5. Uses `git mv` to perform the rename explicitly.
6. Copies the updated content back over the renamed file.
7. Removes the temporary file.
8. Stages everything.
9. Checks whether Git detects the rename.

Only use the longer workflow if you care about Git or GitHub displaying the change as a clean rename.

### Commit message and optional body for a rename

A one-line commit message is often enough:

```powershell
git commit -m "docs: update full guide filename references"
```

A commit body is optional, but useful when you want to explain why the rename happened:

```powershell
git commit `
  -m "docs: update full guide filename references" `
  -m "Update README, CHANGELOG, quick-start companion, cheat sheet, and main guide filename metadata after renaming the full guide from aws-s3-static-website-quick-start.md to aws-s3-static-website-setup.md.

This avoids confusion now that the repository has a separate quick-start guide and cheat sheet."
```

Alternative with a PowerShell here-string:

```powershell
$body = @"
Update README, CHANGELOG, quick-start companion, cheat sheet, and main guide filename metadata after renaming the full guide from aws-s3-static-website-quick-start.md to aws-s3-static-website-setup.md.

This avoids confusion now that the repository has a separate quick-start guide and cheat sheet.
"@

git commit -m "docs: update full guide filename references" -m $body
```

### Practical rename checklist

Use this checklist:

1. Choose the new filename.
2. Rename with `git mv`.
3. Update Markdown links and references.
4. Run `git status`.
5. Stage with `git add -A`.
6. Run `git diff --cached --summary`.
7. Run `git diff --cached --name-status --find-renames`.
8. Commit.
9. Tag the new version if this is a versioned documentation update.



---

## 27. Reconstructing a Repository from Historical Snapshots

Sometimes a project already exists outside Git as a series of saved folders or ZIP backups.

Example:

```text
v0.1.0/
v0.1.1/
v0.1.2/
...
v1.4.0/
```

You can turn that folder history into a useful Git repository by importing each historical folder as a sequential commit.

This is not the same as pretending the repository always existed. It is a practical reconstruction of the project history.

### Example project: `demo-jeffskone-com`

For a website deployed at:

```text
https://demo.jeffskone.com
```

a good repository name is:

```text
demo-jeffskone-com
```

Recommended GitHub repository description:

```text
Portfolio site showcasing AWS microservices, websites, and web applications
```

Why use hyphens instead of dots?

```text
demo.jeffskone.com   = actual domain
demo-jeffskone-com   = clean repository/folder name
```

The hyphenated name is easier to use in GitHub URLs, local folder names, scripts, and command-line workflows.


### Website branding and canonical URL planning

A reconstructed repository should capture not only file history, but also the current project identity.

For a portfolio/demo site, it can be useful to distinguish:

| Item | Example | Purpose |
|---|---|---|
| Repository name | `demo-jeffskone-com` | Clean GitHub/local folder name |
| Canonical URL | `https://demo.jeffskone.com` | Official public URL |
| Site heading | `Jeff Skone's AWS Portfolio` | Human-facing branding |
| Browser title | `Jeff Skone's AWS Portfolio \| AWS Demos` | Browser/search/social context |
| Optional alias | `https://portfolio.jeffskone.com` | Friendly alternate address |

A good rule is:

> Use the word **portfolio** for professional positioning and the word **demo** for runnable examples and the established URL.

If an optional alias is added, redirect it to the canonical URL:

```text
https://portfolio.jeffskone.com -> https://demo.jeffskone.com
```

Keep one canonical URL in README files, metadata, resume links, documentation, analytics, and release notes.

Do not rewrite historical commits merely to change old domain references. The old domain may be part of the accurate project history.

### Recommended historical import strategy

Use a truthful historical sequence:

```text
1. Create an empty repository.
2. Copy the files from the earliest version folder into the repo.
3. Commit that version.
4. Replace the repo contents with the next version folder.
5. Commit that version.
6. Continue until the latest version folder is imported.
7. Add annotated tags to the production-release commits.
8. Push the repository and tags to GitHub.
9. Optionally create GitHub Releases from the production tags.
```

Important rule:

> Each historical version folder should become one commit.

Production versions should also receive annotated tags.

Offline development snapshots can remain ordinary commits unless you have a specific reason to tag them.

### Production releases vs. offline development snapshots

A project may have many saved folders but only a few production releases.

Example production versions:

```text
v1.0.0   2026-03-17
v1.1.2   2026-03-22
v1.2.0   2026-03-23
v1.3.0   2026-03-24
v1.4.0   2026-03-27
```

Example offline development snapshots:

```text
v0.1.0 through v0.1.8
v1.1.0
v1.1.1
```

Recommended interpretation:

| Version type | Recommended Git treatment |
|---|---|
| Offline snapshot | Commit only |
| Production release | Commit plus annotated tag |
| GitHub Release | Optional; create for formal published releases |

This preserves history without pretending every backup folder was formally published.

### Do not rewrite truthful history unnecessarily

If older snapshots referenced an old domain, keep that if it accurately reflects the historical state.

Example:

```text
demo.trixareforkids.com
```

Later snapshots may correctly use:

```text
demo.jeffskone.com
```

Do not retroactively rewrite older commits just to make old versions match the current domain.

Similarly, if an offline snapshot had an intermediate broken path that was fixed later, it can be preserved as part of the development history.

### Clean accidental files before import

If a historical folder contains an accidental file that should not be part of that version, remove it before committing that snapshot.

Example:

```text
v1.4.0/test.txt
```

If the file is confirmed accidental, do not include it in the reconstructed commit.

### Bulk-copy import vs. manual change import

There are two common ways to reconstruct history.

#### Method A: Bulk-copy each version folder

This is simplest:

```text
copy v0.1.0 contents into repo
git add -A
git commit -m "feat: add initial AWS microservices index"

replace contents with v0.1.1
git add -A
git commit -m "feat: add Dice microservice link"
```

Continue for each folder.

With this method, `git mv` is not required. Git can often infer renames later by comparing snapshots.

#### Method B: Manually apply each change

If you manually perform each change, use `git mv` for file moves and renames.

Example:

```powershell
git mv assets/images/errors/404/not-found.webp assets/images/errors/not-found.webp
git mv assets/images/errors/404/not-found.png assets/images/errors/not-found.png
git mv assets/images/errors/404/404trooper.gif assets/images/errors/404trooper.gif
git add assets/images/demo-microservices-preview.png
```

Use this method when you want more control over the intermediate working tree.

### Recommended commit-message style for reconstruction

Use concise Conventional Commit-style messages:

```text
type: concise description
```

Examples:

```text
feat: add Dice microservice link
fix: update canonical domain to demo.jeffskone.com
docs: add author attribution and version history
style: normalize HTML formatting
chore: refresh metadata guidance and sitemap date
```

For historical reconstruction, the message should describe what that historical snapshot introduced, not what you are doing today.

### Recommended production tag strategy

Use annotated tags for production releases.

Example:

```powershell
git tag -a v1.0.0 -m "Release v1.0.0: initial production publish. Original production publish: 2026-03-17."
```

Do not put production dates in tag names.

Recommended:

```text
v1.0.0
```

Avoid:

```text
v1.0.0-2026-03-17
prod-v1.0.0
```

Keep the tag name clean and put production context in the tag message, changelog, release notes, or deployment documentation.

### Tag immediately after committing a production version

Best practice:

```powershell
git add -A
git commit -m "chore: prepare initial production site snapshot"
git tag -a v1.0.0 -m "Release v1.0.0: initial production publish. Original production publish: 2026-03-17."
```

Then continue importing the next version.

### If you forget to tag before the next commit

That is not a problem.

Find the old commit:

```powershell
git log --oneline
```

Then tag the correct historical commit directly:

```powershell
git tag -a v1.0.0 <commit-sha> -m "Release v1.0.0: initial production publish. Original production publish: 2026-03-17."
```

The tag must point to the correct commit. The GitHub Release can be created later.

### Push commits and tags

Push the branch:

```powershell
git push -u origin main
```

Push one tag:

```powershell
git push origin v1.0.0
```

Push all intended tags only after checking them carefully:

```powershell
git push origin v1.0.0 v1.1.2 v1.2.0 v1.3.0 v1.4.0
```

Be careful with:

```powershell
git push --tags
```

It pushes all local tags, including tags you may not have intended to publish.

### GitHub Releases for reconstructed production tags

GitHub Releases are optional.

Use them when you want a formal release page with release notes and downloadable assets.

Recommended workflow:

```text
1. Create annotated production tag locally.
2. Push the tag to GitHub.
3. Create a GitHub Release from the pushed tag.
4. Add release notes explaining the production publish.
```

Do not create GitHub Releases for offline development snapshots unless you explicitly want archival release pages for them.


### Recommended GitHub Release titles

For GitHub Releases, keep release titles simple and aligned with the tag.

Recommended:

```text
v1.0.0
v1.1.2
v1.2.0
```

Also acceptable:

```text
Version 1.0.0
Release v1.0.0
```

Avoid overloading the release title with too much detail. Put the detail in the release notes.

### Recommended GitHub Release notes structure

A useful release note structure is:

```markdown
## Summary

Short explanation of what this release represents.

## Production Publish Date

YYYY-MM-DD

## Highlights

- Important change 1.
- Important change 2.
- Important change 3.

## Notes

- Any historical import notes.
- Any domain or deployment notes.
- Any known limitations.
```

Example:

```markdown
## Summary

Initial production publish of the AWS portfolio/demo site.

## Production Publish Date

2026-03-17

## Highlights

- Added initial AWS microservices index.
- Published the first production version.
- Established the baseline site structure.

## Notes

- This release was reconstructed from historical backup folders.
```

### Recommended documentation files for reconstructed sites

At minimum, use:

```text
README.md
CHANGELOG.md
```

For reconstructed website history, these can also be useful:

```text
RELEASES.md
IMPORT-NOTES.md
```

Purpose:

| File | Purpose |
|---|---|
| `README.md` | Explains what the site is, where it is deployed, and how the repository is organized |
| `CHANGELOG.md` | Summarizes notable changes by version |
| `RELEASES.md` | Lists production publish dates, production tags, release summaries, and GitHub Release notes |
| `IMPORT-NOTES.md` | Explains how historical backup folders were reconstructed into Git history |

Do not force every historical folder to contain every documentation file.

A practical policy is:

| Snapshot type | Documentation expectation |
|---|---|
| Offline development snapshot | May have minimal documentation |
| Production release snapshot | Should include release/documentation files if they existed at that stage |
| Current/latest version | Should have the best README, CHANGELOG, and release/import notes |

### Recommended future workflow after reconstruction

After the historical repository is reconstructed, stop using folder backups as the primary versioning method.

Use normal Git workflow:

```powershell
git status
git add -A
git status
git commit -m "Describe the change"
git push
```

For a production release:

```powershell
git tag -a vX.Y.Z -m "Release vX.Y.Z: short release summary. Original production publish: YYYY-MM-DD."
git push origin vX.Y.Z
```

Then optionally create a GitHub Release from the pushed tag.



---

## 28. Correcting Tag Mistakes and Understanding Tag Messages

Tag mistakes can be fixed.

The right method depends on three questions:

1. Has the tag already been pushed to GitHub?
2. Should the corrected tag point to the current commit or an older commit?
3. Is there already a GitHub Release attached to the tag?

### Three different message types

Do not confuse these:

| Message type | Stored where | Example |
|---|---|---|
| Commit message | Git commit | `feat: add Dice microservice link` |
| Annotated tag message | Git tag object | `Release v1.0.0: initial production publish.` |
| GitHub Release notes | GitHub Release page | Bulleted summary, links, publish notes |

Changing a tag message is not the same thing as changing a commit message or GitHub Release notes.

### Correct a local tag that has not been pushed

Problem:

```powershell
git tag -a v0.1.1 -m "Ve0sion 0.1.1"
```

Then:

```powershell
git tag -a v0.1.1 -m "Version 0.1.1"
```

Git reports:

```text
fatal: tag 'v0.1.1' already exists
```

If the tag has not been pushed, delete and recreate the local tag:

```powershell
git tag -d v0.1.1
git tag -a v0.1.1 -m "Version 0.1.1"
```

Verify:

```powershell
git show v0.1.1
git tag -n99 v0.1.1
```

Then push:

```powershell
git push origin v0.1.1
```

Caution:

```powershell
git tag -a v0.1.1 -m "Version 0.1.1"
```

creates the tag on the current commit, also called `HEAD`.

If the tag should point to an older commit, specify that commit explicitly.

### Correct a pushed tag on the current commit

If the tag has already been pushed and should point to the current commit, delete the remote tag, delete the local tag, recreate it, and push it again.

Example:

```powershell
git push origin --delete v0.1.1
git tag -d v0.1.1
git tag -a v0.1.1 -m "Version 0.1.1"
git push origin v0.1.1
```

Verify:

```powershell
git show v0.1.1
git tag -n99 v0.1.1
git ls-remote --tags origin v0.1.1
```

### Correct a pushed tag from several commits back

If the tag points to an older commit, save the original commit first.

PowerShell:

```powershell
$commit = git rev-list -n 1 v0.1.0
$commit
```

Then delete and recreate the tag on that same saved commit:

```powershell
git push origin --delete v0.1.0
git tag -d v0.1.0
git tag -a v0.1.0 $commit -m "Version 0.1.0"
git push origin v0.1.0
```

Verify:

```powershell
git show v0.1.0
git tag -n99 v0.1.0
git ls-remote --tags origin v0.1.0
```

### Bash equivalent

In Bash:

```bash
commit=$(git rev-list -n 1 v0.1.0)
echo "$commit"

git push origin --delete v0.1.0
git tag -d v0.1.0
git tag -a v0.1.0 "$commit" -m "Version 0.1.0"
git push origin v0.1.0
```

### What `$commit = git rev-list -n 1 v0.1.0` means

This is a PowerShell variable assignment.

```powershell
$commit = git rev-list -n 1 v0.1.0
```

`$commit` is a PowerShell variable.

`git rev-list -n 1 v0.1.0` asks Git for the commit ID pointed to by `v0.1.0`. Git's `rev-list` command lists commit objects, and `-n 1` limits the output to one commit. [R64]

This pattern is useful because it lets you delete and recreate the tag without accidentally moving it to the current commit.

### Generic safe pattern for fixing an older pushed tag

PowerShell:

```powershell
$tag = "vX.Y.Z"
$commit = git rev-list -n 1 $tag

git push origin --delete $tag
git tag -d $tag
git tag -a $tag $commit -m "Version X.Y.Z"
git push origin $tag
git show $tag
git tag -n99 $tag
git ls-remote --tags origin $tag
```

### Caution about replacing pushed tags

Replacing pushed tags can confuse other people or tools if they already fetched the old tag.

Before replacing a pushed tag, ask:

```text
Has anyone else pulled/fetched this tag?
Is a build, deployment, or release asset based on it?
Does a GitHub Release already exist for it?
```

If a GitHub Release already exists:

1. Update/delete the GitHub Release as needed.
2. Correct the tag.
3. Recreate or update the release so it points to the corrected tag.

### Checking tags locally

List tag names only:

```powershell
git tag
```

Show one tag in detail:

```powershell
git show v1.0.0
```

Show tag names with short messages:

```powershell
git tag -n
```

Show tag names with up to 99 lines of message:

```powershell
git tag -n99
```

Show one tag with up to 99 lines of message:

```powershell
git tag -n99 v1.0.0
```

### What `git tag -n99` means

`git tag` lists tags.

`-n` asks Git to show annotation lines.

`99` means show up to 99 lines of each tag message.

So:

```powershell
git tag -n99
```

means:

> List tags and show up to 99 lines of each tag annotation message.

### Viewing tags and commit messages on GitHub

GitHub shows commit messages in the commit history.

GitHub also shows tags in repository tag views and release/tag pages.

Important limitation:

> GitHub's normal file browsing interface does not always make annotated tag messages as obvious as local Git commands do.

For precise tag-message inspection, use local Git commands such as:

```powershell
git show v1.0.0
git tag -n99 v1.0.0
```

### Proper terminology for pushed tags

Use:

```text
Push the tag to GitHub.
Push the tag to origin.
Publish the tag.
```

Avoid:

```text
Commit the tag.
```

You commit changes, then create a tag, then push the tag.



---

## 29. Line Endings, LF, CRLF, and `.gitattributes`

On Windows, Git may warn about line endings.

Example warning:

```text
warning: in the working copy of 'index.html', LF will be replaced by CRLF the next time Git touches it
```

This is usually not an error.

It means Git noticed line-ending differences between the repository-normalized content and the working-copy content.

### LF vs. CRLF

| Term | Meaning | Common platform |
|---|---|---|
| `LF` | Line Feed | Linux, macOS, Git repository normalization |
| `CRLF` | Carriage Return + Line Feed | Windows |

A text file can look normal in an editor while still using different line endings internally.

### What Git is warning about

The warning means something like:

> Git sees LF line endings now, but based on your Git settings or repository attributes, the file may be written with CRLF line endings in your Windows working copy later.

This often happens when Git is configured with Windows-friendly line-ending behavior, such as `core.autocrlf=true`, or when `.gitattributes` requests CRLF for certain text files. Git's configuration documentation covers line-ending conversion settings such as `core.autocrlf`. [R65]

### What is being fixed?

The goal is not to make every file use the same line endings everywhere.

The goal is to make line-ending behavior explicit and predictable.

A good policy is:

```text
Repository-normalized text = consistent
Windows working files       = comfortable for Windows tools
Shell scripts               = LF so they work on Unix/Linux
Binary files                = never line-ending converted
```

### Recommended fix: add `.gitattributes`

Create a file named:

```text
.gitattributes
```

in the repository root.

Recommended Windows-friendly starter content:

```gitattributes
# Normalize text files in the repository.
* text=auto

# Common website/documentation text files.
*.html text eol=crlf
*.css  text eol=crlf
*.js   text eol=crlf
*.md   text eol=crlf
*.txt  text eol=crlf
*.xml  text eol=crlf
*.svg  text eol=crlf
*.json text eol=crlf

# PowerShell scripts should use Windows line endings.
*.ps1 text eol=crlf

# Unix/Linux shell scripts should use LF.
*.sh text eol=lf

# Images and binary files should never be line-ending converted.
*.png  binary
*.jpg  binary
*.jpeg binary
*.gif  binary
*.ico  binary
*.webp binary
```

Git's attributes documentation describes using `.gitattributes` to set path-specific attributes, including text and end-of-line behavior. [R66]

This style is especially useful for a Windows-managed documentation or website repository where you intentionally want CRLF in common working-copy text files.

### What to do before the first commit

If the line-ending warning appears before the first commit, fix it before committing.

PowerShell workflow:

```powershell
git reset
notepad .gitattributes
git add .gitattributes
git add .
git status
```

Then commit:

```powershell
git commit -m "feat: add initial AWS microservices index"
```

What the commands do:

| Command | Purpose |
|---|---|
| `git reset` | Unstages files that were already staged |
| `notepad .gitattributes` | Creates or edits `.gitattributes` |
| `git add .gitattributes` | Stages the line-ending rules |
| `git add .` | Stages project files again using the new attributes |
| `git status` | Confirms what is staged |

### Inspect line endings in Git

Use:

```powershell
git ls-files --eol
```

Example output:

```text
i/lf    w/crlf  attr/text eol=crlf  index.html
```

Meaning:

| Part | Meaning |
|---|---|
| `i/lf` | Git index/repository-normalized version uses LF |
| `w/crlf` | Working copy uses CRLF |
| `attr/text eol=crlf` | `.gitattributes` requests CRLF in the working copy |

For a Windows-managed repository, this can be normal and expected.

Git's `git ls-files` documentation includes the `--eol` option for showing end-of-line information. [R67]

### Risks of ignoring LF/CRLF warnings

For a static website, the website behavior risk is usually low.

The Git/history risk can still matter.

Possible problems:

```text
1. Repeated line-ending warnings.
2. Git diffs showing entire files changed because of line endings.
3. Future commits including line-ending-only changes.
4. Harder comparison between historical versions.
5. Noisier merge conflicts.
6. Cross-platform inconsistency.
7. Scripts breaking if they receive the wrong line endings.
```

The biggest technical risk is scripts.

A Linux shell script with CRLF line endings can fail with errors like:

```text
/bin/bash^M: bad interpreter
```

That is why `.sh` files should generally stay LF, even if the repo is managed on Windows.

### Bottom line

When Git warns:

```text
LF will be replaced by CRLF the next time Git touches it
```

read it as:

> Git detected LF line endings in a file that may be written with CRLF line endings in the Windows working copy.

It is usually not fatal, but it is a good reason to add `.gitattributes` early.



---

## 30. Correcting Commit Message Mistakes

Commit-message mistakes are different from tag-message mistakes.

A commit message is part of the commit object. If you change a commit message, Git creates a replacement commit with a new commit hash. Even if the file content is unchanged, the commit hash changes because the commit metadata changed.

The central rule is:

> Fixing a commit message rewrites history for that commit and any descendant commits.

So the safe method depends on whether the commit has already been pushed or shared.

Git's `git commit` documentation describes `--amend` as replacing the tip of the current branch by creating a new commit. [R69] Git's interactive rebase documentation says that to edit a commit message during an interactive rebase, replace `pick` with `reword`. [R70]

### Commit messages vs. tag messages vs. release notes

Do not confuse these:

| Thing | Stored where | Example | Correction method |
|---|---|---|---|
| Commit message | Git commit object | `feat: add Dice service link` | Amend or rebase/reword commit |
| Annotated tag message | Git tag object | `Version 1.8.0` | Delete/recreate tag, preserving target commit if needed |
| GitHub Release notes | GitHub Release page | Release summary/body | Edit GitHub Release notes |

Changing a commit message is not the same thing as changing an annotated tag message.

### Quickly check commit messages across a repository

Show recent commit messages:

```bash
git log --oneline
```

Show all reachable commit messages:

```bash
git log --all --oneline
```

Show commit messages with short dates:

```bash
git log --all --date=short --format="%h %ad %s"
```

Show the full latest commit metadata and message:

```bash
git show --no-patch --format=fuller HEAD
```

Show a specific commit:

```bash
git show --no-patch --format=fuller <commit-sha>
```

Show only the latest commit message:

```bash
git log -1 --format=%B
```

Show only a specific commit message:

```bash
git log -1 --format=%B <commit-sha>
```

### Search commit messages for a typo

Use `git log --grep`. Git's `git log` documentation describes `git log` as showing commit logs; its revision filtering options include grep-style message matching. [R68]

Search all reachable commit messages for an exact typo:

```bash
git log --all --grep="Ve0sion" --oneline
```

Search case-insensitively:

```bash
git log --all --regexp-ignore-case --grep="ve0sion" --oneline
```

Search with useful context:

```bash
git log --all --grep="Ve0sion" --date=short --format="%h %ad %an %s"
```

Search only the current branch:

```bash
git log --grep="Ve0sion" --oneline
```

Search all branches and tags:

```bash
git log --all --grep="Ve0sion" --oneline
```

Search for several likely misspellings:

```bash
git log --all --grep="Ve0sion" --oneline
git log --all --grep="Versoin" --oneline
git log --all --grep="Verison" --oneline
git log --all --grep="Vesion" --oneline
```

PowerShell helper:

```powershell
$patterns = @("Ve0sion", "Versoin", "Verison", "Vesion")

foreach ($pattern in $patterns) {
    Write-Host ""
    Write-Host "Searching for: $pattern"
    git log --all --grep="$pattern" --date=short --format="%h %ad %an %s"
}
```

Important:

```text
git log --grep searches commit messages.
git grep searches tracked file contents.
```

For commit-message misspellings, use `git log --grep`.

### Fix the most recent commit message

Use this when the bad commit is the latest commit on the current branch.

Check first:

```bash
git log -1 --oneline
git show --no-patch --format=fuller HEAD
```

Fix with a one-line message:

```bash
git commit --amend -m "Corrected commit message"
```

Example:

```bash
git commit --amend -m "docs: update version references"
```

Fix with a subject and body:

```bash
git commit --amend -m "docs: update version references" -m "Correct misspelled version wording in the commit message and clarify the documentation update scope."
```

Verify:

```bash
git log -1 --oneline
git show --no-patch --format=fuller HEAD
```

If the commit has not been pushed, this is usually safe.

If it has already been pushed, amending it changes the commit hash and the remote branch will still point to the old commit until you push the rewritten history.

### Fix an older commit message

Use interactive rebase with `reword`.

Find the bad commit:

```bash
git log --oneline
```

Example:

```text
9f8e7d6 docs: update changelog
a1b2c3d docs: update versoin references
123abcd docs: add quick-start guide
```

Start an interactive rebase from before the bad commit:

```bash
git rebase -i <bad-commit-sha>~1
```

Example:

```bash
git rebase -i a1b2c3d~1
```

Git opens an editor with a list like this:

```text
pick a1b2c3d docs: update versoin references
pick 9f8e7d6 docs: update changelog
```

Change only the bad commit line from `pick` to `reword`:

```text
reword a1b2c3d docs: update versoin references
pick 9f8e7d6 docs: update changelog
```

Save and close the editor.

Git then opens the selected commit message. Correct the message, save, and close.

Verify:

```bash
git log --oneline
```

Important:

```text
The corrected commit has a new hash.
Any later commits replayed by the rebase also get new hashes.
```

### Fix the root commit message

If the misspelled commit is the first commit in the repository, there is no earlier parent commit.

Use:

```bash
git rebase -i --root
```

Then change `pick` to `reword` for the root commit.

This rewrites the root commit and every later commit. Use this only before pushing, or only when you fully understand the impact.

### What changes if the commit was already pushed?

If the commit was already pushed, correcting its message rewrites published history.

A normal push may fail:

```bash
git push
```

because your local branch history no longer matches the remote branch history.

If it is safe to rewrite the remote branch, use:

```bash
git push --force-with-lease
```

Git's `git push` documentation says `--force-with-lease` protects remote refs being updated by requiring their current value to match what your local remote-tracking branch expects. [R71]

Preferred:

```bash
git push --force-with-lease
```

Avoid unless you have a very specific reason:

```bash
git push --force
```

`--force-with-lease` is still a force push, but it adds a safety check that can prevent overwriting someone else's newer remote work.

### When `git push --force-with-lease` is reasonable

Use it only when all of these are true:

```text
1. You understand that commit hashes will change.
2. The branch is your private branch, or everyone sharing it agrees.
3. You have checked that nobody else pushed new work.
4. The branch is not protected, or you have permission to rewrite it.
5. No release, deployment, tag, or other process depends on the old commit hash.
```

Typical acceptable cases:

- your own feature branch;
- a branch nobody else uses;
- a pull request branch where rebasing is accepted;
- an unprotected documentation branch you control.

### When not to rewrite history

Do not rewrite history just to fix a commit-message typo when:

- the branch is shared by other people;
- the branch is `main` and already published;
- the branch is protected;
- a CI/CD process already built or deployed that commit;
- a tag points to the old commit;
- a GitHub Release points to a tag based on the old commit;
- other people may have based work on the old commit;
- the typo is minor and does not affect understanding;
- the correction would cause more confusion than the typo.

In those cases, prefer one of these:

1. Leave the typo alone.
2. Correct the wording in `CHANGELOG.md` or release notes.
3. Add a later documentation commit if actual files need clarification.
4. Mention the typo in import notes if historical accuracy matters.

For a commit-message typo only, a follow-up commit that changes no files is usually not useful.

### If a tag points to the commit being rewritten

If a tag points to the old commit and you rewrite that commit, the tag still points to the old commit.

Before rewriting a tagged commit, ask:

```text
Is this tag already pushed?
Is this a production tag?
Is there a GitHub Release attached to it?
Has anything been deployed from it?
```

If the tag should move to the corrected commit, correct the tag separately after the commit rewrite. That may require deleting and recreating the tag, and it may also require updating a GitHub Release.

Use the tag-correction guidance in [Section 28](#28-correcting-tag-mistakes-and-understanding-tag-messages) before replacing a pushed tag.

### Safe workflow: latest unpushed commit

```bash
git log -1 --oneline
git commit --amend -m "Corrected commit message"
git log -1 --oneline
git push
```

### Safe workflow: older unpushed commit

```bash
git log --oneline
git rebase -i <bad-commit-sha>~1
```

In the editor, change:

```text
pick <bad-commit-sha> old misspelled message
```

to:

```text
reword <bad-commit-sha> old misspelled message
```

Then verify:

```bash
git log --oneline
```

If the branch has never been pushed, push normally:

```bash
git push -u origin branch-name
```

### Safe workflow: latest pushed commit on a private branch

```bash
git log -1 --oneline
git commit --amend -m "Corrected commit message"
git log -1 --oneline
git push --force-with-lease
```

Use only when it is safe to rewrite that branch.

### Safe workflow: older pushed commit on a private branch

```bash
git log --oneline
git rebase -i <bad-commit-sha>~1
git log --oneline
git push --force-with-lease
```

Use only when it is safe to rewrite that branch.

### Abort or continue an interactive rebase

Abort if you decide not to continue:

```bash
git rebase --abort
```

Continue after resolving a stopped rebase:

```bash
git rebase --continue
```

### PowerShell examples

Most Git commands are the same in PowerShell:

```powershell
git rebase -i a1b2c3d~1
git commit --amend -m "docs: update version references"
```

For a commit subject and body:

```powershell
git commit --amend `
  -m "docs: update version references" `
  -m "Correct the commit message typo and clarify the documentation update scope."
```

PowerShell here-string body:

```powershell
$body = @"
Correct the commit message typo and clarify the documentation update scope.

This commit message was amended before the branch was shared.
"@

git commit --amend -m "docs: update version references" -m $body
```



---

## 31. Commit Message Prefixes and When to Use Them

Commit message prefixes such as `feat`, `fix`, `docs`, `chore`, and `refactor` are not Git commands.

Git does not require them, and Git does not enforce them by default.

They are a human convention. The value comes from consistency.

A common pattern is:

```text
type: short imperative summary
```

Example:

```bash
git commit -m "feat: expand demo index into AWS portfolio"
```

A longer commit can include a body:

```bash
git commit -m "feat: expand demo index into AWS portfolio" -m "Update the site title, subtitle, metadata, README, changelog, release notes, and sitemap for v2.1.0. Move Anagram from Microservices to Web Applications while preserving the existing layout and preview image."
```

### Why prefixes are useful

Prefixes make commit history easier to:

- scan;
- search;
- group by type of change;
- summarize in changelogs;
- review when preparing tags or releases;
- understand later when reconstructing why a version changed.

Git sees this:

```text
feat: expand demo index into AWS portfolio
```

as ordinary commit message text.

The prefix is for humans and tooling that chooses to interpret the convention.

### Recommended prefix ranking for this guide workflow

This ranking is based on practical usefulness for documentation repositories, website repositories, release packages, and small project/versioned file sets.

| Rank | Prefix | Meaning | Most useful when |
|---:|---|---|---|
| 1 | `feat` | Feature | A user-visible capability, page, endpoint, section, or meaningful content structure is added or expanded |
| 2 | `fix` | Bug fix | Something incorrect, broken, misleading, stale, or malfunctioning is corrected |
| 3 | `docs` | Documentation | README, guide, changelog, release notes, comments, or explanatory text are updated without changing functional behavior |
| 4 | `chore` | Maintenance | Routine upkeep, release preparation, metadata refresh, housekeeping, or non-user-facing maintenance |
| 5 | `refactor` | Internal restructuring | Code or structure is reorganized without changing visible behavior |
| 6 | `style` | Formatting only | Whitespace, indentation, line endings, formatting, or visual/code style changes without meaningfully changing content or behavior |
| 7 | `test` | Tests | Test files, test cases, test data, or test infrastructure are added or changed |
| 8 | `build` | Build/dependency system | Build scripts, package files, Dockerfiles, dependency manifests, or generated build configuration change |
| 9 | `ci` | Continuous integration | GitHub Actions, CI/CD pipelines, deployment automation, or validation workflows change |
| 10 | `perf` | Performance | A change primarily improves speed, size, load time, or efficiency |
| 11 | `revert` | Revert | A previous commit is intentionally undone |
| 12 | `release` | Release marker/custom convention | Optional custom prefix for release-only commits, but often `chore` is better |

### `feat`

Use `feat` when the change adds, expands, or meaningfully changes something user-facing.

Examples:

```bash
git commit -m "feat: expand demo index into AWS portfolio"
git commit -m "feat: add Anagram web application section"
git commit -m "feat: add Dice microservice link"
git commit -m "feat: add website section placeholder"
```

Use `feat` when:

- a visible page changes in a meaningful way;
- a new section, endpoint, guide, app, feature, or user-facing capability is added;
- a project grows beyond its previous purpose;
- metadata and documentation are updated as part of a visible feature release.

For example, changing a live site from a microservices-only index into a broader AWS portfolio is better described with `feat:` than `docs:` or `chore:` because the user-visible site changed.

### `fix`

Use `fix` when correcting something wrong.

Examples:

```bash
git commit -m "fix: correct canonical domain"
git commit -m "fix: update stale Open Graph metadata"
git commit -m "fix: move Anagram out of microservices section"
git commit -m "fix: correct typo in release tag message guidance"
```

Use `fix` when:

- a URL is wrong;
- metadata is stale or incorrect;
- a link is broken;
- a typo changes meaning or looks unprofessional;
- a service appears under the wrong section;
- a deployment problem is corrected;
- an accessibility issue is corrected.

Do not overuse `fix` for ordinary wording improvements. If the change is simply making documentation clearer, `docs:` is usually better.

### `docs`

Use `docs` for documentation-only changes.

Examples:

```bash
git commit -m "docs: add AWS S3 static website quick start guide"
git commit -m "docs: update README with primary site URL and alias"
git commit -m "docs: add Git tag message correction guidance"
git commit -m "docs: document commit message prefixes"
```

Use `docs` when:

- the README changes;
- a guide changes;
- a changelog or release note changes;
- comments or explanatory text are updated;
- usage examples are added;
- no live behavior or visible product feature changes.

If the only changed files are `README.md`, `CHANGELOG.md`, or guide files, `docs:` is usually correct.

If `index.html` changes the live visible site in a meaningful way, use `feat:` or `fix:` depending on the reason.

### `chore`

`chore` is not an acronym. It means routine maintenance.

Examples:

```bash
git commit -m "chore: prepare v2.1.0 release"
git commit -m "chore: refresh sitemap lastmod date"
git commit -m "chore: normalize line endings"
git commit -m "chore: update project metadata"
```

Use `chore` when:

- preparing a release;
- updating metadata that does not change visible behavior;
- cleaning generated files;
- updating housekeeping files;
- normalizing line endings;
- refreshing dates;
- updating non-functional project settings.

Do not use `chore` as a junk drawer. If the change is a real feature, fix, or documentation update, use the more specific prefix.

### `refactor`

Use `refactor` when the structure changes but visible behavior is intended to stay the same.

Examples:

```bash
git commit -m "refactor: reorganize error image assets"
git commit -m "refactor: split metadata helpers"
git commit -m "refactor: simplify service card markup"
```

Use `refactor` when:

- code is reorganized without intended behavior change;
- files move to clearer locations;
- repeated code or markup is simplified;
- internal structure improves but users should not see a functional difference.

If the refactor also changes visible behavior, consider `feat:` or `fix:` instead.

### `style`

Use `style` for formatting-only changes.

Examples:

```bash
git commit -m "style: normalize HTML indentation"
git commit -m "style: format markdown tables"
git commit -m "style: normalize line endings"
```

Use `style` when:

- indentation changes;
- whitespace changes;
- Markdown table formatting changes;
- line endings change;
- quote style or semicolon style changes;
- code formatting changes without changing meaning.

Do not use `style` for visual design changes to a website. If the user-visible page design changes, `feat:` or `fix:` may be better.

### `test`

Use `test` when test-related files or validation workflows change.

Examples:

```bash
git commit -m "test: add homepage metadata checks"
git commit -m "test: add link validation script"
git commit -m "test: update accessibility test cases"
```

### `build`

Use `build` when build tooling, dependency configuration, or package infrastructure changes.

Examples:

```bash
git commit -m "build: update Dockerfile"
git commit -m "build: update package lockfile"
git commit -m "build: add static site build script"
```

### `ci`

Use `ci` when continuous integration or deployment automation changes.

Examples:

```bash
git commit -m "ci: add link-check workflow"
git commit -m "ci: update GitHub Actions deployment workflow"
git commit -m "ci: run markdown validation on pull requests"
```

### `perf`

Use `perf` when the main point is performance.

Examples:

```bash
git commit -m "perf: reduce homepage image size"
git commit -m "perf: lazy-load preview image"
git commit -m "perf: minimize static CSS"
```

### `revert`

Use `revert` when intentionally undoing an earlier commit.

Examples:

```bash
git commit -m "revert: restore previous metadata layout"
git commit -m "revert: undo sitemap date refresh"
```

When possible, use Git's revert command because it creates a normal inverse commit:

```bash
git revert <commit-sha>
```

### `release`

`release` can be used as a custom prefix, but it is optional.

Examples:

```bash
git commit -m "release: prepare v2.1.0"
git commit -m "release: publish v1.4.0 assets"
```

For many small projects, `chore:` is usually enough:

```bash
git commit -m "chore: prepare v2.1.0 release"
```

Use `release:` only if you want release-only commits to stand out.

### Choosing the best prefix

Ask these questions in order:

| Question | Prefix |
|---|---|
| Did the live product, site, app, endpoint, or guide gain meaningful new user-facing content? | `feat` |
| Did the change correct something wrong, broken, stale, misleading, or misplaced? | `fix` |
| Did only documentation, comments, release notes, or guides change? | `docs` |
| Was this routine release prep, metadata refresh, housekeeping, or maintenance? | `chore` |
| Did the internal structure change without intended visible behavior change? | `refactor` |
| Did only formatting, whitespace, line endings, or style change? | `style` |
| Did tests or validation change? | `test` |
| Did build/dependency files change? | `build` |
| Did GitHub Actions, CI, or deployment automation change? | `ci` |
| Did performance improve? | `perf` |
| Did the commit undo a previous commit? | `revert` |

### Commit messages vs. tag messages

Commit messages, tag names, tag messages, and GitHub Release notes are related, but not the same thing.

| Item | Example | Purpose |
|---|---|---|
| Commit message | `feat: expand demo index into AWS portfolio` | Describes one commit |
| Tag name | `v2.1.0` | Identifies a version point |
| Annotated tag message | `Version 2.1.0` | Describes the tag |
| GitHub Release title | `v2.1.0` | Title for a GitHub Release |
| GitHub Release notes | Bulleted release summary | Explains the release |

Commit prefixes belong in commit messages, not tag names.

Recommended tag name:

```text
v2.1.0
```

Recommended annotated tag message:

```text
Version 2.1.0
```

Avoid:

```text
feat: v2.1.0
```

as a tag name or tag message.

### Multiple `-m` options

A commit can use multiple `-m` options.

For commits, the first `-m` becomes the subject and the later `-m` values become body paragraphs.

Example:

```bash
git commit -m "feat: expand demo index into AWS portfolio" -m "Update the site title, subtitle, metadata, README, changelog, release notes, and sitemap for v2.1.0. Move Anagram from Microservices to Web Applications while preserving the existing layout and preview image."
```

Annotated tags can also use multiple `-m` options when you want a longer tag annotation, but simple version tags usually only need one concise tag message:

```bash
git tag -a v2.1.0 -m "Version 2.1.0"
```

### Recommended subject style

Use this style:

```text
type: imperative summary
```

Recommended:

```text
docs: document commit message prefixes
fix: correct canonical domain
feat: add Anagram web application section
chore: prepare v2.1.0 release
```

Guidelines:

- use lowercase prefixes;
- use the imperative mood when practical;
- keep the subject concise;
- do not end the subject with a period;
- use a body when the reason or context matters.

### Optional scopes

A scope can clarify the area being changed.

Pattern:

```text
type(scope): summary
```

Examples:

```bash
git commit -m "docs(readme): add repository navigation"
git commit -m "fix(metadata): correct canonical domain"
git commit -m "feat(portfolio): add web applications section"
```

Scopes are optional. Use them when they make the message clearer.

### Breaking changes

For breaking changes, use a `!` after the type or scope and explain the breaking change in the body.

Examples:

```bash
git commit -m "feat!: replace guide structure" -m "BREAKING CHANGE: The guide section order and anchor names changed."
git commit -m "feat(api)!: change response format" -m "BREAKING CHANGE: Clients must update JSON parsing."
```

For documentation repositories, breaking changes are less common, but they can happen if a guide is reorganized in a way that breaks anchors, links, or instructions.

### Recommended defaults for this workflow

Use these defaults:

| Situation | Recommended prefix |
|---|---|
| Main guide or companion guide updated | `docs` |
| New guide section or appendix added | `docs` |
| Broken link fixed | `fix` |
| Incorrect guidance corrected | `fix` |
| Stable filename link patch | `fix` |
| Release prep only | `chore` |
| Sitemap/date/metadata housekeeping only | `chore` |
| Formatting-only Markdown cleanup | `style` |
| Line-ending-only normalization | `style` or `chore` |
| Site gains new visible section/app/content | `feat` |
| Site content corrected or moved to the right section | `fix` |



---

## 32. Push, Tag, Branch, and Repository Hygiene Workflows

This section gathers practical repository-maintenance guidance for careful versioned file-set work.

It covers:

- when plain `git push` behaves like `git push origin main`;
- why branch pushes and tag pushes are different;
- a repeatable commit, push, and tag checklist;
- when to work directly on `main` versus a working branch;
- recommended repository folders;
- `.gitignore`;
- `.gitkeep`;
- GitHub topics;
- line-ending policy reminders.

### Is `git push` the same as `git push origin main`?

Sometimes, yes, in a specific repository state.

If you are on `main`, and local `main` is tracking `origin/main`, then:

```powershell
git push
```

usually behaves like:

```powershell
git push origin main
```

A status message like this means the current branch and upstream are aligned:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

That tells you:

- the current local branch is `main`;
- local `main` tracks `origin/main`;
- there are no staged, unstaged, or untracked changes that Git is reporting;
- local `main` and remote `origin/main` are currently aligned.

However, plain `git push` is not universally identical to `git push origin main`.

A safer mental model:

```text
git push
```

means:

```text
Push the current branch according to its configured upstream and push settings.
```

Whereas:

```text
git push origin main
```

means:

```text
Push local main to the remote named origin.
```

For careful versioned guide, website, or historical-import workflows, the explicit command is often better:

```powershell
git push origin main
```

Git's `git push` documentation describes pushing local refs to remote refs; this is why being explicit about remote and branch can reduce ambiguity. [R22]

### Why branch pushes and tag pushes both matter

A commit, branch, and tag are related but different.

```text
Commit = saved snapshot of the file tree
Branch = movable pointer to the latest commit in a line of work
Tag    = fixed label pointing to a specific commit
```

Example:

```text
A -- B -- C
          ^
          main
          v1.20.0
```

Here, `main` and `v1.20.0` both point to commit `C`, but they serve different purposes:

- `main` moves forward as new commits are added;
- `v1.20.0` stays fixed unless deliberately changed;
- the tag identifies a specific version or release;
- the branch identifies the current line of development.

Pushing a tag:

```powershell
git push origin v1.20.0
```

pushes the tag. If the remote does not yet have the commit pointed to by the tag, Git can transfer the objects needed by that tag.

But pushing only the tag does not necessarily update the remote branch pointer.

That can create a confusing state:

```text
origin/main  -> older commit
v1.20.0      -> newer commit
```

The version tag exists on GitHub, but the default branch may still show older files.

For a normal version workflow, push both:

```powershell
git push origin main
git push origin v1.20.0
```

For careful historical imports, pushing one intended tag at a time is usually safer than pushing every local tag:

```powershell
git push origin main
git push origin v1.20.0
```

Avoid casual use of:

```powershell
git push --tags
```

unless you have checked that every local tag should be published.

### Consequences of not pushing `main`

If you push only tags but not the branch, the repository may still be recoverable, but it can be harder to understand.

| Area | Possible consequence |
|---|---|
| GitHub default branch view | May show old files instead of the latest version |
| GitHub commit history on `main` | May omit commits that only exist through tags |
| Releases/tags page | May show version tags correctly |
| Deployment workflows | Anything deploying from `main` may deploy an old version |
| Clones/checkouts | Users may not get the expected latest branch state |
| Repo auditability | History can look confusing because tags point to commits not visible on the pushed branch line |

Check whether local `main` has unpushed commits:

```powershell
git status
```

If it says:

```text
Your branch is up to date with 'origin/main'.
```

then local `main` and remote `origin/main` are aligned.

If it says:

```text
Your branch is ahead of 'origin/main' by 1 commit.
```

then local commits exist that have not yet been pushed to the remote branch.

Useful verification commands:

```powershell
git log --oneline --decorate -10
git log --oneline --decorate --graph --all
git log --oneline origin/main..main
git log --oneline main..origin/main
git tag --list
git show v1.20.0
```

### Recommended commit, push, and tag sequence

For careful versioned website or guide repos, use a repeatable checklist:

```powershell
git status
git add -A
git status
git commit -m "type: concise subject" -m "Longer body explaining what changed and why."
git push origin main

git tag -a v1.20.0 -m "Release v1.20.0: production cleanup release published on 2026-07-06."
git push origin v1.20.0
```

Use `git add -A` for full version snapshots because it stages additions, modifications, deletions, and renamed/deleted paths across the working tree. [R19]

Check `git status` before and after staging:

| When | Why |
|---|---|
| Before `git add -A` | See what changed before staging |
| After `git add -A` | Confirm what will be committed |
| After commit | Confirm the working tree is clean |
| After push | Confirm local and remote branch alignment if needed |

Example release-style commit messages:

```powershell
git commit -m "feat: expand demo index into AWS portfolio" -m "Update the site title, subtitle, metadata, README, changelog, release notes, and sitemap for v2.1.0."
git commit -m "fix: correct canonical domain references" -m "Update metadata, README, and release notes to use the canonical demo.jeffskone.com domain."
git commit -m "docs: document git push and tag workflow" -m "Add guidance explaining branch pushes, tag pushes, upstream tracking, and version-release verification."
git commit -m "chore: prepare v1.20.0 release" -m "Refresh metadata and release documentation before tagging v1.20.0."
```

### First `-m` vs. second `-m`

In this command:

```powershell
git commit -m "docs: document git push and tag workflow" -m "Add guidance explaining branch pushes, tag pushes, upstream tracking, and version-release verification."
```

the first `-m` creates the commit subject.

The second `-m` creates the commit body.

View subjects only:

```powershell
git log --oneline
```

View full messages:

```powershell
git log --format=fuller
```

View a single latest message:

```powershell
git show --no-patch --format=fuller HEAD
```

### Checking out branches before committing and pushing

There are three common states.

#### Option A: commit directly on `main`

This is simplest:

```powershell
git switch main
git pull
git status
git add -A
git commit -m "docs: update guide"
git push origin main
```

Pros:

- simple;
- good for solo/personal repos;
- fewer branch-management steps.

Cons:

- less review structure;
- easier to mix unrelated changes;
- less suitable for team repos.

#### Option B: create a working branch, then merge into `main`

```powershell
git switch main
git pull
git switch -c update-guide
git add -A
git commit -m "docs: update guide"
git push -u origin update-guide
```

After review or self-check:

```powershell
git switch main
git pull
git merge update-guide
git push origin main
```

Pros:

- safer;
- easier review;
- better for pull requests;
- cleaner isolation for changes.

Cons:

- more steps;
- branch cleanup needed later.

#### Option C: detached `HEAD`

This can happen when you check out a tag or commit directly:

```powershell
git switch --detach v1.20.0
```

Detached `HEAD` is useful for inspection, but not ideal for normal committing.

If you need to edit from that point, create a branch:

```powershell
git switch -c fix-from-v1.20.0
```

### Recommended repo folders

Repository structure should support how the project is actually used.

Common folders:

| Folder | Purpose |
|---|---|
| `docs/` | Additional documentation, guides, diagrams, or notes |
| `archive/` | Old reference material kept intentionally but not active |
| `assets/` | Images, icons, CSS assets, screenshots, or downloadable resources |
| `src/` or `source/` | Source code or source content |
| `public/`, `dist/`, or `site/` | Published/static/generated website output, depending on project |
| `scripts/` | Helper scripts for build, release, validation, or maintenance |
| `.github/` | GitHub-specific files, such as workflows, issue templates, or pull request templates |

Suggested simple static-site structure:

```text
README.md
CHANGELOG.md
index.html
style.css
script.js
assets/
docs/
scripts/
.github/
```

Use `archive/` only for material that has long-term historical value. Do not let it become a dumping ground.

### `.gitignore`: what it is and how to use it

`.gitignore` tells Git which untracked files to ignore.

It does not remove files that are already tracked.

Git's `gitignore` documentation describes ignore patterns for intentionally untracked files. [R72]

Common starter example:

```gitignore
# Windows
Thumbs.db
Desktop.ini

# macOS
.DS_Store

# Logs
*.log

# Temporary files
*.tmp
*.bak
*.swp

# Build output
bin/
obj/
dist/
build/

# Local environment files
.env
.env.*

# Editor folders
.vscode/
.idea/

# Archives generated locally
*.zip
*.7z
```

Important:

> `.gitignore` only ignores untracked files.

If a file is already tracked, adding it to `.gitignore` does not stop tracking it.

To stop tracking a file but keep it locally:

```powershell
git rm --cached file-name
```

Then commit the change.

For guide/website repos, create `.gitignore` early, before the first commit when possible.

### `.gitkeep`: what it is and how to use it

Git does not track empty folders.

A `.gitkeep` file is a common placeholder file used to keep an otherwise-empty folder in the repository.

Example:

```text
logs/.gitkeep
exports/.gitkeep
```

Then:

```powershell
git add logs/.gitkeep
git commit -m "chore: keep logs folder placeholder"
```

Use `.gitkeep` when:

- the folder needs to exist;
- the folder is currently empty;
- future scripts or docs expect that folder path.

Do not use `.gitkeep` when:

- the folder already contains tracked files;
- the folder is generated and should not be tracked;
- the folder is only temporary.

`.gitkeep` is a convention, not a special Git feature.

### GitHub topics

GitHub topics are short repository metadata tags that help classify a repository.

Examples:

```text
git
github
documentation
versioning
static-site
aws
cloudfront
s3
```

Pros:

- helps organize repositories;
- improves discoverability;
- makes a repo easier to understand at a glance.

Cons:

- easy to overdo;
- not a substitute for README content;
- needs occasional cleanup if the project changes.

Use a small set of accurate topics.

GitHub's repository topic documentation describes topics as a way to classify repositories and make them more discoverable. [R73]

### LF vs. CRLF and `.gitattributes` reminder

The detailed line-ending guidance is in [Section 29](#29-line-endings-lf-crlf-and-gitattributes).

High-confidence policy:

| File type | Recommended line ending |
|---|---|
| General text in repository | Usually normalize to LF in the repository |
| Windows working copy | CRLF may be acceptable depending on `.gitattributes` |
| Shell scripts `.sh` | LF |
| PowerShell scripts `.ps1` | CRLF is acceptable |
| Binary files | No line-ending conversion |

A portable static website policy is:

```gitattributes
# Auto-detect text files and normalize them to LF in the repository
* text=auto

# Explicit text formats
*.html text eol=lf
*.css  text eol=lf
*.js   text eol=lf
*.json text eol=lf
*.md   text eol=lf
*.txt  text eol=lf
*.xml  text eol=lf
*.svg  text eol=lf

# Windows PowerShell
*.ps1 text eol=crlf

# Unix/Linux shell scripts
*.sh text eol=lf

# Binary files
*.png  binary
*.jpg  binary
*.jpeg binary
*.gif  binary
*.ico  binary
*.webp binary
```

If your repo intentionally wants CRLF for common documentation and website files, that is also acceptable. The important thing is to make the policy explicit in `.gitattributes`, then verify with:

```powershell
git ls-files --eol
```

Git's `gitattributes` documentation covers text/eol attributes, and Git's `git ls-files` documentation includes `--eol` for inspecting end-of-line behavior. [R66] [R67]



---

## 33. GitHub File Search, Tag Inspection, and Commit History Lookup

This section collects quick lookup workflows for three common questions:

- How do I search inside the file I am viewing on GitHub?
- How do I list and inspect version tags or GitHub Releases?
- How do I review or search commit messages?

Some of these commands already appear elsewhere in the guide. This section groups the most useful inspection commands together so they are easier to find.

### Search only the file currently open on GitHub

If you are already viewing a file on GitHub and only want to search inside that file, use your browser's Find command:

```text
Windows/Linux: Ctrl+F
Mac: Cmd+F
```

That is usually the fastest and most precise method.

For larger files or an editor-like experience, press:

```text
.
```

while viewing the repository or file on GitHub. This opens GitHub's web editor. Then use:

```text
Ctrl+F
```

or:

```text
Cmd+F
```

to search inside the open file.

### Search a specific path with GitHub search

GitHub's search bar can be limited to a path by using `path:`.

Pattern:

```text
search-term path:folder/subfolder/filename.ext
```

Example:

```text
force-with-lease path:git-repository-guide.md
```

When using the GitHub search bar, make sure the search is limited to the current repository if you do not want results from all of GitHub.

For a file you already have open, prefer `Ctrl+F` or `Cmd+F`.

### Use symbols for code files

For some source-code files, GitHub can show a symbols or outline pane. Use it when you want to jump to:

- a function;
- a class;
- a method;
- a variable;
- another code symbol.

This is useful for navigating code definitions, but it is not a replacement for general text search.

### Practical GitHub file-search ranking

| Rank | Method | Best use |
|---:|---|---|
| 1 | Browser Find, `Ctrl+F` or `Cmd+F` | Search the currently open file |
| 2 | GitHub web editor, `.` then `Ctrl+F` or `Cmd+F` | Search or navigate a larger file in an editor-like view |
| 3 | GitHub search bar with `path:` | Search a specific file path from the repository search interface |
| 4 | Symbols pane | Jump to functions, classes, or other code definitions |

### List tags and version markers

List all local tags:

```bash
git tag
```

Equivalent form:

```bash
git tag --list
```

Filter tags by pattern:

```bash
git tag --list "v1.*"
```

List tags in descending version-aware order:

```bash
git tag --sort=-v:refname
```

List tags in ascending version-aware order:

```bash
git tag --sort=v:refname
```

Show tag refs with their hashes:

```bash
git show-ref --tags
```

### Show tags in commit history

Show commit history with branches and tags displayed:

```bash
git log --oneline --decorate --graph --all
```

Show a simplified view focused on tagged or decorated commits:

```bash
git log --tags --simplify-by-decoration --oneline
```

This can be useful when you want a quick release/version timeline instead of every ordinary commit.

### Inspect one tag

Inspect a tag:

```bash
git show v1.0.0
```

For an annotated tag, this can show the tagger, date, tag message, target commit, and related commit details.

Show the nearest reachable tag from the current commit:

```bash
git describe --tags
```

This is useful when you want to know which tagged version the current commit is closest to.

### Git tags vs. GitHub Releases

Git tags and GitHub Releases are related, but not identical.

| Thing | Meaning |
|---|---|
| Git tag | A Git ref pointing to a specific commit |
| Annotated tag | A Git tag object with metadata and a message |
| GitHub Release | A GitHub page/object based on a tag, often with release notes and assets |

Use Git commands to inspect Git tags.

Use GitHub.com or GitHub CLI to inspect GitHub Releases.

Examples with GitHub CLI:

```bash
gh release list
gh release view v1.0.0
```

### View commit messages

Compact commit history:

```bash
git log --oneline
```

Full current-branch history:

```bash
git log
```

All branch and ref history:

```bash
git log --all --oneline
```

Readable graph:

```bash
git log --all --oneline --decorate --graph
```

### Print commit messages only

Print raw commit messages only:

```bash
git log --format=%B
```

Print commit subjects only:

```bash
git log --format=%s
```

Print short hash and subject:

```bash
git log --format="%h %s"
```

Print short hash, short date, and subject:

```bash
git log --date=short --format="%h %ad %s"
```

### Search or filter commit messages

Search commit messages on the current branch:

```bash
git log --grep="keyword"
```

Search commit messages across all refs:

```bash
git log --all --grep="keyword"
```

Search case-insensitively:

```bash
git log --all --regexp-ignore-case --grep="keyword"
```

Filter by author:

```bash
git log --author="Name"
```

Limit the number of commits shown:

```bash
git log -n 5 --oneline
```

### Exit the Git pager

Many `git log` and `git show` commands open in Git's pager.

Press:

```text
q
```

to quit the pager and return to the terminal prompt.

This is important because beginners sometimes think the terminal is stuck.

### Later update push choice reminder

After the first push with upstream tracking:

```bash
git push -u origin main
```

plain `git push` usually works for later updates because local `main` tracks `origin/main`.

For ordinary later updates, this is often enough:

```bash
git push
```

For careful versioned updates, release tagging, historical imports, or documentation examples where clarity matters, use the explicit form:

```bash
git push origin main
```

The two forms should not normally be run one after the other every time. They are shown together to explain the choice.

A later update can be documented like this:

```bash
git status
git add -A
git status
git commit -m "docs: describe what changed"

# Option A: normal later push after upstream is configured
git push

# Option B: explicit push to the main branch on origin
git push origin main
```

For a later versioned update, the explicit branch push is often clearest:

```bash
git status
git add -A
git status
git commit -m "docs: describe what changed"

git push origin main

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

That keeps GitHub's normal/default branch view current and also publishes the exact version tag.



---

## 34. Linking Related Repositories and Multi-Repo Release Workflows

Sometimes a larger project is split into several separate GitHub repositories.

Example:

```text
simple-website-examples
simple-website-example-01-first-web-page
simple-website-example-02-basic-site-files
simple-website-example-03-html-css-js-assets
...
simple-website-example-18-media-and-embeds
```

In that structure, the first repository can act as a **hub** or documentation repository, while each example repository remains independent.

GitHub repositories are not normally nested inside each other like folders. Instead, you make them feel connected through documentation, metadata, naming, topics, tags, and releases.

### Recommended relationship model

For beginner-friendly educational examples, use a documentation-level relationship:

```text
Hub README links to each example repo.
Each example README links back to the hub repo.
Each example README links to the previous and next examples.
All repos use consistent descriptions, topics, README structure, changelog structure, tag style, and release conventions.
```

This keeps the repositories simple and independent while still making them feel like one coherent learning series.

### Recommended ranking for linking related repositories

| Rank | Method | Recommendation | Best use |
|---:|---|---|---|
| 1 | README links | Strongly recommended | Primary navigation between hub and examples |
| 2 | GitHub topics | Strongly recommended | Discovery, grouping, and searchability |
| 3 | GitHub About / website link | Recommended | Quick context from each repository landing page |
| 4 | GitHub Releases and tags | Recommended | Versioned snapshots and downloadable releases |
| 5 | Git submodules | Usually not recommended | Only when one repo must embed another repo as a dependency |
| 6 | Git subtree | Usually not recommended | Only when content must be copied into a parent repo while preserving some history |

For a simple educational series, use methods 1 through 4. Avoid submodules and subtree unless there is a specific technical reason.

### README links are the primary connection

The hub README should link to every example repository.

Example hub table:

```markdown
# Simple Website Examples

A progressive series of plain HTML, CSS, and JavaScript examples.

## Examples

| # | Example | Repo | Main Concept |
|---:|---|---|---|
| 01 | First Web Page | [simple-website-example-01-first-web-page](https://github.com/YOUR-USERNAME/simple-website-example-01-first-web-page) | Minimum HTML page |
| 02 | Basic Site Files | [simple-website-example-02-basic-site-files](https://github.com/YOUR-USERNAME/simple-website-example-02-basic-site-files) | index.html, robots.txt, sitemap.xml |
| 18 | Media and Embeds | [simple-website-example-18-media-and-embeds](https://github.com/YOUR-USERNAME/simple-website-example-18-media-and-embeds) | Audio, video, and embedded content |
```

Each example README should link back to the hub and, when useful, to the previous and next examples:

```markdown
Part of the [Simple Website Examples](https://github.com/YOUR-USERNAME/simple-website-examples) series.

Previous: [Example 02 — Basic Site Files](https://github.com/YOUR-USERNAME/simple-website-example-02-basic-site-files)  
Next: [Example 04 — Multi-Page Site](https://github.com/YOUR-USERNAME/simple-website-example-04-multi-page-site)
```

### Cross-repo links vs. same-repo links

Use this rule:

```text
Relative links are best for files inside the same repository.
Absolute GitHub URLs are best for links between separate repositories.
```

Good same-repo relative links:

```markdown
[Changelog](CHANGELOG.md)
[Learning path](docs/learning-path.md)
[Main stylesheet](assets/css/styles.css)
```

Good cross-repository GitHub links:

```markdown
[Series hub](https://github.com/YOUR-USERNAME/simple-website-examples)
[Example 02 — Basic Site Files](https://github.com/YOUR-USERNAME/simple-website-example-02-basic-site-files)
[Example 18 — Media and Embeds](https://github.com/YOUR-USERNAME/simple-website-example-18-media-and-embeds)
```

For the `jefsko` GitHub account, the same pattern would be:

```markdown
[Series hub](https://github.com/jefsko/simple-website-examples)
[Example 02 — Basic Site Files](https://github.com/jefsko/simple-website-example-02-basic-site-files)
[Example 18 — Media and Embeds](https://github.com/jefsko/simple-website-example-18-media-and-embeds)
```

Avoid final GitHub README links like this when each folder will become a separate repository:

```markdown
[Example 02](../simple-website-example-02-basic-site-files/)
```

That sibling-folder link might work in a local ZIP workspace, but it is not the right final form for separate GitHub repositories.

### Link-type recommendation table

| Link type | Best use | Example | Recommended for final separate GitHub repos? |
|---|---|---|---|
| Same-repo relative link | Link to a file inside the current repo | `[Changelog](CHANGELOG.md)` | Yes |
| Same-repo docs relative link | Link to documentation inside the current repo | `[Glossary](docs/glossary.md)` | Yes |
| Same-repo source relative link | Link to a source file inside the current repo | `[CSS](assets/css/styles.css)` | Yes |
| Sibling-folder relative link | Temporary local ZIP/workspace navigation | `[Example 02](../simple-website-example-02-basic-site-files/)` | No, not for final separate repos |
| Absolute GitHub cross-repo link | Link from one separate GitHub repo to another | `[Example 02](https://github.com/YOUR-USERNAME/simple-website-example-02-basic-site-files)` | Yes |
| Submodule/subtree relationship | Technical repo embedding or history sharing | `git submodule add ...` | Usually no for beginner educational examples |

### GitHub topics

Use shared GitHub topics to group related repositories.

Example topics:

```text
html
css
javascript
static-site
web-development
beginner-friendly
learning-examples
simple-website-examples
```

For a series, use one shared topic on every repo, such as:

```text
simple-website-examples
```

Then add repo-specific topics as appropriate.

### GitHub About / website links

Use GitHub's About sidebar to reinforce the relationship.

Recommended pattern:

| Repository type | About / website link |
|---|---|
| Hub repo | Link to the hub documentation, project homepage, or published learning path |
| Example repo | Link back to the hub repo, the live demo, or the example's GitHub Pages site |

Keep descriptions consistent.

Example hub description:

```text
A progressive series of plain HTML, CSS, and JavaScript examples for learning static websites.
```

Example repo description:

```text
Example 01 in the Simple Website Examples series: the smallest useful HTML page.
```

### Tags and releases as relationship markers

Tags and releases should remain repository-specific.

A tag like this:

```text
v1.0.0
```

inside `simple-website-example-01-first-web-page` applies to that example repo only.

A tag with the same name in the hub repo is a separate tag in a separate repository.

Use consistent tag names and release-note style across the series, but do not assume one repo's tag automatically versions another repo.

### Recommended initial check-in workflow for a new example repo

Use the Git CLI when you want the most explicit and repeatable workflow.

```bash
git status
git init -b main
git status
git add -A
git status
git commit -m "docs: add initial example files" -m "Add the initial README, changelog, source files, and supporting documentation for this example repository."
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git remote -v
git push -u origin main
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

Use this pattern when creating a new hub repository or a new standalone example repository.

### Recommended documentation-only update workflow

```bash
git status
git add -A
git status
git commit -m "docs: update repository links" -m "Update README navigation, cross-repository links, and related documentation."
git push origin main
```

If the update should become a new version:

```bash
git tag -a v1.1.0 -m "Version 1.1.0"
git push origin v1.1.0
```

### Recommended source-code update workflow

```bash
git status
git add -A
git status
git commit -m "feat: add media embed example" -m "Add audio, video, and iframe embed examples with supporting README and changelog updates."
git push origin main
git tag -a v1.1.0 -m "Version 1.1.0"
git push origin v1.1.0
```

### Recommended verification commands

Before tagging:

```bash
git status
git log --oneline --decorate -5
git diff --cached --stat
```

After tagging:

```bash
git tag --list
git show v1.0.0
git log --oneline --decorate --graph --all -10
```

After pushing:

```bash
git status
git branch -vv
git log --oneline origin/main..main
git log --oneline main..origin/main
```

The two `git log` comparison commands should normally return no output when local `main` and `origin/main` are aligned.

### Git CLI vs. VS Code vs. Visual Studio

| Method | Recommendation | Best use |
|---|---|---|
| Git CLI | Best for exact, repeatable guide workflows | Tagging, releases, verification, documentation examples |
| Visual Studio Code | Good for reviewing diffs and writing commits | Documentation repos, websites, small projects |
| Visual Studio | Good when the repo is part of a Visual Studio solution | .NET or application projects |

A hybrid workflow is often best:

```text
Use VS Code or Visual Studio to review changes.
Use Git CLI for exact commit, push, tag, and release commands.
```

### VS Code workflow summary

1. Open the repository folder.
2. Review changed files in Source Control.
3. Stage the intended changes.
4. Enter a clear commit message.
5. Commit.
6. Push or Sync.
7. Use the terminal for tags and releases.

Recommended hybrid commands:

```bash
git status
git push origin main
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

### Visual Studio workflow summary

Visual Studio is useful when the repository is part of a solution.

1. Open the solution or folder.
2. Use Git Changes to review edits.
3. Stage changes.
4. Commit.
5. Push.
6. Use Git CLI for exact tagging and release commands when needed.

Recommended hybrid commands:

```bash
git status
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

### Required vs. optional concepts

| Concept | Required? | Notes |
|---|---:|---|
| Commit message | Yes | Every commit needs a message |
| Commit body | No | Useful when the reason or scope needs explanation |
| Tag | No | Required only when you want a named version snapshot |
| Version | No | Strongly recommended for examples, releases, and guides |
| GitHub Release | No | Useful for a polished release page and downloadable assets |
| README links | No, but strongly recommended | Best way to connect related repos |
| GitHub topics | No, but recommended | Helps group and discover related repos |



---

## 35. Renaming Repositories, Local Folders, Project Names, and Remotes

Renaming is common as a project matures.

A draft project might start with an early folder name, then later move to a cleaner final repository name before publication. That is normal, but it is important to know **which thing is being renamed**.

A local folder name, a tracked folder inside a Git repository, and a GitHub repository name are related but different things.

| Item | Tracked by Git? | Renamed where? | Example |
|---|---:|---|---|
| Local parent folder containing a repo | Usually no | File Explorer / command line | `old-local-folder-name/` to `new-local-folder-name/` |
| File or folder inside a repo | Yes | `git mv` or filesystem move plus `git add -A` | `docs/old-name.md` to `docs/new-name.md` |
| GitHub repository name | No, not as file content | GitHub repository settings | `old-repo-name` to `new-repo-name` |
| Git remote URL | Stored in local Git config | `git remote set-url` | Update `origin` after a repo rename |
| Project/application name | Maybe | Project files, README, metadata, source code | Depends where the name appears |

The key idea:

```text
Not every rename needs a Git commit.
Only tracked file/folder changes inside the repo become Git history.
```

### Local parent folder rename

If you have a standalone repo in a local folder, the folder that contains `.git/` is usually not part of the repo history.

Example before:

```text
old-local-folder-name/
  .git/
  README.md
  index.html
```

Example after:

```text
new-local-folder-name/
  .git/
  README.md
  index.html
```

That local folder rename does not require a Git commit because Git is tracking the contents inside the repository, not the name of the parent folder on your computer.

After renaming the local folder, open the new folder path in your terminal or editor.

PowerShell example:

```powershell
Rename-Item "old-local-folder-name" "new-local-folder-name"
cd "new-local-folder-name"
git status
```

### Tracked file or folder rename inside a repo

If the file or folder is inside an existing Git repository, renaming it is a tracked change.

Example before:

```text
main-repo/
  examples/
    old-example-name/
      index.html
```

Example after:

```text
main-repo/
  examples/
    new-example-name/
      index.html
```

Recommended command:

```bash
git mv examples/old-example-name examples/new-example-name
git status
git commit -m "chore: rename example folder" -m "Rename the example folder to match the final project naming convention."
```

Alternative using a normal filesystem move:

```bash
mv examples/old-example-name examples/new-example-name
git add -A
git status
git commit -m "chore: rename example folder" -m "Rename the example folder to match the final project naming convention."
```

PowerShell example:

```powershell
Rename-Item "examples/old-example-name" "new-example-name"
git add -A
git status
git commit -m "chore: rename example folder" -m "Rename the example folder to match the final project naming convention."
```

`git mv` is convenient because it moves the file/folder and stages the change at the same time. Git still detects renames based on content similarity when comparing history.

### GitHub repository rename

A GitHub repository rename changes the remote repository name.

Example:

```text
https://github.com/USERNAME/old-repo-name
```

to:

```text
https://github.com/USERNAME/new-repo-name
```

This is done in GitHub, usually through:

```text
Repository > Settings > General > Repository name
```

Do not use `git mv` to rename a GitHub repository. `git mv` is only for tracked files and folders inside a repository.

### Should you rename a GitHub repo later?

Yes, you can rename a GitHub repository later. It can be a good choice when the old name is unclear, inconsistent, misspelled, too long, or no longer matches the project.

However, it is usually better to choose the final repo name before the repo is public or widely used.

Pros:

| Pro | Why it matters |
|---|---|
| Improves clarity | A cleaner repo name helps users understand the project faster |
| Preserves history | Commits, tags, branches, releases, issues, and stars generally remain with the repo |
| Fixes early naming mistakes | Useful when a project evolves from draft names to final names |
| Improves consistency | Important for multi-repo series or related repos |

Risks:

| Risk | Why it matters |
|---|---|
| Existing users may be confused | People may still recognize or bookmark the old name |
| Links may need updates | READMEs, docs, badges, scripts, package files, and deployment settings may reference the old URL |
| Local clones may need remote updates | Developers should update `origin` to the new URL |
| GitHub Pages project-site URLs are special | Project-site URLs may not redirect the same way regular repo URLs do |
| Old-name redirects may become confusing | If a new repo is later created with the old name, redirect behavior can be affected |

### Update the local remote after a GitHub repo rename

After renaming a GitHub repository, check your local remote:

```bash
git remote -v
```

Update it:

```bash
git remote set-url origin https://github.com/USERNAME/new-repo-name.git
```

Verify it:

```bash
git remote -v
```

Test with a safe read operation:

```bash
git fetch origin
```

If the remote is correct and reachable, `git fetch origin` should succeed.

### Search for old names after a rename

After a repo, folder, or project rename, search for old references.

PowerShell examples:

```powershell
Select-String -Path *.md -Pattern "old-repo-name"
Get-ChildItem -Recurse -File | Select-String -Pattern "old-repo-name"
```

Git examples:

```bash
git grep "old-repo-name"
git grep "old-folder-name"
```

Search likely places:

```text
README.md
CHANGELOG.md
docs/
.github/
package files
project files
deployment configuration
badges
GitHub Pages references
scripts
```

### Rename decision table

| Scenario | Usually needs a Git commit? | Usually needs remote update? | Typical action |
|---|---:|---:|---|
| Rename local parent folder containing `.git/` | No | No | Rename in File Explorer or PowerShell |
| Rename tracked file inside repo | Yes | No | `git mv`, then commit |
| Rename tracked folder inside repo | Yes | No | `git mv`, then commit |
| Rename GitHub repository | No, not by itself | Yes, for local clones | Rename in GitHub settings, then `git remote set-url` |
| Rename project/application in source files | Yes | Maybe | Edit files, search old name, commit |
| Rename live site/domain | Maybe | Maybe | Update docs, DNS/deployment config, links, and commit tracked changes |

### Recommended rename workflow

For a clean, low-risk rename:

```bash
git status
git branch -vv
git remote -v
```

If renaming tracked files or folders:

```bash
git mv old-path new-path
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
git commit -m "chore: rename project paths" -m "Rename tracked paths to match the final project naming convention."
```

If renaming the GitHub repository:

```bash
git remote -v
git remote set-url origin https://github.com/USERNAME/new-repo-name.git
git remote -v
git fetch origin
```

Then search for old references:

```bash
git grep "old-name"
```

Update references as needed:

```bash
git add -A
git status
git commit -m "docs: update renamed repository references" -m "Update documentation, links, and metadata after the repository rename."
git push origin main
```

### Commit-message recommendations for rename work

| Change | Suggested prefix | Example |
|---|---|---|
| Rename tracked files/folders | `chore` | `chore: rename project paths` |
| Update README/docs links after rename | `docs` | `docs: update renamed repository references` |
| Fix a stale old-name reference | `fix` | `fix: correct old repository link` |
| Rename a user-visible app/site/product | `feat` or `chore` | Depends whether it is user-visible or internal |

For documentation-only rename cleanup, `docs:` is usually best.

For path-only cleanup or housekeeping, `chore:` is usually best.

### When to use scenario appendices vs. Troubleshooting

Rename guidance usually belongs in a topic-specific **Scenarios** appendix because it includes planned workflows, decision tables, and examples.

Troubleshooting is best for errors and recovery, such as:

```text
remote URL still points to old repo
GitHub Pages URL no longer works
old-name link is broken
rename appears as delete/add instead of rename
```

For this guide, the best structure is:

```text
Main section: Renaming Repositories, Local Folders, Project Names, and Remotes
Appendix: Repository Renaming and Rename Workflow Scenarios
```



---

## 36. Consolidated Git Workflow Defaults and Verification Checklists

This section consolidates the safest default choices from the guide into one reference.

Most of these topics are explained in more detail elsewhere. This section is a practical “use these defaults unless you have a reason not to” summary.

### Recommended defaults

| Area | Recommended default |
|---|---|
| Primary branch | `main` |
| Primary remote name | `origin` |
| Version tag format | `vMAJOR.MINOR.PATCH`, such as `v1.0.0` |
| First pre-1.0 snapshot | `v0.1.0` |
| First stable release | `v1.0.0` |
| Meaningful version tags | Annotated tags |
| Pre-release tag message | `Pre-release 0.1.0` |
| Stable tag message | `Version 1.0.0` |
| Commit message style | Subject plus optional body |
| Tag pushing | Push one intentional tag at a time |
| Documentation line endings on Windows | Use `.gitattributes` with explicit `text eol=crlf` rules |
| Repository publishing | Verify local branch, remote branch, tag, README, changelog, and release notes |
| VS Code workflow | Open one repository folder at a time; commit intentionally; use the terminal for exact tag/release commands |

### Remote vocabulary quick reminder

| Term | Meaning |
|---|---|
| `origin` | Local nickname for a remote repository URL |
| `main` | Local branch name |
| `origin/main` | Local remote-tracking reference for the `main` branch on `origin` |
| Remote repository | The repository hosted elsewhere, such as on GitHub |
| Local repository | The repository on your machine |
| Working tree | The files you are editing on disk |

Recommended wording:

```text
I pushed my local main branch to the remote named origin on GitHub.
```

Less precise wording:

```text
I pushed to the origin server.
```

`origin` is usually not the server itself. It is the local nickname for a remote URL.

### First push vs. later push

First push for a new branch:

```bash
git push -u origin main
```

Meaning:

```text
Push local main to origin, then remember that local main tracks origin/main.
```

Later push after upstream tracking is configured:

```bash
git push
```

Explicit later push, recommended in careful release documentation:

```bash
git push origin main
```

### Push branch and tag deliberately

For careful versioned updates, push the branch and the tag intentionally:

```bash
git status
git add -A
git status
git commit -m "docs: describe what changed" -m "Explain why this version changed."

git push origin main

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Avoid casual use of:

```bash
git push --tags
```

unless you specifically intend to push all local tags.

### Pre-1.0 snapshots and stable releases

Use `v0.x.0` tags for early drafts, prototypes, or pre-1.0 snapshots:

```bash
git tag -a v0.1.0 -m "Pre-release 0.1.0"
git push origin v0.1.0
```

Use `v1.0.0` for the first stable or intentionally published baseline:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

For documentation projects, the exact meaning of pre-release and stable is a project policy decision. The important thing is to choose a pattern and use it consistently.

### GitHub Release title and notes

A tag and a GitHub Release are related, but different.

Recommended release title:

```text
v1.0.0
```

Recommended release notes structure:

```markdown
## Summary

Short summary of the release.

## Highlights

- Important change 1.
- Important change 2.

## Notes

- Compatibility, publishing, production, or historical-import notes.
```

### Multi-repo synchronized version tags

For a multi-repository project, tags are repository-specific.

A `v1.0.0` tag in one repository is not the same Git object as a `v1.0.0` tag in another repository.

If several repositories are intentionally released together, you can use synchronized tag names across repos:

```text
hub repo:      v1.0.0
example 01:   v1.0.0
example 02:   v1.0.0
example 18:   v1.0.0
```

Use this only when the versions really represent a coordinated set.

If each repo evolves independently, let each repo version independently.

### Line-ending policy reminder

For a Windows-oriented documentation or static-site repo, a `.gitattributes` starter policy can be:

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
*.jpeg binary
*.gif  binary
*.webp binary
*.pdf  binary
```

Inspect line endings:

```powershell
git ls-files --eol
```

If `.gitattributes` changes after files are already tracked, renormalize intentionally:

```bash
git add --renormalize .
git status
git diff --cached --stat
git commit -m "style: normalize line endings" -m "Apply the repository line-ending policy from .gitattributes."
```

### PowerShell repository search recipes

Search tracked files with Git:

```bash
git grep "search text"
```

Search all files from PowerShell:

```powershell
Get-ChildItem -Recurse -File | Select-String -Pattern "search text"
```

Search Markdown files only:

```powershell
Get-ChildItem -Recurse -File -Include *.md | Select-String -Pattern "search text"
```

List matching file paths only:

```powershell
Get-ChildItem -Recurse -File | Select-String -Pattern "search text" | Select-Object -ExpandProperty Path -Unique
```

### Repository publishing readiness checklist

Before publishing a new GitHub repo or release, check:

```text
Repository name is final enough.
README.md explains the project.
CHANGELOG.md includes the current version.
.gitignore is appropriate.
.gitattributes is appropriate.
No secrets are staged.
Remote is correct.
Default branch is main.
Version tag is intentional.
Release notes match the tag.
GitHub Pages settings are correct, if used.
```

Useful commands:

```bash
git status
git remote -v
git branch -vv
git log --oneline --decorate -10
git tag --list
git ls-files --eol
```

### GitHub Pages project-site reminder

For GitHub Pages project sites, repository names can affect project-site URLs.

If you rename a repository, check:

```text
GitHub Pages settings
published site URL
README links
custom domain settings
deployment workflow files
badges
```

A normal repository URL may redirect after a repo rename, but project-site URLs deserve a separate verification pass.

### Final release verification sequence

After committing, pushing, tagging, and pushing the tag:

```bash
git status
git log --oneline --decorate -5
git show --stat --oneline vX.Y.Z
git ls-remote --tags origin vX.Y.Z
```

For branch alignment:

```bash
git log --oneline origin/main..main
git log --oneline main..origin/main
```

Those two branch-alignment commands should normally show no output when local `main` and `origin/main` are aligned.



---

## 37. Staging, Rename Review, Status Checks, and Precise `origin` Wording

This section adds a careful pre-commit review workflow for documentation and website repositories.

It focuses on a small set of practical questions:

```text
Am I staging the right changes?
Did Git notice my rename or move?
Am I at the repo root?
Does .gitattributes exist?
Did I review staged changes before committing?
Am I describing origin precisely?
```

### Prefer `git add -A` for whole-repo release/update workflows

Both `git add .` and `git add -A` stage changes, but their scope can differ.

| Command | Meaning | Best use | Main caution |
|---|---|---|---|
| `git add .` | Stage changes under the current directory | Current-folder work | May miss changes outside the current folder if you are not at the repo root |
| `git add -A` | Stage all changes across the whole repository | Controlled whole-repo updates | Can stage unrelated changes if you have not reviewed status first |

For beginner-friendly documentation or website release workflows, prefer:

```bash
git add -A
```

when you intentionally want to stage the whole current repo state.

Before staging:

```bash
git status --short
```

After staging:

```bash
git status --short
git diff --cached --stat
```

### `git add .` is not wrong

`git add .` is fine when you intentionally want to stage changes under the current folder and below.

It is common in simple examples because users are often at the repo root.

The safer rule is:

```text
Use git add . when you understand the current folder scope.
Use git add -A when you want all intended repo-wide changes staged.
```

If you are unsure where you are, check:

```bash
pwd
git rev-parse --show-toplevel
```

On Windows PowerShell, `pwd` shows your current folder. `git rev-parse --show-toplevel` shows the repository root.

### Working tree, index, and committed history

Git has three important places to compare:

| Place | Meaning |
|---|---|
| Working tree | Files currently on disk |
| Index / staging area | Files staged for the next commit |
| `HEAD` | The latest committed snapshot currently checked out |

Useful commands:

```bash
git diff
```

shows unstaged working-tree changes.

```bash
git diff --cached
```

shows staged changes.

```bash
git status
```

summarizes both.

This matters because a file can be changed on disk but not staged, or staged but changed again afterward.

### Recommended status review sequence

For careful updates:

```bash
git status --short
git diff --stat
git add -A
git status --short
git status --short --renames
git diff --cached --stat
git diff --cached --name-status --find-renames
```

Then commit only after the staged summary matches your intent.

### Review rename detection

A rename may appear as a rename, or it may appear as a delete plus add, depending on similarity and how much the file changed.

Useful commands:

```bash
git status --short --renames
git diff --cached --summary
git diff --cached --name-status --find-renames
```

If you want the cleanest history for a major rename plus rewrite, consider two commits:

```text
Commit 1: rename/move only
Commit 2: edit/rewrite content
```

This makes the rename easier for Git and humans to follow.

### `git mv` behavior and overwrite caution

`git mv` is useful for Git-aware moves and renames.

Example:

```bash
git mv old-name.md new-name.md
```

However, `git mv` will not overwrite an existing destination file by default.

If the destination already exists, stop and decide what you intend:

```text
Do you want to replace the destination file?
Do you want a different filename?
Do you need to compare the two files first?
```

Avoid forcing a move unless you are sure.

### Create folders safely in PowerShell

Use `New-Item` to create folders safely:

```powershell
New-Item -ItemType Directory -Force ".\docs\reference"
```

The `-Force` option makes the command tolerant if the folder already exists.

### Check whether `.gitattributes` exists

From the repo root in PowerShell:

```powershell
Test-Path .\.gitattributes
```

If it returns `True`, the file exists at that path.

If it returns `False`, either the file is missing or you are not in the folder where you expected it.

A helpful check:

```bash
git rev-parse --show-toplevel
```

Then check the repo root for `.gitattributes`.

### Re-apply line-ending rules after `.gitattributes` changes

After adding or changing `.gitattributes`, use:

```bash
git add --renormalize .
git status --short
git diff --cached --stat
```

Then commit the normalization intentionally:

```bash
git commit -m "style: normalize line endings" -m "Apply the repository line-ending policy from .gitattributes."
```

### Precise wording for commits and pushes

Avoid saying:

```text
checked into origin
```

That phrase is understandable, but it mixes concepts.

Better:

```text
committed locally and pushed to origin
```

More precise:

```text
committed locally on main and pushed to the remote named origin
```

Best when teaching:

```text
committed locally to the main branch, then pushed main to the remote named origin on GitHub
```

The reason:

```text
A commit is created locally.
A push sends commits from a local branch to a remote.
origin is the local nickname for a remote URL.
```

### Careful check-in sequence

For a versioned guide or documentation repo:

```bash
git status --short
git diff --stat
git add -A
git status --short --renames
git diff --cached --stat
git diff --cached --name-status --find-renames

git commit -m "docs: update guide" -m "Describe the update."

git push origin main

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

This is a little longer than a minimal workflow, but it is safer when you care about clean versioned history.

### When this belongs in Troubleshooting

Most staging and rename review guidance belongs in the main workflow and command-reference material.

Troubleshooting is useful for symptoms such as:

```text
git add . did not stage the file I expected
rename appears as delete plus add
git mv failed because the destination exists
.gitattributes seems missing
line endings changed unexpectedly
I said checked into origin and want more precise wording
```

For that reason, this version adds a small Troubleshooting entry, but does not create a new broad troubleshooting structure.



---

## 38. GitHub Releases, `.gitignore`, and Release-Ready Version Notes

This section consolidates practical release publishing, tag usage, and `.gitignore` guidance.

The guide already explains commits, tags, releases, versioning, stable filenames, and line endings. This section adds a release-ready checklist view and fills in common beginner gaps.

### Commit, tag, and release memory aid

Use this memory aid:

```text
Commit  = record the work
Tag     = name the version
Release = explain and distribute the version
```

A commit is the saved repository snapshot.

A tag names a specific commit.

A GitHub Release is a GitHub page based on a tag. It usually includes a release title, release notes, automatic source archives, and optional uploaded assets.

### Recommended release workflow

For a documentation or software repo:

```bash
git status --short
git diff --stat
git add -A
git status --short --renames
git diff --cached --stat
git diff --cached --name-status --find-renames

git commit -m "docs: describe the update" -m "Explain what changed and why."

git push origin main

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Then create the GitHub Release from the pushed tag.

### GitHub UI wording can vary

GitHub may show wording such as:

```text
Create a new release
Draft a new release
```

The exact button label can vary based on repository state and GitHub UI changes.

Focus on the workflow:

```text
Choose or create tag
Choose target branch or commit
Write release title
Write release notes
Attach optional assets if useful
Choose prerelease/latest/draft options
Publish release
```

### Release title and description

A release title is the short display name for the release.

Recommended title:

```text
v1.19.0
```

or:

```text
Version 1.19.0
```

For this guide's existing convention, concise titles such as `v1.19.0` are usually best on GitHub, while annotated tag messages can use `Version 1.19.0`.

A release description explains what changed and why it matters.

Starter release-note structure:

```markdown
## Summary

Briefly describe the release.

## Highlights

- Important change 1.
- Important change 2.
- Important change 3.

## Notes

- Compatibility, migration, documentation, or publishing notes.
```

### Manual versus generated release notes

GitHub can generate release notes from commits, pull requests, contributors, and tag comparisons.

Generated notes are useful when:

```text
commit messages and pull request titles are clean
the repository has multiple contributors
you want a quick draft
the previous tag comparison is correct
```

Manual notes are better when:

```text
the audience is beginner-level
commit messages are too technical
the project is documentation-heavy
you want a clearer summary than the raw commit list
```

A good hybrid workflow is:

```text
Generate notes, then edit them manually.
```

### Previous tag selection

The previous tag controls what GitHub compares against when generating release notes.

For a normal next version, compare:

```text
previous tag: v1.18.0
current tag:  v1.19.0
```

If the previous tag is wrong, generated notes can include too much, too little, or unrelated history.

### Release assets versus automatic source archives

GitHub automatically provides source archives for a release tag, usually as ZIP and tarball downloads.

Optional uploaded release assets are separate files you attach yourself.

Use uploaded assets for:

```text
compiled binaries
installers
PDF exports
custom ZIP packages
checksums
signed artifacts
```

For a Markdown documentation repo, you often do not need a custom uploaded asset unless you intentionally created one.

### Drafts, pre-releases, and latest releases

| Option | Meaning | Use when |
|---|---|---|
| Draft release | Saved but not public | You are still editing notes/assets |
| Pre-release | Not final/stable | Alpha, beta, RC, preview, or draft-quality version |
| Latest release | The release GitHub highlights as latest | Usually the newest stable release |

A pre-release can still have a normal-looking tag such as:

```text
v0.3.0
v1.2.0-rc.1
```

Choose the label based on what you want users to understand.

### Editing or deleting releases

Editing a GitHub Release changes the release page, title, notes, assets, or release flags.

It does not automatically change the underlying Git tag.

Deleting a GitHub Release removes the release page.

It does not necessarily delete the underlying tag unless you explicitly delete the tag too.

Treat tags as more permanent than release notes.

### Tag names, tag messages, and release titles

These are related but not identical.

| Item | Example | Where it lives | Purpose |
|---|---|---|---|
| Tag name | `v1.19.0` | Git | Version marker |
| Annotated tag message | `Version 1.19.0` | Git tag object | Tag annotation |
| Release title | `v1.19.0` | GitHub Release | Display title |
| Release notes | Markdown summary | GitHub Release | Explains what changed |

Recommended convention for this guide:

```bash
git tag -a v1.19.0 -m "Version 1.19.0"
```

GitHub Release title:

```text
v1.19.0
```

### Optional annotated tag body

Annotated tags can have more than one `-m` paragraph:

```bash
git tag -a v1.19.0 -m "Version 1.19.0" -m "Add release, tag, and .gitignore guidance."
```

For most beginner documentation workflows, a concise one-line tag message is enough. Put the detailed explanation in the commit body, changelog, and GitHub Release notes.

### Signed tags

Signed tags are annotated tags with a cryptographic signature.

Use signed tags when:

```text
your organization requires release provenance
users need cryptographic verification
you already have signing keys configured and maintained
```

Do not add signed tags merely for appearance. Poorly managed signing can create confusion.

### `.gitignore` spelling and purpose

The standard filename is exactly:

```text
.gitignore
```

Important details:

```text
starts with a period
has no filename before the period
has no extension after gitignore
is lowercase by convention
may appear hidden in some file managers
should not be accidentally saved as .gitignore.txt
```

A `.gitignore` file tells Git which untracked files and folders to ignore.

It is commonly used for:

```text
build output
dependency folders
temporary files
log files
editor or IDE files
operating-system metadata
local environment files
local secrets/configuration
```

### `.gitignore` is optional but strongly recommended

Git does not require `.gitignore`.

However, most software and documentation repositories should have one because generated files and local tool files can otherwise clutter `git status` or be committed accidentally.

A good beginner rule:

```text
If the file is generated, local-only, machine-specific, secret, or easily recreated, it probably belongs in .gitignore.
```

### `.gitignore` does not affect already tracked files

Important:

```text
.gitignore affects untracked files.
It does not stop tracking files that are already tracked.
```

If a file is already tracked and should become ignored, remove it from Git's index while keeping it locally:

```bash
git rm --cached path/to/file
git commit -m "chore: stop tracking generated file"
```

For a tracked folder:

```bash
git rm -r --cached path/to/folder
git commit -m "chore: stop tracking generated folder"
```

### Check ignore behavior

See whether a file is ignored and why:

```bash
git check-ignore -v path/to/file
```

Show ignored files in status:

```bash
git status --ignored
```

Force-add an ignored file only when you intentionally want to override the rule:

```bash
git add -f path/to/file
```

### Starter `.gitignore` patterns

Common examples:

```gitignore
# Build output
bin/
obj/
dist/
build/

# Dependencies
node_modules/

# Logs and temporary files
*.log
*.tmp

# Local environment files
.env
.env.*

# Editor and OS files
.vscode/
.idea/
.DS_Store
Thumbs.db

# User-specific files
*.user
*.suo
```

Adjust these rules for the project. Do not blindly copy ignore rules that might hide files you actually need to commit.

### `.gitignore`, `.gitattributes`, and `.gitkeep`

These files solve different problems.

| File | Purpose |
|---|---|
| `.gitignore` | Ignore untracked generated/local files |
| `.gitattributes` | Control text/binary handling, line endings, diff/merge behavior, and archive/export attributes |
| `.gitkeep` | Placeholder convention for keeping an otherwise empty folder in Git |

`.gitkeep` is not a Git feature. It is just a commonly used placeholder filename.

### Release-ready checklist

Before publishing a GitHub Release:

```text
README is current.
CHANGELOG has the new version.
.gitignore exists if the project needs it.
.gitattributes policy is correct if line endings matter.
No secrets or local-only files are staged.
Commit has been pushed.
Annotated tag has been created and pushed.
GitHub Release uses the intended tag.
Previous tag comparison is correct.
Release title is clear.
Release notes explain the user-facing changes.
Optional assets are intentional.
```

Useful commands:

```bash
git status --short
git diff --cached --stat
git log --oneline --decorate -5
git tag --list
git show vX.Y.Z
git ls-remote --tags origin vX.Y.Z
git check-ignore -v path/to/file
git status --ignored
```


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


### `git add --renormalize`

```bash
git add --renormalize .
```

Stages line-ending normalization according to `.gitattributes`.

Use this intentionally after changing `.gitattributes`, because it can touch many files.

Verify before committing:

```bash
git status
git diff --cached --stat
```


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


### `git log --format`

```bash
git log --format=%B
git log --format=%s
git log --date=short --format="%h %ad %s"
```

Prints commit messages or selected commit fields in a compact custom format.

Official reference: [R26]

### `git describe --tags`

```bash
git describe --tags
```

Shows the nearest reachable tag from the current commit.

Official reference: [R74]

### `git show-ref --tags`

```bash
git show-ref --tags
```

Shows tag refs with their hashes.

Official reference: [R75]

### `gh release list`

```bash
gh release list
```

Lists GitHub Releases for the current repository when GitHub CLI is installed and authenticated.

Official reference: [R78]

### `gh release view`

```bash
gh release view v1.0.0
```

Shows one GitHub Release.

Official reference: [R79]

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




### `git status --ignored`

```bash
git status --ignored
```

Shows ignored files in status output.

Use it when you want to confirm that `.gitignore` rules are matching files.


### `git status --short --renames`

```bash
git status --short --renames
```

Shows compact status output and asks Git to detect renames.

Use it before committing when you moved or renamed files.


### `git submodule`

```bash
git submodule add https://github.com/OWNER/REPO.git path/to/submodule
```

Adds another Git repository as a submodule.

For beginner educational example repos, this is usually not the recommended way to link related repositories. Prefer README links and GitHub topics unless there is a true technical dependency.

### `git subtree`

```bash
git subtree add --prefix=path/to/folder https://github.com/OWNER/REPO.git main --squash
```

Copies another repository into a folder while preserving a relationship to the source.

For beginner educational example repos, this is usually more complexity than needed. Prefer separate repositories connected by README links and GitHub metadata.


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



### PowerShell `New-Item -ItemType Directory -Force`

```powershell
New-Item -ItemType Directory -Force ".\docs\reference"
```

Creates a folder and parent folders as needed.

The `-Force` option makes the command tolerant if the folder already exists.



### PowerShell `Test-Path .\.gitattributes`

```powershell
Test-Path .\.gitattributes
```

Returns `True` if `.gitattributes` exists at the current path and `False` if it does not.

Use `git rev-parse --show-toplevel` first if you are unsure whether you are in the repo root.


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



## E. Staging and rename review problems

### `git add .` did not stage the file I expected

Likely cause:

```text
You ran git add . from a subfolder, so Git staged changes under that folder but missed changes elsewhere.
```

Check:

```bash
pwd
git rev-parse --show-toplevel
git status --short
```

Fix:

```bash
cd "$(git rev-parse --show-toplevel)"
git add -A
git status --short
```

On Windows PowerShell, use:

```powershell
Set-Location (git rev-parse --show-toplevel)
git add -A
git status --short
```

### A rename appears as delete plus add

Check rename detection:

```bash
git status --short --renames
git diff --cached --summary
git diff --cached --name-status --find-renames
```

If the file was heavily rewritten during the rename, Git may not display it as a rename. For cleaner history next time, consider one commit for the rename and another commit for the content rewrite.

### `git mv` failed because the destination exists

`git mv` does not overwrite an existing destination by default.

Stop and compare the files before forcing anything. Decide whether you want to replace the existing file, choose a different name, or merge content manually.

### `.gitattributes` seems missing

From the repo root in PowerShell:

```powershell
Test-Path .\.gitattributes
```

If needed, confirm the repo root:

```bash
git rev-parse --show-toplevel
```

### Line endings changed unexpectedly

Inspect line endings:

```powershell
git ls-files --eol
```

If `.gitattributes` changed and you need to re-apply the policy:

```bash
git add --renormalize .
git status --short
git diff --cached --stat
```

Commit line-ending normalization separately when possible.

### “Checked into origin” sounds imprecise

Use:

```text
committed locally and pushed to origin
```

More precise:

```text
committed locally on main and pushed to the remote named origin
```


## E. Release, tag, and `.gitignore` problems

### GitHub generated release notes show the wrong changes

Likely causes:

```text
The previous tag comparison is wrong.
The current tag points to the wrong commit.
Expected commits were not pushed.
The repository history does not match the release sequence you expected.
```

Check:

```bash
git tag --list
git show vX.Y.Z
git log --oneline previous-tag..current-tag
git ls-remote --tags origin vX.Y.Z
```

Fix the release notes manually if the tag is correct but the generated notes are confusing.

### I created a GitHub Release but cannot find the tag locally

Fetch tags:

```bash
git fetch --tags
git tag --list
```

If GitHub created the tag during release creation, fetching tags brings that tag into your local repository.

### I deleted a GitHub Release but the tag still exists

A GitHub Release page and the underlying Git tag are related but separate.

Deleting a release page does not necessarily delete the Git tag.

Check local tags:

```bash
git tag --list
```

Check remote tags:

```bash
git ls-remote --tags origin
```

### An ignored file is still being tracked

`.gitignore` does not affect files already tracked by Git.

Remove the file from Git's index while keeping it locally:

```bash
git rm --cached path/to/file
git commit -m "chore: stop tracking ignored file"
```

For a folder:

```bash
git rm -r --cached path/to/folder
git commit -m "chore: stop tracking ignored folder"
```

### I do not know why a file is ignored

Use:

```bash
git check-ignore -v path/to/file
```

Git prints the matching ignore file, line number, and pattern when a rule applies.

### My `.gitignore` file is not working on Windows

Check that the file is named exactly:

```text
.gitignore
```

Not:

```text
.gitignore.txt
```

Also make sure it is in the intended repository folder.

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



## F.101 If unchanged tracked files do not appear in `git status`, is that good?

Yes. It means Git sees no changes to those files. They are still tracked and still part of the repository.

## F.102 Do I need to run `git add` on unchanged files?

No. Unchanged tracked files are already part of the current repository snapshot. They do not need to be staged again.

## F.103 Does `git add .` include unchanged files?

No meaningful change is staged for unchanged tracked files. `git add .` stages new files, modified files, and deleted tracked files under the current directory.

## F.104 Does `git add .` check subfolders?

Yes. It stages changes under the current directory, including subfolders, subject to `.gitignore`.

## F.105 If I delete a tracked file locally, will `git add .` stage its deletion?

Yes. Deleting a tracked file is a change. If you run `git add .`, Git can stage that deletion.

## F.106 Should I delete unchanged files locally before running `git add .`?

No. Leave unchanged tracked files in place unless you intentionally want to remove them from the repository.

## F.107 If I tag `v1.1.1`, does the tag apply only to the files I staged?

No. The tag points to a commit. The commit represents the full tracked repository snapshot.

## F.108 If six files changed but the repository has eight tracked files, how many files are in the tag download?

Usually eight, assuming all eight are tracked at that tag and none were deleted.

## F.109 Is GitHub's source ZIP the same as a custom release asset ZIP?

No. GitHub's automatic source ZIP is generated from the tagged repository snapshot. A custom release asset ZIP contains whatever files were manually placed in it.



## F.110 How do I see which files changed between two version tags?

Use:

```bash
git diff --name-status old-tag..new-tag
```

Example:

```bash
git diff --name-status v1.1.0..v1.1.1
```

## F.111 How do I see only added files between two tags?

```bash
git diff --name-status --diff-filter=A v1.1.0..v1.1.1
```

## F.112 How do I see all files contained in a tag?

```bash
git ls-tree -r --name-only v1.1.1
```

## F.113 Can I compare tags on GitHub.com?

Yes. Open the repository's Compare page, then select the earlier tag as the base and the newer tag as the compare target.

## F.114 Why did my GitHub compare URL not work?

Common causes include wrong owner or repository name, a missing pushed tag, typo in the tag name, private repository access, or branch/tag name ambiguity.

## F.115 What is a Pull Request?

A Pull Request is a GitHub workflow for proposing, reviewing, discussing, and merging changes from one branch into another.

## F.116 Is a Pull Request the same as `git pull`?

No. Despite the name, a Pull Request is not mainly the `git pull` command. It is a GitHub review and merge workflow.

## F.117 When should I use a Pull Request?

Use one for reviewed work, collaboration, larger changes, risky changes, branch protection, or whenever you want a clear review record before merging into `main`.

## F.118 When should I tag after using a Pull Request?

After the Pull Request is merged, update local `main`, then tag from `main`.

```bash
git switch main
git pull
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```



## F.119 Should I use `git mv` to rename files?

Usually, yes. It is the clearest command when you intentionally rename or move a tracked file.

## F.120 Is `git mv` required?

No. You can rename the file outside Git and then stage with `git add -A`, but `git mv` makes the intent clearer.

## F.121 Why use `git add -A` after a rename?

Because a rename may include an addition, a deletion, and related file modifications. `git add -A` stages all of those changes across the working tree.

## F.122 How do I check whether Git detected a rename?

Use:

```powershell
git diff --cached --summary
git diff --cached --name-status --find-renames
```

## F.123 Why does Git show a rename as delete plus add?

Git may show delete plus add when the new file is not similar enough to the old file, or when rename detection is not being used.

## F.124 How can I make a rename easier for Git and GitHub to detect?

Rename first, then make large content changes in a separate commit.

## F.125 How do I view file history after a rename?

Use:

```bash
git log --follow -- new-name.md
```

## F.126 What should I do if I deleted the old file and copied in the renamed file manually?

Try staging with `git add -A`, then check rename detection. If Git still does not detect the rename and you care about clean rename display, restore the old file and redo the rename with `git mv`.

## F.127 Do I need a commit body for a rename?

No. A one-line commit is often enough. A body is useful when you want to explain why the rename was needed.



## F.128 How do I reconstruct a Git repository from historical version folders?

Import each folder as one commit in chronological order. Tag only the commits that represent production releases unless you have a specific reason to tag every snapshot.

## F.129 Should offline development snapshots be tagged?

Usually no. Keep them as ordinary commits. Use annotated tags for production releases or important official versions.

## F.130 Should production dates be included in tag names?

Usually no. Keep tag names clean, such as `v1.0.0`, and put production dates in the tag message, release notes, changelog, or deployment notes.

## F.131 How do I tag an older commit?

Find the commit with:

```powershell
git log --oneline
```

Then tag it explicitly:

```powershell
git tag -a vX.Y.Z <commit-sha> -m "Version X.Y.Z"
```

## F.132 How do I fix a local tag message before pushing?

Delete and recreate the local tag:

```powershell
git tag -d vX.Y.Z
git tag -a vX.Y.Z -m "Version X.Y.Z"
```

## F.133 How do I fix a pushed tag message?

Delete the remote tag, delete the local tag, recreate the tag, and push it again. Be careful if other people or releases already depend on the tag.

## F.134 How do I fix an older pushed tag without moving it to the latest commit?

Save the commit first:

```powershell
$commit = git rev-list -n 1 vX.Y.Z
```

Then delete and recreate the tag on that saved commit.

## F.135 What does `git tag -n99` do?

It lists tag names and shows up to 99 lines of each annotated tag message.

## F.136 What is the difference between a commit message, tag message, and release notes?

A commit message describes one commit. A tag message is stored in an annotated tag. Release notes are stored on a GitHub Release page.

## F.137 Is `LF will be replaced by CRLF` an error?

Usually no. It is a line-ending warning. It means Git may write the file with CRLF line endings in the Windows working copy.

## F.138 What is the difference between LF and CRLF?

LF is a single line-feed character. CRLF is carriage return plus line feed. Windows commonly uses CRLF; Linux/macOS commonly use LF.

## F.139 How do I control line endings in a repository?

Add a `.gitattributes` file and define line-ending rules for text files, scripts, and binary files.

## F.140 How do I inspect line endings in Git?

Use:

```powershell
git ls-files --eol
```

## F.141 Why should `.sh` files usually use LF?

Linux/Unix shell scripts can fail if they use CRLF line endings.

## F.142 Should binary image files be line-ending converted?

No. Mark binary formats such as PNG, JPG, GIF, ICO, and WEBP as binary in `.gitattributes`.



## F.143 What repository name should I use for a domain-based site?

Use a clean hyphenated repository name based on the domain, such as `demo-jeffskone-com`, rather than a dotted name like `demo.jeffskone.com`.

## F.144 What is a canonical URL?

A canonical URL is the official preferred URL for a page or site when similar content could be reached through multiple addresses.

## F.145 Should historical commits be rewritten to update an old domain?

Usually no. If the old domain was accurate at the time, preserve it in the historical commit.

## F.146 What should GitHub Release notes include?

A useful release note includes a summary, production publish date, highlights, and notes.

## F.147 What extra documentation files are useful for reconstructed repositories?

`RELEASES.md` and `IMPORT-NOTES.md` can be useful. `RELEASES.md` summarizes production releases. `IMPORT-NOTES.md` explains how historical folders were reconstructed into Git history.



## F.148 How do I search commit messages for a typo?

Use `git log --grep`:

```bash
git log --all --grep="Ve0sion" --oneline
```

## F.149 How do I search commit messages case-insensitively?

Use:

```bash
git log --all --regexp-ignore-case --grep="ve0sion" --oneline
```

## F.150 How do I fix the latest commit message?

Use:

```bash
git commit --amend -m "Corrected commit message"
```

## F.151 How do I fix an older commit message?

Use interactive rebase:

```bash
git rebase -i <bad-commit-sha>~1
```

Then change `pick` to `reword` for the commit whose message you want to fix.

## F.152 Does changing a commit message change the commit hash?

Yes. The commit message is part of the commit object, so changing it creates a new commit hash.

## F.153 What changes if the commit was already pushed?

You have rewritten published history. A normal push may fail, and a force push may be required if rewriting the remote branch is safe.

## F.154 Should I use `git push --force` or `git push --force-with-lease`?

Prefer `git push --force-with-lease`. It is still a force push, but it checks that the remote ref has not changed unexpectedly.

## F.155 When should I not rewrite a commit message?

Avoid rewriting shared, protected, tagged, released, deployed, or widely used history just to fix a minor typo.

## F.156 What if a tag points to the commit I want to rewrite?

The tag will continue to point to the old commit unless you correct the tag separately. Be especially careful with pushed production tags and GitHub Releases.

## F.157 How do I abort an interactive rebase?

Use:

```bash
git rebase --abort
```

## F.158 How do I continue an interactive rebase?

Use:

```bash
git rebase --continue
```



## F.159 Are `feat`, `fix`, and `docs` Git commands?

No. They are commit-message prefixes. Git treats them as ordinary commit message text.

## F.160 Why use commit-message prefixes?

They make history easier to scan, search, summarize, and review later.

## F.161 When should I use `feat`?

Use `feat` when a user-visible capability, section, endpoint, page, or meaningful content structure is added or expanded.

## F.162 When should I use `fix`?

Use `fix` when correcting something wrong, broken, stale, misleading, misplaced, or malfunctioning.

## F.163 When should I use `docs`?

Use `docs` for documentation-only changes, such as README, guide, changelog, release notes, comments, or explanatory text.

## F.164 When should I use `chore`?

Use `chore` for routine maintenance, release preparation, metadata refreshes, housekeeping, or non-user-facing maintenance.

## F.165 When should I use `style`?

Use `style` for formatting-only changes, including whitespace, indentation, Markdown table formatting, or line-ending-only changes.

## F.166 Should commit prefixes go in tag messages?

Usually no. Commit prefixes belong in commit messages. Tag names should usually be clean versions such as `v1.2.0`, and annotated tag messages can simply say `Version 1.2.0`.

## F.167 What is a commit-message scope?

A scope is an optional area in parentheses, such as `docs(readme): add navigation`.

## F.168 How do I mark a breaking change in a commit message?

Use `!` after the type or scope and explain the breaking change in the body, such as `feat!: replace guide structure` with a `BREAKING CHANGE:` body.



## F.169 How do I search only the file I currently have open on GitHub?

Use your browser's Find command:

```text
Windows/Linux: Ctrl+F
Mac: Cmd+F
```

For an editor-like view, press `.` on GitHub to open the web editor, then use `Ctrl+F` or `Cmd+F`.

## F.170 How do I search a specific file path on GitHub?

Use the `path:` qualifier:

```text
search-term path:folder/file-name.ext
```

Example:

```text
force-with-lease path:git-repository-guide.md
```

## F.171 How do I list all Git tags?

Use:

```bash
git tag
```

or:

```bash
git tag --list
```

## F.172 How do I list tags newest-first by version?

Use:

```bash
git tag --sort=-v:refname
```

## F.173 How do I show only tagged release/version commits?

Use:

```bash
git log --tags --simplify-by-decoration --oneline
```

For more context, use:

```bash
git log --oneline --decorate --graph --all
```

## F.174 How do I inspect one tag?

Use:

```bash
git show v1.0.0
```

## F.175 How do I find the nearest reachable tag from my current commit?

Use:

```bash
git describe --tags
```

## F.176 How do I see all commit messages in a repo?

Use:

```bash
git log --oneline
```

For all refs:

```bash
git log --all --oneline
```

## F.177 How do I print only commit messages?

Use:

```bash
git log --format=%B
```

For subjects only:

```bash
git log --format=%s
```

## F.178 How do I search commit messages?

Use:

```bash
git log --all --grep="keyword"
```

For case-insensitive search:

```bash
git log --all --regexp-ignore-case --grep="keyword"
```

## F.179 How do I exit `git log` when it fills the terminal?

Press:

```text
q
```

## F.180 Should I use `git push` or `git push origin main` for later updates?

After `git push -u origin main`, plain `git push` usually works because `main` tracks `origin/main`.

For careful versioned updates, release tagging, historical imports, or examples where clarity matters, use the explicit form:

```bash
git push origin main
```



## F.181 Can Git repositories be linked?

Yes, but usually through documentation and metadata rather than by nesting repositories inside each other.

For beginner-friendly educational projects, prefer:

```text
README links
GitHub topics
GitHub About / website links
consistent tags and releases
```

Avoid submodules or subtree unless there is a real technical dependency.

## F.182 Should related repos use relative sibling links?

Usually no for final separate GitHub repositories.

Use relative links for files inside the same repository:

```markdown
[Changelog](CHANGELOG.md)
```

Use full GitHub URLs for links to other repositories:

```markdown
[Example 02](https://github.com/YOUR-USERNAME/simple-website-example-02-basic-site-files)
```

## F.183 How should a hub repo link to example repos?

Use a README table.

```markdown
| # | Example | Repo | Main Concept |
|---:|---|---|---|
| 01 | First Web Page | [simple-website-example-01-first-web-page](https://github.com/YOUR-USERNAME/simple-website-example-01-first-web-page) | Minimum HTML page |
```

## F.184 How should an example repo link back to the hub?

Add a short navigation block near the top of the README.

```markdown
Part of the [Simple Website Examples](https://github.com/YOUR-USERNAME/simple-website-examples) series.
```

When useful, add previous and next example links.

## F.185 Should a beginner educational repo use Git submodules?

Usually no.

Submodules are useful when one repo must embed another repo at a specific commit, but they add workflow complexity. For beginner examples, README links and GitHub topics are simpler.

## F.186 Should a beginner educational repo use Git subtree?

Usually no.

Subtree can be useful when content must be copied into a parent repo while preserving some history, but it is more advanced than needed for most simple educational examples.

## F.187 Are tags shared across related repositories?

No.

A tag named `v1.0.0` in one repository is separate from a tag named `v1.0.0` in another repository. Use consistent tag names across a series, but remember each repo has its own Git history.

## F.188 What is the recommended first check-in workflow for a new example repo?

Use:

```bash
git status
git init -b main
git add -A
git status
git commit -m "feat: add first web page example" -m "Add the initial HTML file, README, changelog, and supporting documentation."
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git remote -v
git push -u origin main
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

## F.189 What is the recommended documentation-only update workflow?

Use:

```bash
git status
git add -A
git status
git commit -m "docs: update repository links" -m "Update README navigation and cross-repository links."
git push origin main
```

## F.190 When should I use Git CLI, VS Code, or Visual Studio?

Use Git CLI for exact, repeatable commands.

Use VS Code for reviewing diffs and documentation/source changes.

Use Visual Studio when the repo is part of a Visual Studio solution.

A hybrid workflow is often best: review in an editor, then use Git CLI for exact push/tag/release commands.



## F.191 Does renaming my local repo folder require a Git commit?

Usually no.

If you rename the parent folder that contains `.git/`, Git does not treat that as a tracked file change.

Example:

```text
old-local-folder-name/
  .git/
  README.md
```

renamed to:

```text
new-local-folder-name/
  .git/
  README.md
```

No Git commit is needed for that local parent-folder rename.

## F.192 Does renaming a file or folder inside a repo require a Git commit?

Yes.

If the file or folder is tracked inside the repository, the rename is a tracked change.

Use:

```bash
git mv old-path new-path
git status
git commit -m "chore: rename project paths"
```

or use a normal filesystem rename followed by:

```bash
git add -A
git status
git commit -m "chore: rename project paths"
```

## F.193 How do I rename a GitHub repository?

Rename it on GitHub:

```text
Repository > Settings > General > Repository name
```

Then update local clones:

```bash
git remote -v
git remote set-url origin https://github.com/USERNAME/new-repo-name.git
git remote -v
git fetch origin
```

## F.194 Is `git mv` used to rename a GitHub repository?

No.

`git mv` renames tracked files or folders inside a repository. A GitHub repository rename is done in GitHub repository settings.

## F.195 How do I update `origin` after a GitHub repo rename?

Use:

```bash
git remote set-url origin https://github.com/USERNAME/new-repo-name.git
```

Verify:

```bash
git remote -v
git fetch origin
```

## F.196 How do I search for old names after a rename?

Use `git grep`:

```bash
git grep "old-name"
```

Or in PowerShell:

```powershell
Get-ChildItem -Recurse -File | Select-String -Pattern "old-name"
```

## F.197 Should rename work go in Troubleshooting or Common Scenarios?

Planned rename guidance usually belongs in Common Scenarios.

Troubleshooting should be reserved for errors and recovery, such as stale remote URLs, broken GitHub Pages links, broken badges, or old names that remain after cleanup.



## F.198 What defaults should I use for a beginner-friendly Git repo?

Recommended defaults:

```text
Primary branch: main
Primary remote: origin
Version tags: vMAJOR.MINOR.PATCH
Meaningful tags: annotated tags
Stable tag messages: Version X.Y.Z
Tag pushing: push one intentional tag at a time
```

Use these defaults unless the project has a specific reason to differ.

## F.199 What is the difference between `origin`, `main`, and `origin/main`?

`origin` is the local nickname for a remote repository URL.

`main` is a local branch.

`origin/main` is a local remote-tracking reference for the `main` branch on the remote named `origin`.

## F.200 Should I use `v0.1.0` or `v1.0.0` for the first version?

Use `v0.1.0` for a pre-1.0 draft, prototype, or early snapshot.

Use `v1.0.0` for the first stable or intentionally published baseline.

## F.201 What tag message should I use for pre-release tags?

For pre-1.0 snapshots:

```bash
git tag -a v0.1.0 -m "Pre-release 0.1.0"
```

For stable versions:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

## F.202 Should related repos use synchronized tags?

Only when the repositories are intentionally released together.

A `v1.0.0` tag in one repository is separate from a `v1.0.0` tag in another repository, even when the names match.

## F.203 How do I verify a repo is ready to publish?

Check:

```bash
git status
git remote -v
git branch -vv
git log --oneline --decorate -10
git tag --list
git ls-files --eol
```

Also verify README, changelog, `.gitignore`, `.gitattributes`, secrets, tags, release notes, and GitHub Pages settings if used.

## F.204 How do I renormalize line endings after adding `.gitattributes`?

Use:

```bash
git add --renormalize .
git status
git diff --cached --stat
git commit -m "style: normalize line endings"
```

Do this intentionally because it can touch many files.



## F.205 Should I use `git add .` or `git add -A`?

Use `git add .` when you intentionally want to stage changes under the current folder.

Use `git add -A` when you intentionally want to stage all changes across the whole repository, including additions, modifications, deletions, renames, and changes outside the current subfolder.

For careful documentation or release workflows, `git add -A` is usually the safer default after reviewing `git status`.

## F.206 How do I check what is staged before committing?

Use:

```bash
git status --short
git diff --cached --stat
git diff --cached --name-status --find-renames
```

Use `git diff` without `--cached` to see unstaged working-tree changes.

## F.207 How do I make Git show renames more clearly?

Use:

```bash
git status --short --renames
git diff --cached --summary
git diff --cached --name-status --find-renames
```

If a file was renamed and heavily rewritten at the same time, consider separate commits next time: one for the rename and one for the rewrite.

## F.208 Does `git mv` overwrite an existing file?

Not by default.

If the destination exists, stop and compare the files before forcing anything.

## F.209 How do I safely create a folder in PowerShell?

Use:

```powershell
New-Item -ItemType Directory -Force ".\docs\reference"
```

`-Force` makes the command tolerant if the folder already exists.

## F.210 How do I check whether `.gitattributes` exists?

From the expected repo root:

```powershell
Test-Path .\.gitattributes
```

If you are unsure where the repo root is:

```bash
git rev-parse --show-toplevel
```

## F.211 What should I say instead of “checked into origin”?

Prefer:

```text
committed locally and pushed to origin
```

More precise:

```text
committed locally on main and pushed to the remote named origin
```

A commit is created locally. A push sends commits to a remote. `origin` is the local nickname for a remote URL.



## F.212 What is the difference between a commit, tag, and GitHub Release?

A commit records the work.

A tag names a specific version snapshot.

A GitHub Release explains and distributes that tagged version.

Memory aid:

```text
Commit = record the work
Tag = name the version
Release = explain and distribute the version
```

## F.213 Should I let GitHub create the tag while creating a release?

You can, but this guide generally recommends creating and pushing the annotated tag first.

That makes the Git history explicit before you create the GitHub Release page.

## F.214 What should my GitHub Release title be?

For this guide's convention, use the tag name as the release title:

```text
v1.19.0
```

Use the release notes body to explain what changed.

## F.215 Should I use generated release notes or manual release notes?

Generated notes are useful as a starting point when commit messages and pull request titles are clean.

Manual notes are better for beginner-facing documentation, especially when you want a clear explanation instead of raw commit history.

A good workflow is:

```text
Generate notes, then edit them manually.
```

## F.216 What is the Previous tag setting for?

It tells GitHub what earlier tag to compare against when generating release notes.

For a normal `v1.19.0` release, the previous tag would usually be:

```text
v1.18.0
```

## F.217 Should I upload custom release assets?

Only when they add value.

GitHub automatically provides source archives for the tag. Upload custom assets for compiled binaries, installers, PDFs, custom ZIPs, checksums, or signed artifacts.

## F.218 What is `.gitignore`?

`.gitignore` tells Git which untracked files or folders to ignore.

It is commonly used for build output, dependency folders, logs, temp files, editor files, OS metadata, local environment files, and secrets.

## F.219 Is `.gitignore` required?

No.

Git works without `.gitignore`, but most repositories should have one because it keeps generated and local-only files out of normal staging workflows.

## F.220 Why is an ignored file still tracked?

Because `.gitignore` does not affect files already tracked by Git.

Remove it from the index while keeping it locally:

```bash
git rm --cached path/to/file
```

For a folder:

```bash
git rm -r --cached path/to/folder
```

## F.221 How do I check why a file is ignored?

Use:

```bash
git check-ignore -v path/to/file
```

## F.222 What is the difference between `.gitignore`, `.gitattributes`, and `.gitkeep`?

| File | Purpose |
|---|---|
| `.gitignore` | Ignore untracked generated/local files |
| `.gitattributes` | Control text/binary handling, line endings, diff/merge behavior, and archive/export behavior |
| `.gitkeep` | Placeholder convention for keeping an otherwise empty folder in Git |


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



---

# Appendix K: Practical Staging, Tag, and Download Scenarios

This appendix expands [Section 23](#23-practical-staging-and-tag-snapshot-example) with compact recipes and Q&A-style reminders.

## K.1 Scenario summary

Starting repository at `v1.1.0`:

```text
README.md
CHANGELOG.md
aws-live-streaming-guide-obs-ivs.md
aws-live-streaming-guide-obs-medialive.md
```

Local changes before `v1.1.1`:

```text
modified: README.md
modified: CHANGELOG.md

new:
aws-live-streaming-cheat-sheet-obs-ivs.md
aws-live-streaming-cheat-sheet-obs-medialive.md
aws-live-streaming-quick-start-guide-obs-ivs.md
aws-live-streaming-quick-start-guide-obs-medialive.md

unchanged:
aws-live-streaming-guide-obs-ivs.md
aws-live-streaming-guide-obs-medialive.md
```

## K.2 Safe staging workflow

```bash
git status
git add .
git status
git commit -m "Add quick-start guides and cheat sheets"
git push

git tag -a v1.1.1 -m "Version 1.1.1"
git push origin v1.1.1
```

Use this when `git status` confirms that only intended files are new, modified, or deleted.

## K.3 Explicit staging workflow

```bash
git status
git add README.md CHANGELOG.md aws-live-streaming-cheat-sheet-obs-ivs.md aws-live-streaming-cheat-sheet-obs-medialive.md aws-live-streaming-quick-start-guide-obs-ivs.md aws-live-streaming-quick-start-guide-obs-medialive.md
git status
git commit -m "Add quick-start guides and cheat sheets"
git push

git tag -a v1.1.1 -m "Version 1.1.1"
git push origin v1.1.1
```

Use this when you want exact control over what is staged.

## K.4 Do not delete unchanged tracked files

If unchanged tracked files do not appear in `git status`, that is normal.

They are already tracked and still part of the repository.

Do not delete them locally just to simplify `git add .`.

## K.5 Recover accidentally deleted tracked files

If deletion is not staged:

```bash
git restore aws-live-streaming-guide-obs-ivs.md
git restore aws-live-streaming-guide-obs-medialive.md
git status
```

If deletion is already staged:

```bash
git restore --staged aws-live-streaming-guide-obs-ivs.md
git restore --staged aws-live-streaming-guide-obs-medialive.md

git restore aws-live-streaming-guide-obs-ivs.md
git restore aws-live-streaming-guide-obs-medialive.md

git status
```

## K.6 Intentionally remove tracked files

```bash
git status
git rm aws-live-streaming-guide-obs-ivs.md
git rm aws-live-streaming-guide-obs-medialive.md
git status
git commit -m "Remove full guides"
git push

git tag -a v1.1.1 -m "Version 1.1.1"
git push origin v1.1.1
```

Use this only when the intended new repository snapshot should no longer include those files.

## K.7 Tag download contents

A tag identifies a commit.

A commit represents a full tracked repository snapshot.

Therefore, a tag download is not limited to the files changed in the tagged commit.

If six files changed but eight files are tracked at the tagged commit, the tag source download should contain eight files.

## K.8 GitHub automatic source ZIP

GitHub's automatic source ZIP for a tag is generated from the tagged repository snapshot.

It should contain the tracked files at that tag.

## K.9 Custom release asset ZIP

A manually uploaded release asset ZIP is different.

It contains whatever was manually packaged and uploaded.

It might contain:

- all tracked files;
- only selected files;
- generated PDFs;
- quick-start guides only;
- any other custom package.

## K.10 Quick decision table

| Question | Answer |
|---|---|
| Do unchanged tracked files need to be staged again? | No. |
| Is it good if unchanged tracked files do not appear in `git status`? | Yes. |
| Does `git add .` check subfolders? | Yes, under the current directory. |
| Can `git add .` stage deletions? | Yes, if tracked files were deleted. |
| Should unchanged tracked files be deleted before staging? | No. |
| Does a tag apply only to changed files? | No. It points to the full commit snapshot. |
| Does GitHub's source ZIP contain only changed files? | No. It contains the tagged source snapshot. |
| Does a custom release asset ZIP have to match the source ZIP? | No. It contains whatever was manually uploaded. |



---

# Appendix L: Compare, Diff, and Tag Inspection Scenarios

This appendix expands [Section 24](#24-comparing-version-tags-and-changed-files).

## L.1 Show which files changed between two tags

```bash
git diff --name-status v1.1.0..v1.1.1
```

Use this for version-to-version review.

## L.2 Show only added files

```bash
git diff --name-status --diff-filter=A v1.1.0..v1.1.1
```

## L.3 Show only modified files

```bash
git diff --name-status --diff-filter=M v1.1.0..v1.1.1
```

## L.4 Show added and modified files only

```bash
git diff --name-status --diff-filter=AM v1.1.0..v1.1.1
```

## L.5 Show deleted files only

```bash
git diff --name-status --diff-filter=D v1.1.0..v1.1.1
```

## L.6 Show renamed files

```bash
git diff --name-status --diff-filter=R v1.1.0..v1.1.1
```

## L.7 Show a compact summary

```bash
git diff --stat v1.1.0..v1.1.1
```

## L.8 Show full content differences

```bash
git diff v1.1.0..v1.1.1
```

## L.9 Show commits between tags

```bash
git log --oneline v1.1.0..v1.1.1
```

## L.10 Show all files contained in a tag

```bash
git ls-tree -r --name-only v1.1.1
```

Remember:

```text
git diff old..new      = what changed between snapshots
git ls-tree tag        = what exists inside one snapshot
```

## L.11 Compare tags on GitHub.com

URL pattern:

```text
https://github.com/OWNER/REPO/compare/v1.1.0...v1.1.1
```

Manual path:

1. Open the repository.
2. Add `/compare` to the URL.
3. Choose the old tag as the base.
4. Choose the new tag as the compare target.
5. Review commits and changed files.

## L.12 Force tag comparison with `tags/`

If names are ambiguous:

```text
https://github.com/OWNER/REPO/compare/tags/v1.1.0...tags/v1.1.1
```

## L.13 Compare releases

If the repository uses GitHub Releases:

1. Open the repository.
2. Click **Releases**.
3. Find the base release.
4. Use the **Compare** dropdown.
5. Choose the newer tag.
6. Review the comparison.

## L.14 Troubleshooting compare problems

| Problem | Try this |
|---|---|
| URL does not work | Open the repo first, then add `/compare` manually |
| Tag missing | Push it with `git push origin vX.Y.Z` |
| Wrong tag name | Check whether the tag uses a leading `v` |
| Private repo issue | Sign in with an account that has access |
| Branch/tag ambiguity | Use `tags/vX.Y.Z` |
| Releases compare missing | Use the normal Compare page |



---

# Appendix M: Pull Request Scenarios

This appendix expands [Section 25](#25-pull-requests-from-basic-to-advanced).

## M.1 Solo project, tiny edit

For a tiny solo edit, a direct commit to `main` can be acceptable:

```bash
git status
git add .
git status
git commit -m "Fix typo"
git push
```

Use a Pull Request if you want a review record or a safer checkpoint.

## M.2 Solo project, major guide update

For a larger documentation update, use a branch and Pull Request:

```bash
git switch main
git pull
git switch -c update-v1.7.0-guide
git add .
git commit -m "Expand guide with compare and pull request workflows"
git push -u origin update-v1.7.0-guide
```

Then open a Pull Request from `update-v1.7.0-guide` into `main`.

## M.3 Team project

Use Pull Requests by default.

Benefits:

- review;
- discussion;
- checks;
- branch protection;
- better shared understanding;
- safer `main` branch.

## M.4 Pull Request needs corrections

```bash
git switch update-v1.7.0-guide
# edit files
git status
git add .
git status
git commit -m "Address review feedback"
git push
```

The existing Pull Request updates automatically.

## M.5 Pull Request branch is out of date

Merge-based path:

```bash
git switch update-v1.7.0-guide
git fetch origin
git merge origin/main
git push
```

Rebase path for private branches:

```bash
git switch update-v1.7.0-guide
git fetch origin
git rebase origin/main
git push --force-with-lease
```

Beginner rule:

> Prefer the merge-based path unless you understand rebase and history rewriting.

## M.6 Pull Request was merged and now you need to tag

```bash
git switch main
git pull
git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

Tag the final merged result on `main`.

## M.7 Pull Request was closed without merging

If a Pull Request is closed without merging:

- the branch may still exist;
- the work is not on `main`;
- you can reopen it, create a new Pull Request, or delete the branch;
- do not tag from `main` unless the change was actually merged.

## M.8 Draft Pull Request

Use a draft Pull Request when the work is visible but not ready to merge.

Good uses:

- early feedback;
- CI/check testing;
- showing progress;
- collecting comments before final review.

## M.9 Choosing a merge method

| Goal | Merge method to consider |
|---|---|
| Preserve all branch commits | Create a merge commit |
| Turn many small commits into one clean commit | Squash and merge |
| Keep linear history with individual commits | Rebase and merge |

Repository settings control which options are available.

## M.10 Pull Request checklist

Before merging:

- Confirm the base branch is correct.
- Review the changed files.
- Confirm the README and CHANGELOG are updated if needed.
- Confirm version references are correct.
- Confirm checks pass, if the project uses checks.
- Confirm no secrets or unintended files are included.
- Decide whether to delete the branch after merge.
- Tag from `main` after merge if this is a versioned release.



---

# Appendix N: File Rename and Move Scenarios

This appendix expands [Section 26](#26-renaming-files-in-a-git-repository).

## N.1 Rename a tracked file with `git mv`

```powershell
git mv old-name.md new-name.md
git add -A
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
git commit -m "Rename guide file"
```

## N.2 Rename a file and update Markdown references

```powershell
git mv old-guide-name.md new-guide-name.md
```

Then search the repository for the old filename.

In VS Code:

```text
Ctrl+Shift+F
```

Search for:

```text
old-guide-name.md
```

Replace with:

```text
new-guide-name.md
```

Then stage and verify:

```powershell
git add -A
git diff --cached --summary
git diff --cached --name-status --find-renames
```

## N.3 Manual PowerShell rename

```powershell
Rename-Item old-name.md new-name.md
git add -A
git diff --cached --summary
git diff --cached --name-status --find-renames
```

This can work, but `git mv` is clearer when the file is already tracked.

## N.4 Rename appears as delete plus add

If Git shows:

```text
D       old-name.md
A       new-name.md
```

try:

```powershell
git diff --cached --summary
git diff --cached --name-status --find-renames
```

If rename detection still does not recognize the move, the file may have changed too much.

Options:

1. Accept the delete/add display if the final snapshot is correct.
2. Redo the rename cleanly with `git mv`.
3. Separate the rename and large content rewrite into two commits.

## N.5 Clean redo after accidental delete/copy

```powershell
git reset
Copy-Item new-name.md new-name-temp.md
git restore old-name.md
Remove-Item new-name.md
git mv old-name.md new-name.md
Copy-Item new-name-temp.md new-name.md
Remove-Item new-name-temp.md
git add -A
git diff --cached --summary
git diff --cached --name-status --find-renames
```

Use this only when you care about preserving a clean rename display.

## N.6 Rename first, edit second

For the cleanest history:

```powershell
git mv old-name.md new-name.md
git commit -m "Rename guide file"
```

Then edit content and commit again:

```powershell
git add new-name.md
git commit -m "Update guide content"
```

This makes the rename easy to see.

## N.7 Rename plus reference updates in one commit

For small documentation updates, this is usually fine:

```powershell
git mv old-name.md new-name.md
# update README, CHANGELOG, quick-start, cheat sheet, and links
git add -A
git diff --cached --summary
git diff --cached --name-status --find-renames
git commit -m "docs: update full guide filename references"
```

## N.8 View file history after a rename

```bash
git log --follow -- new-name.md
```

With patch output:

```bash
git log --follow -p -- new-name.md
```

## N.9 Rename workflow decision table

| Situation | Recommended action |
|---|---|
| Simple tracked-file rename | Use `git mv` |
| Rename plus small link updates | Use `git mv`, update links, stage with `git add -A` |
| Rename plus major rewrite | Consider two commits: rename first, rewrite second |
| Already deleted old file and copied new file | Try `git add -A` and check rename detection |
| Git does not detect the rename | Accept delete/add or redo with `git mv` |
| Need to prove what changed | Use `git diff --cached --summary` and `git diff --cached --name-status --find-renames` |



---

# Appendix P: Historical Repository Reconstruction Scenario

This appendix expands [Section 27](#27-reconstructing-a-repository-from-historical-snapshots).

## P.1 Example historical folder sequence

```text
v0.1.0
v0.1.1
v0.1.2
v0.1.3
v0.1.4
v0.1.5
v0.1.6
v0.1.7
v0.1.8
v1.0.0
v1.1.0
v1.1.1
v1.1.2
v1.2.0
v1.3.0
v1.4.0
```

Each folder can become one Git commit.

## P.2 Production versions

```text
v1.0.0   2026-03-17
v1.1.2   2026-03-22
v1.2.0   2026-03-23
v1.3.0   2026-03-24
v1.4.0   2026-03-27
```

These should receive annotated tags if they were production releases.

## P.3 Offline snapshots

```text
v0.1.0 through v0.1.8
v1.1.0
v1.1.1
```

These can remain ordinary commits.

## P.4 Import loop pattern

For each version folder:

```powershell
# Replace the repository working files with the next version folder's files.
git status
git add -A
git status
git commit -m "message for that version"
```

Use `git add -A` because the folder replacement may include additions, edits, deletions, and moved files.

## P.5 Example commit messages

| Version | Recommended commit message |
|---|---|
| `v0.1.0` | `feat: add initial AWS microservices index` |
| `v0.1.1` | `feat: add Dice microservice link` |
| `v0.1.2` | `docs: add author attribution and version history` |
| `v0.1.3` | `feat: add Time microservice link` |
| `v0.1.4` | `docs: clarify Dice service description` |
| `v0.1.5` | `feat: add Lottery microservice link` |
| `v0.1.6` | `feat: add WordOfTheDay and polish index page` |
| `v0.1.7` | `style: normalize HTML formatting` |
| `v0.1.8` | `style: reformat index markup and comments` |
| `v1.0.0` | `chore: prepare initial production site snapshot` |
| `v1.1.0` | `chore: add preview image and reorganize error assets` |
| `v1.1.1` | `feat: add Anagram and update site metadata` |
| `v1.1.2` | `fix: update canonical domain to demo.jeffskone.com` |
| `v1.2.0` | `chore: refine SEO and social preview metadata` |
| `v1.3.0` | `fix: improve accessibility, metadata, and 404 page` |
| `v1.4.0` | `chore: refresh metadata guidance and sitemap date` |

## P.6 Example production tag commands

```powershell
git tag -a v1.0.0 -m "Release v1.0.0: initial production publish. Original production publish: 2026-03-17."
git tag -a v1.1.2 -m "Release v1.1.2: production domain and preview metadata update. Original production publish: 2026-03-22."
git tag -a v1.2.0 -m "Release v1.2.0: SEO and social metadata polish. Original production publish: 2026-03-23."
git tag -a v1.3.0 -m "Release v1.3.0: accessibility and 404 page polish. Original production publish: 2026-03-24."
git tag -a v1.4.0 -m "Release v1.4.0: metadata guidance and sitemap refresh. Original production publish: 2026-03-27."
```

If tagging after the fact, specify the correct commit hash:

```powershell
git tag -a v1.0.0 <commit-sha> -m "Release v1.0.0: initial production publish. Original production publish: 2026-03-17."
```

## P.7 Recommended documentation files for reconstructed websites

At minimum:

```text
README.md
CHANGELOG.md
```

Useful additional files:

```text
RELEASES.md
IMPORT-NOTES.md
```

Purpose:

| File | Purpose |
|---|---|
| `README.md` | Explains what the site is and where it is deployed |
| `CHANGELOG.md` | Summarizes notable changes by version |
| `RELEASES.md` | Lists production publish dates, tags, and release notes |
| `IMPORT-NOTES.md` | Explains how historical folder backups were reconstructed into Git history |




## P.8 Website identity checklist

For a reconstructed website repository, document these decisions:

| Item | Example |
|---|---|
| Repository name | `demo-jeffskone-com` |
| Repository description | `Portfolio site showcasing AWS microservices, websites, and web applications` |
| Canonical URL | `https://demo.jeffskone.com` |
| Optional alias | `https://portfolio.jeffskone.com` |
| Main heading | `Jeff Skone's AWS Portfolio` |
| Browser title | `Jeff Skone's AWS Portfolio \| AWS Demos` |

This helps future readers understand the difference between repository naming, site branding, and the production URL.

## P.9 Pre-import cleanup checklist

Before committing a historical snapshot, check for:

| Item | Example | Recommended action |
|---|---|---|
| Accidental test files | `test.txt` | Remove before committing if confirmed accidental |
| Expected old domains | `demo.trixareforkids.com` | Keep if historically accurate |
| Broken intermediate references | old asset paths | Keep if they reflect actual offline development history |
| Suspicious file extensions | `404trooper.gif` with JPEG content | Preserve if historical; clean only current/latest version if appropriate |

This is about truthful reconstruction, not perfecting every old snapshot.

## P.10 Release notes template

```markdown
## Summary

Short explanation of what this release represents.

## Production Publish Date

YYYY-MM-DD

## Highlights

- Important change 1.
- Important change 2.
- Important change 3.

## Notes

- Historical import notes.
- Domain or deployment notes.
- Known limitations.
```

## P.11 GitHub Release title examples

Recommended:

```text
v1.0.0
v1.1.2
v1.2.0
```

Also acceptable:

```text
Version 1.0.0
Release v1.0.0
```

Keep detailed explanations in the release notes, not the title.

## P.12 Documentation files for reconstructed projects

| File | Purpose |
|---|---|
| `README.md` | Project overview, canonical URL, repository purpose, and navigation |
| `CHANGELOG.md` | Notable changes by version |
| `RELEASES.md` | Production publish dates, production tags, and release summaries |
| `IMPORT-NOTES.md` | Explanation of the historical reconstruction process |

Do not add documentation files retroactively to old snapshots unless they really existed in that snapshot or you intentionally document the import as part of a new current-state commit.

---

# Appendix Q: Tag Correction and Release Repair Scenarios

This appendix expands [Section 28](#28-correcting-tag-mistakes-and-understanding-tag-messages).

## Q.1 Correct local unpushed tag message

```powershell
git tag -d v0.1.1
git tag -a v0.1.1 -m "Version 0.1.1"
git show v0.1.1
git tag -n99 v0.1.1
git push origin v0.1.1
```

## Q.2 Correct pushed tag on current commit

```powershell
git push origin --delete v0.1.1
git tag -d v0.1.1
git tag -a v0.1.1 -m "Version 0.1.1"
git push origin v0.1.1
git ls-remote --tags origin v0.1.1
```

## Q.3 Correct pushed older tag without moving it to `HEAD`

```powershell
$commit = git rev-list -n 1 v0.1.0
$commit

git push origin --delete v0.1.0
git tag -d v0.1.0
git tag -a v0.1.0 $commit -m "Version 0.1.0"
git push origin v0.1.0

git show v0.1.0
git tag -n99 v0.1.0
git ls-remote --tags origin v0.1.0
```

## Q.4 Generic PowerShell pattern

```powershell
$tag = "vX.Y.Z"
$commit = git rev-list -n 1 $tag

git push origin --delete $tag
git tag -d $tag
git tag -a $tag $commit -m "Version X.Y.Z"
git push origin $tag
```

## Q.5 Bash pattern

```bash
tag="vX.Y.Z"
commit=$(git rev-list -n 1 "$tag")

git push origin --delete "$tag"
git tag -d "$tag"
git tag -a "$tag" "$commit" -m "Version X.Y.Z"
git push origin "$tag"
```

## Q.6 Verification commands

```powershell
git show vX.Y.Z
git tag -n99 vX.Y.Z
git ls-remote --tags origin vX.Y.Z
```

## Q.7 If a GitHub Release exists

Before replacing the tag:

1. Check whether a GitHub Release exists for that tag.
2. Delete or update the release if necessary.
3. Replace the tag.
4. Recreate or update the GitHub Release so it points to the corrected tag.



---

# Appendix R: Line-Ending and `.gitattributes` Scenarios

This appendix expands [Section 29](#29-line-endings-lf-crlf-and-gitattributes).

## R.1 Recommended `.gitattributes` starter file

```gitattributes
# Normalize text files in the repository.
* text=auto

# Common website/documentation text files.
*.html text eol=crlf
*.css  text eol=crlf
*.js   text eol=crlf
*.md   text eol=crlf
*.txt  text eol=crlf
*.xml  text eol=crlf
*.svg  text eol=crlf
*.json text eol=crlf

# PowerShell scripts should use Windows line endings.
*.ps1 text eol=crlf

# Unix/Linux shell scripts should use LF.
*.sh text eol=lf

# Images and binary files should never be line-ending converted.
*.png  binary
*.jpg  binary
*.jpeg binary
*.gif  binary
*.ico  binary
*.webp binary
```

## R.2 Add `.gitattributes` before first commit

```powershell
git reset
notepad .gitattributes
git add .gitattributes
git add .
git status
git commit -m "feat: add initial AWS microservices index"
```

## R.3 Inspect line endings

```powershell
git ls-files --eol
```

Example:

```text
i/lf    w/crlf  attr/text eol=crlf  index.html
```

Meaning:

| Part | Meaning |
|---|---|
| `i/lf` | Git index/repository-normalized version uses LF |
| `w/crlf` | Working copy uses CRLF |
| `attr/text eol=crlf` | Attribute rule requests CRLF in working copy |

## R.4 Common warning

```text
LF will be replaced by CRLF the next time Git touches it
```

Interpretation:

```text
Git detected LF line endings in a file that may be written as CRLF in the Windows working copy.
```

This is usually not an error.

## R.5 Most important risks

| Risk | Why it matters |
|---|---|
| Noisy diffs | Entire files may appear changed because line endings changed |
| Harder history comparison | Historical versions become harder to compare cleanly |
| Merge noise | Line-ending changes can make conflicts harder to read |
| Script failures | Unix shell scripts may fail if saved with CRLF |

## R.6 Bottom-line rule

For Windows-managed website/documentation repositories:

```text
Use .gitattributes early.
Use CRLF for common text files if that is your repo preference.
Keep .sh files LF.
Mark images and other binary files binary.
```



---

# Appendix S: Commit Message Correction Scenarios

This appendix expands [Section 30](#30-correcting-commit-message-mistakes).

## S.1 Search all commit messages for a typo

```bash
git log --all --grep="Ve0sion" --oneline
```

Case-insensitive:

```bash
git log --all --regexp-ignore-case --grep="ve0sion" --oneline
```

With dates and authors:

```bash
git log --all --grep="Ve0sion" --date=short --format="%h %ad %an %s"
```

## S.2 Search multiple typo patterns in PowerShell

```powershell
$patterns = @("Ve0sion", "Versoin", "Verison", "Vesion")

foreach ($pattern in $patterns) {
    Write-Host ""
    Write-Host "Searching for: $pattern"
    git log --all --grep="$pattern" --date=short --format="%h %ad %an %s"
}
```

## S.3 Inspect the latest commit message

```bash
git log -1 --oneline
git log -1 --format=%B
git show --no-patch --format=fuller HEAD
```

## S.4 Inspect a specific commit message

```bash
git log -1 --format=%B <commit-sha>
git show --no-patch --format=fuller <commit-sha>
```

## S.5 Fix the latest unpushed commit message

```bash
git log -1 --oneline
git commit --amend -m "Corrected commit message"
git log -1 --oneline
```

With a body:

```bash
git commit --amend -m "docs: update version references" -m "Correct the commit message typo and clarify the documentation update scope."
```

## S.6 Fix an older unpushed commit message

```bash
git log --oneline
git rebase -i <bad-commit-sha>~1
```

In the editor, change:

```text
pick <bad-commit-sha> old misspelled message
```

to:

```text
reword <bad-commit-sha> old misspelled message
```

Save, enter the corrected message, and verify:

```bash
git log --oneline
```

## S.7 Fix the root commit message

```bash
git rebase -i --root
```

Change `pick` to `reword` for the root commit.

Use this carefully because it rewrites the root commit and every descendant commit.

## S.8 Fix the latest pushed commit message on a private branch

```bash
git log -1 --oneline
git commit --amend -m "Corrected commit message"
git log -1 --oneline
git push --force-with-lease
```

Use only when it is safe to rewrite the remote branch.

## S.9 Fix an older pushed commit message on a private branch

```bash
git log --oneline
git rebase -i <bad-commit-sha>~1
git log --oneline
git push --force-with-lease
```

Use only when it is safe to rewrite the remote branch.

## S.10 Abort or continue rebase

Abort:

```bash
git rebase --abort
```

Continue:

```bash
git rebase --continue
```

## S.11 Decision table

| Situation | Recommended action |
|---|---|
| Latest commit, not pushed | `git commit --amend -m "Corrected message"` |
| Older commit, not pushed | `git rebase -i <bad-commit-sha>~1`, then `reword` |
| Latest commit, pushed private branch | Amend, then `git push --force-with-lease` |
| Older commit, pushed private branch | Interactive rebase, then `git push --force-with-lease` |
| Shared/protected/main branch | Usually do not rewrite history for a typo |
| Tagged/released/deployed commit | Avoid rewriting unless you fully plan tag/release/deployment repair |

## S.12 Rewrite safety checklist

Before rewriting a pushed commit message, confirm:

```text
The branch is private or everyone agrees.
No one else pushed new work.
The branch is not protected, or rewriting is allowed.
No production tag depends on the old commit.
No GitHub Release depends on the old commit.
No deployment depends on the old commit.
The benefit is worth the disruption.
```



---

# Appendix T: Commit Message Prefix Scenarios

This appendix expands [Section 31](#31-commit-message-prefixes-and-when-to-use-them).

## T.1 Prefix quick table

| Prefix | Use when | Example |
|---|---|---|
| `feat` | User-visible feature/content/capability added or expanded | `feat: add Anagram web application section` |
| `fix` | Incorrect, broken, stale, misleading, or misplaced item corrected | `fix: correct canonical domain` |
| `docs` | Documentation-only change | `docs: document commit message prefixes` |
| `chore` | Routine maintenance or release preparation | `chore: prepare v2.1.0 release` |
| `refactor` | Internal restructure without intended visible behavior change | `refactor: reorganize error image assets` |
| `style` | Formatting, whitespace, line endings, or style-only change | `style: normalize markdown tables` |
| `test` | Tests or validation changed | `test: add link validation script` |
| `build` | Build/dependency/package configuration changed | `build: update Dockerfile` |
| `ci` | CI/CD or GitHub Actions changed | `ci: add markdown validation workflow` |
| `perf` | Performance improved | `perf: reduce homepage image size` |
| `revert` | Previous change intentionally undone | `revert: restore previous metadata layout` |
| `release` | Optional release-only custom convention | `release: prepare v2.1.0` |

## T.2 Decision flow

```text
New user-visible behavior/content?      -> feat
Correction to wrong/broken/stale item?  -> fix
Documentation only?                     -> docs
Routine maintenance/release prep?       -> chore
Internal restructure only?              -> refactor
Formatting only?                        -> style
Tests changed?                          -> test
Build/dependencies changed?             -> build
CI/deployment automation changed?       -> ci
Performance improved?                   -> perf
Undoing a previous commit?              -> revert
```

## T.3 Examples for guide repositories

| Change | Recommended message |
|---|---|
| Add a new main guide section | `docs: add commit message prefix guidance` |
| Add a new appendix | `docs: add commit prefix scenarios appendix` |
| Correct wrong Git guidance | `fix: correct tag repair workflow` |
| Fix broken internal links | `fix: use stable filenames for internal guide links` |
| Prepare a new documentation version | `chore: prepare v1.12.0 guide update` |
| Reformat Markdown tables only | `style: format guide tables` |

## T.4 Examples for website repositories

| Change | Recommended message |
|---|---|
| Add a new visible site section | `feat: add web applications section` |
| Expand a demo index into a portfolio | `feat: expand demo index into AWS portfolio` |
| Correct a stale canonical URL | `fix: correct canonical domain` |
| Move a service to the right section | `fix: move Anagram to web applications section` |
| Refresh sitemap date only | `chore: refresh sitemap lastmod date` |
| Reduce image size | `perf: reduce homepage preview image size` |

## T.5 Commit body examples

One-line message:

```bash
git commit -m "docs: document commit message prefixes"
```

Subject and body:

```bash
git commit -m "docs: document commit message prefixes" -m "Add prefix definitions, decision guidance, examples, and recommendations for documentation, website, release, and maintenance workflows."
```

PowerShell multiline command:

```powershell
git commit `
  -m "feat: expand demo index into AWS portfolio" `
  -m "Update the site title, subtitle, metadata, README, changelog, release notes, and sitemap for v2.1.0. Move Anagram from Microservices to Web Applications while preserving the existing layout and preview image."
```

## T.6 Tag message examples

Commit prefixes do not belong in tag names.

Recommended tag name:

```text
v2.1.0
```

Recommended tag message:

```text
Version 2.1.0
```

Recommended command:

```bash
git tag -a v2.1.0 -m "Version 2.1.0"
```

Do not use:

```bash
git tag -a feat:v2.1.0 -m "feat: version 2.1.0"
```

## T.7 Scopes

Scopes are optional.

Pattern:

```text
type(scope): summary
```

Examples:

```bash
git commit -m "docs(readme): add repository navigation"
git commit -m "fix(metadata): correct canonical domain"
git commit -m "feat(portfolio): add web applications section"
```

Use scopes only when they make the message clearer.

## T.8 Breaking changes

Use `!` and a `BREAKING CHANGE` body when the change breaks compatibility.

```bash
git commit -m "feat!: replace guide structure" -m "BREAKING CHANGE: The guide section order and anchor names changed."
```

For documentation repositories, this is uncommon but possible when anchors, filenames, or instructions change in incompatible ways.



---

# Appendix U: Push, Tag, Branch, and Repository Hygiene Scenarios

This appendix expands [Section 32](#32-push-tag-branch-and-repository-hygiene-workflows).

## U.1 Check whether plain `git push` has an upstream

```powershell
git status
git branch -vv
```

Look for text such as:

```text
main  abc1234 [origin/main] latest commit subject
```

That means local `main` is tracking `origin/main`.

## U.2 Explicit release push checklist

```powershell
git status
git add -A
git status
git commit -m "docs: update guide" -m "Explain what changed and why."
git push origin main

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```

## U.3 Verify branch and tag state

```powershell
git log --oneline --decorate -10
git log --oneline --decorate --graph --all
git log --oneline origin/main..main
git log --oneline main..origin/main
git tag --list
git show vX.Y.Z
```

## U.4 Push branch and one tag, not every tag

Recommended for careful version work:

```powershell
git push origin main
git push origin vX.Y.Z
```

Use this cautiously:

```powershell
git push --tags
```

because it pushes every local tag that the remote does not have.

## U.5 Direct-to-main vs. working branch

| Workflow | Best for | Watch out for |
|---|---|---|
| Direct on `main` | Solo/personal repos, small docs updates | Less review/isolation |
| Working branch | Larger updates, PRs, team review | More steps |
| Detached `HEAD` | Inspecting old commits/tags | Not ideal for normal commits |

## U.6 Static-site folder starter

```text
README.md
CHANGELOG.md
index.html
style.css
script.js
assets/
docs/
scripts/
.github/
```

Optional:

```text
archive/
```

Use `archive/` only for intentional historical material.

## U.7 `.gitignore` starter

```gitignore
# Windows
Thumbs.db
Desktop.ini

# macOS
.DS_Store

# Logs
*.log

# Temporary files
*.tmp
*.bak
*.swp

# Build output
bin/
obj/
dist/
build/

# Local environment files
.env
.env.*

# Editor folders
.vscode/
.idea/

# Archives generated locally
*.zip
*.7z
```

## U.8 Stop tracking a file that is now ignored

```powershell
git rm --cached file-name
git commit -m "chore: stop tracking generated file"
```

## U.9 `.gitkeep` placeholder

```text
exports/.gitkeep
```

Then:

```powershell
git add exports/.gitkeep
git commit -m "chore: keep exports folder placeholder"
```

## U.10 GitHub topics checklist

Use a small set of accurate topics.

Example:

```text
git
github
documentation
versioning
static-site
```

Avoid irrelevant tags, outdated tags, and huge topic lists.

## U.11 Line-ending verification

```powershell
git ls-files --eol
```

Example:

```text
i/lf    w/crlf  attr/text eol=crlf  README.md
```

Use this after adding or changing `.gitattributes`.



---

# Appendix V: GitHub File Search, Tag Inspection, and Commit History Scenarios

This appendix expands [Section 33](#33-github-file-search-tag-inspection-and-commit-history-lookup).

## V.1 Search only the open file on GitHub

Use browser Find:

```text
Windows/Linux: Ctrl+F
Mac: Cmd+F
```

This is the best first choice when the file is already open.

## V.2 Open GitHub's web editor and search there

While viewing a repository or file on GitHub, press:

```text
.
```

Then search the open file with:

```text
Ctrl+F
```

or:

```text
Cmd+F
```

## V.3 Search a specific path on GitHub

Use the `path:` qualifier:

```text
search-term path:folder/file-name.ext
```

Example:

```text
force-with-lease path:git-repository-guide.md
```

Make sure the search is limited to the intended repository when you do not want global GitHub results.

## V.4 List tags

```bash
git tag
git tag --list
```

## V.5 Filter tags

```bash
git tag --list "v1.*"
git tag --list "v1.13.*"
```

## V.6 Sort tags by version

Newest first:

```bash
git tag --sort=-v:refname
```

Oldest first:

```bash
git tag --sort=v:refname
```

## V.7 Show tags with hashes

```bash
git show-ref --tags
```

## V.8 Show tags in history

```bash
git log --oneline --decorate --graph --all
```

Show a simplified tagged/decorated history:

```bash
git log --tags --simplify-by-decoration --oneline
```

## V.9 Inspect one tag

```bash
git show v1.0.0
```

## V.10 Find the nearest reachable tag

```bash
git describe --tags
```

## V.11 List GitHub Releases with GitHub CLI

```bash
gh release list
```

View one release:

```bash
gh release view v1.0.0
```

## V.12 Show compact commit messages

```bash
git log --oneline
```

## V.13 Show all commit messages across refs

```bash
git log --all --oneline
```

Readable graph:

```bash
git log --all --oneline --decorate --graph
```

## V.14 Print only commit message text

Full raw messages:

```bash
git log --format=%B
```

Subjects only:

```bash
git log --format=%s
```

Short hash plus subject:

```bash
git log --format="%h %s"
```

## V.15 Search commit messages

```bash
git log --grep="keyword"
git log --all --grep="keyword"
git log --all --regexp-ignore-case --grep="keyword"
```

## V.16 Filter commit history by author

```bash
git log --author="Name"
```

## V.17 Limit commit history output

```bash
git log -n 5 --oneline
```

## V.18 Exit the Git pager

Press:

```text
q
```

## V.19 Later push choice examples

Normal later push after upstream is configured:

```bash
git push
```

Explicit later push:

```bash
git push origin main
```

Use one of those forms for the branch push. They are shown together to explain the choice.

For a careful versioned update:

```bash
git status
git add -A
git status
git commit -m "docs: describe what changed"

git push origin main

git tag -a vX.Y.Z -m "Version X.Y.Z"
git push origin vX.Y.Z
```



---

# Appendix W: Multi-Repository Linking and Release Workflow Scenarios

This appendix expands [Section 34](#34-linking-related-repositories-and-multi-repo-release-workflows).

It is a topic-specific **scenarios** appendix rather than a troubleshooting-only appendix. Some entries prevent mistakes, some explain choices, and some provide complete workflow examples.

## W.1 Hub repository README template

```markdown
# Simple Website Examples

A progressive series of plain HTML, CSS, and JavaScript examples.

## Examples

| # | Example | Repository | Main Concept |
|---:|---|---|---|
| 01 | First Web Page | [simple-website-example-01-first-web-page](https://github.com/YOUR-USERNAME/simple-website-example-01-first-web-page) | Minimum HTML page |
| 02 | Basic Site Files | [simple-website-example-02-basic-site-files](https://github.com/YOUR-USERNAME/simple-website-example-02-basic-site-files) | index.html, robots.txt, sitemap.xml |
```

## W.2 Example repository README navigation template

```markdown
Part of the [Simple Website Examples](https://github.com/YOUR-USERNAME/simple-website-examples) series.

Previous: [Example 02 — Basic Site Files](https://github.com/YOUR-USERNAME/simple-website-example-02-basic-site-files)  
Next: [Example 04 — Multi-Page Site](https://github.com/YOUR-USERNAME/simple-website-example-04-multi-page-site)
```

## W.3 Same-repo link examples

```markdown
[Changelog](CHANGELOG.md)
[Learning path](docs/learning-path.md)
[Main stylesheet](assets/css/styles.css)
```

## W.4 Cross-repo link examples

```markdown
[Series hub](https://github.com/YOUR-USERNAME/simple-website-examples)
[Example 02 — Basic Site Files](https://github.com/YOUR-USERNAME/simple-website-example-02-basic-site-files)
```

## W.5 Links for the `jefsko` account

```markdown
[Series hub](https://github.com/jefsko/simple-website-examples)
[Example 02 — Basic Site Files](https://github.com/jefsko/simple-website-example-02-basic-site-files)
[Example 18 — Media and Embeds](https://github.com/jefsko/simple-website-example-18-media-and-embeds)
```

## W.6 Avoid sibling-folder links for final separate repos

Avoid this as the final GitHub README form:

```markdown
[Example 02](../simple-website-example-02-basic-site-files/)
```

That can work in a temporary local workspace, but it is not reliable after each folder becomes its own GitHub repository.

## W.7 Recommended GitHub topics

```text
html
css
javascript
static-site
web-development
beginner-friendly
learning-examples
simple-website-examples
```

## W.8 First check-in of a new hub repo

```bash
git status
git init -b main
git add -A
git status
git commit -m "docs: add Simple Website Examples hub" -m "Add the hub README, changelog, learning-path documentation, and navigation links for the example repository series."
git remote add origin https://github.com/YOUR-USERNAME/simple-website-examples.git
git remote -v
git push -u origin main
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

## W.9 First check-in of a new example repo

```bash
git status
git init -b main
git add -A
git status
git commit -m "feat: add first web page example" -m "Add the initial HTML file, README, changelog, and supporting documentation for Example 01."
git remote add origin https://github.com/YOUR-USERNAME/simple-website-example-01-first-web-page.git
git remote -v
git push -u origin main
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

## W.10 Documentation-only update

```bash
git status
git add -A
git status
git commit -m "docs: update repository links" -m "Update hub/example navigation links and README wording."
git push origin main
```

## W.11 Source-code update

```bash
git status
git add -A
git status
git commit -m "feat: add media embed example" -m "Add audio, video, and iframe examples with README and changelog updates."
git push origin main
git tag -a v1.1.0 -m "Version 1.1.0"
git push origin v1.1.0
```

## W.12 Fixing a commit before pushing

If the latest commit has not been pushed yet:

```bash
git commit --amend -m "docs: correct repository navigation links"
```

Then push normally:

```bash
git push origin main
```

## W.13 Creating a GitHub Release after tagging

After creating and pushing the tag:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

create the GitHub Release:

```bash
gh release create v1.0.0 --title "v1.0.0" --notes "Initial release."
```

## W.14 VS Code hybrid workflow

Use VS Code for review and Git CLI for exact release commands.

```text
1. Open the folder in VS Code.
2. Review changes in Source Control.
3. Stage intended files.
4. Commit with a clear message.
5. Open the integrated terminal.
6. Run the explicit push/tag commands.
```

Commands:

```bash
git status
git push origin main
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

## W.15 Visual Studio hybrid workflow

Use Visual Studio for solution-aware review and Git CLI for exact release commands.

```text
1. Open the solution or folder.
2. Review changes in Git Changes.
3. Stage and commit intended files.
4. Push from Visual Studio or Git CLI.
5. Use Git CLI for tags and releases.
```

Commands:

```bash
git status
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
```

## W.16 Required vs. optional workflow elements

| Item | Required? | Recommended use |
|---|---:|---|
| Commit message | Yes | Required for each commit |
| Commit body | No | Add when context or scope matters |
| Tag | No | Use for versioned snapshots |
| Version number | No | Strongly recommended for guides and examples |
| GitHub Release | No | Use for polished release pages and downloadable assets |
| README cross-links | No | Strongly recommended for related repos |
| GitHub topics | No | Recommended for grouping and discovery |



---

# Appendix Y: Repository Renaming and Rename Workflow Scenarios

This appendix expands [Section 35](#35-renaming-repositories-local-folders-project-names-and-remotes).

It is a topic-specific **Scenarios** appendix because rename work is often planned cleanup, not necessarily troubleshooting.

## Y.1 Rename a local parent folder that contains a repo

Example before:

```text
old-local-folder-name/
  .git/
  README.md
```

Example after:

```text
new-local-folder-name/
  .git/
  README.md
```

PowerShell:

```powershell
Rename-Item "old-local-folder-name" "new-local-folder-name"
cd "new-local-folder-name"
git status
```

This does not require a Git commit if only the parent folder name changed.

## Y.2 Rename a tracked file

```bash
git mv old-name.md new-name.md
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
git commit -m "chore: rename file" -m "Rename the tracked file to match the final naming convention."
```

## Y.3 Rename a tracked folder

```bash
git mv docs/old-folder docs/new-folder
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
git commit -m "chore: rename docs folder" -m "Rename the tracked folder to match the final documentation structure."
```

## Y.4 Rename a tracked folder manually in PowerShell

```powershell
Rename-Item "docs/old-folder" "new-folder"
git add -A
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
git commit -m "chore: rename docs folder" -m "Rename the tracked folder to match the final documentation structure."
```

## Y.5 Rename a GitHub repository

Rename the repo in GitHub:

```text
Repository > Settings > General > Repository name
```

Then update local clones:

```bash
git remote -v
git remote set-url origin https://github.com/USERNAME/new-repo-name.git
git remote -v
git fetch origin
```

## Y.6 Search for old repository-name references

PowerShell:

```powershell
Get-ChildItem -Recurse -File | Select-String -Pattern "old-repo-name"
```

Git:

```bash
git grep "old-repo-name"
```

## Y.7 Update old-name references after a repo rename

```bash
git grep "old-repo-name"
```

Edit the affected files, then commit:

```bash
git add -A
git status
git commit -m "docs: update renamed repository references" -m "Update documentation, links, badges, and metadata after the repository rename."
git push origin main
```

## Y.8 Rename project/application references

Search first:

```bash
git grep "Old Project Name"
```

Update files that intentionally use the project name.

Then commit:

```bash
git add -A
git status
git commit -m "chore: rename project references" -m "Update project naming references to match the final name."
```

If the rename is user-visible, consider whether `feat:` is more appropriate than `chore:`.

## Y.9 Rename a GitHub Pages project repo

Be careful with GitHub Pages project sites.

A repository URL may redirect after a repo rename, but project-site URLs can depend on the repository name.

After renaming, check:

```text
GitHub Pages settings
published site URL
README links
deployment workflow files
custom domain settings, if any
```

## Y.10 Rename workflow checklist

Before:

```bash
git status
git branch -vv
git remote -v
```

During tracked path rename:

```bash
git mv old-path new-path
git status
git diff --cached --summary
git diff --cached --name-status --find-renames
```

After GitHub repo rename:

```bash
git remote set-url origin https://github.com/USERNAME/new-repo-name.git
git fetch origin
```

After reference cleanup:

```bash
git grep "old-name"
git add -A
git status
git commit -m "docs: update renamed repository references"
git push origin main
```

## Y.11 Common rename problems

| Problem | Likely fix |
|---|---|
| Local clone still points to old GitHub URL | `git remote set-url origin https://github.com/USERNAME/new-repo-name.git` |
| Old name still appears in README | Search and update docs, then commit |
| Rename appears as delete/add | Use `git diff --cached --name-status --find-renames`; consider separate rename and rewrite commits |
| GitHub Pages URL changed | Check Pages settings and update docs/deployment references |
| Badges broke after repo rename | Update badge URLs |
| Scripts still use old repo name | Search scripts and config files |

## Y.12 Rename commit-message examples

```bash
git commit -m "chore: rename example folder"
git commit -m "docs: update renamed repository references"
git commit -m "fix: correct old repository link"
git commit -m "chore: rename project references"
```


# Appendix Z: References

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


[R57] GitHub Docs, “Viewing and comparing commits.”  
[R58] GitHub Docs, “Comparing releases.”  
[R59] GitHub Docs, “About pull requests.”  
[R60] GitHub Docs, “Creating a pull request.”  
[R61] GitHub Docs, “Reviewing changes in pull requests.”  
[R62] GitHub Docs, “About pull request merges.”  
[R63] GitHub Docs, “Changing the stage of a pull request.”  


[R64] Git documentation, `git-rev-list`.  
[R65] Git documentation, `git-config`, including `core.autocrlf`.  
[R66] Git documentation, `gitattributes`.  
[R67] Git documentation, `git-ls-files`, including `--eol`.  


[R68] Git documentation, `git-log`, including commit log output and message filtering options such as `--grep`.  
[R69] Git documentation, `git-commit`, including `--amend`.  
[R70] Git documentation, `git-rebase`, including interactive rebase and `reword`.  
[R71] Git documentation, `git-push`, including `--force-with-lease`.  


[R72] Git documentation, `gitignore`.  
[R73] GitHub Docs, repository topics/classification guidance.  


[R74] Git documentation, `git-describe`.  
https://git-scm.com/docs/git-describe

[R75] Git documentation, `git-show-ref`.  
https://git-scm.com/docs/git-show-ref

[R76] GitHub Docs, “Searching code.”  
https://docs.github.com/en/search-github/searching-on-github/searching-code

[R77] GitHub Docs, “Navigating code on GitHub.”  
https://docs.github.com/en/repositories/working-with-files/using-files/navigating-code-on-github

[R78] GitHub CLI Manual, `gh release list`.  
https://cli.github.com/manual/gh_release_list

[R79] GitHub CLI Manual, `gh release view`.  
https://cli.github.com/manual/gh_release_view

# Index


## `git add -A`

See [37. Staging, Rename Review, Status Checks, and Precise `origin` Wording](#37-staging-rename-review-status-checks-and-precise-origin-wording) and [Appendix A](#appendix-a-expanded-git-command-reference).

## `git status --short --renames`

See [37. Staging, Rename Review, Status Checks, and Precise `origin` Wording](#37-staging-rename-review-status-checks-and-precise-origin-wording).

## Staged changes

See [37. Staging, Rename Review, Status Checks, and Precise `origin` Wording](#37-staging-rename-review-status-checks-and-precise-origin-wording).

## Rename detection

See [37. Staging, Rename Review, Status Checks, and Precise `origin` Wording](#37-staging-rename-review-status-checks-and-precise-origin-wording), [Appendix N](#appendix-n-file-rename-and-move-scenarios), and [Appendix E](#appendix-e-troubleshooting).

## `Test-Path .\.gitattributes`

See [37. Staging, Rename Review, Status Checks, and Precise `origin` Wording](#37-staging-rename-review-status-checks-and-precise-origin-wording).

## Precise origin wording

See [37. Staging, Rename Review, Status Checks, and Precise `origin` Wording](#37-staging-rename-review-status-checks-and-precise-origin-wording).


## Renaming repositories

See [35. Renaming Repositories, Local Folders, Project Names, and Remotes](#35-renaming-repositories-local-folders-project-names-and-remotes) and [Appendix Y](#appendix-y-repository-renaming-and-rename-workflow-scenarios).

## Local folder rename

See [35. Renaming Repositories, Local Folders, Project Names, and Remotes](#35-renaming-repositories-local-folders-project-names-and-remotes).

## GitHub repository rename

See [35. Renaming Repositories, Local Folders, Project Names, and Remotes](#35-renaming-repositories-local-folders-project-names-and-remotes) and [Appendix Y](#appendix-y-repository-renaming-and-rename-workflow-scenarios).

## `git remote set-url`

See [35. Renaming Repositories, Local Folders, Project Names, and Remotes](#35-renaming-repositories-local-folders-project-names-and-remotes) and [Appendix A](#appendix-a-expanded-git-command-reference).

## Rename cleanup

See [35. Renaming Repositories, Local Folders, Project Names, and Remotes](#35-renaming-repositories-local-folders-project-names-and-remotes) and [Appendix Y](#appendix-y-repository-renaming-and-rename-workflow-scenarios).

## Old-name references

See [35. Renaming Repositories, Local Folders, Project Names, and Remotes](#35-renaming-repositories-local-folders-project-names-and-remotes) and [Appendix Y](#appendix-y-repository-renaming-and-rename-workflow-scenarios).


## Related repositories

See [34. Linking Related Repositories and Multi-Repo Release Workflows](#34-linking-related-repositories-and-multi-repo-release-workflows) and [Appendix W](#appendix-w-multi-repository-linking-and-release-workflow-scenarios).

## Hub repository

See [34. Linking Related Repositories and Multi-Repo Release Workflows](#34-linking-related-repositories-and-multi-repo-release-workflows) and [Appendix W](#appendix-w-multi-repository-linking-and-release-workflow-scenarios).

## Cross-repository links

See [34. Linking Related Repositories and Multi-Repo Release Workflows](#34-linking-related-repositories-and-multi-repo-release-workflows).

## Sibling-folder links

See [34. Linking Related Repositories and Multi-Repo Release Workflows](#34-linking-related-repositories-and-multi-repo-release-workflows).

## Git submodules

See [34. Linking Related Repositories and Multi-Repo Release Workflows](#34-linking-related-repositories-and-multi-repo-release-workflows).

## Git subtree

See [34. Linking Related Repositories and Multi-Repo Release Workflows](#34-linking-related-repositories-and-multi-repo-release-workflows).

## Visual Studio workflow

See [34. Linking Related Repositories and Multi-Repo Release Workflows](#34-linking-related-repositories-and-multi-repo-release-workflows) and [Appendix W](#appendix-w-multi-repository-linking-and-release-workflow-scenarios).

## Multi-repo release workflows

See [34. Linking Related Repositories and Multi-Repo Release Workflows](#34-linking-related-repositories-and-multi-repo-release-workflows) and [Appendix W](#appendix-w-multi-repository-linking-and-release-workflow-scenarios).


## GitHub file search

See [33. GitHub File Search, Tag Inspection, and Commit History Lookup](#33-github-file-search-tag-inspection-and-commit-history-lookup) and [Appendix V](#appendix-v-github-file-search-tag-inspection-and-commit-history-scenarios).

## `Ctrl+F` / `Cmd+F`

See [33. GitHub File Search, Tag Inspection, and Commit History Lookup](#33-github-file-search-tag-inspection-and-commit-history-lookup).

## GitHub `path:` search

See [33. GitHub File Search, Tag Inspection, and Commit History Lookup](#33-github-file-search-tag-inspection-and-commit-history-lookup).

## `git tag --sort`

See [33. GitHub File Search, Tag Inspection, and Commit History Lookup](#33-github-file-search-tag-inspection-and-commit-history-lookup) and [Appendix V](#appendix-v-github-file-search-tag-inspection-and-commit-history-scenarios).

## `git describe --tags`

See [33. GitHub File Search, Tag Inspection, and Commit History Lookup](#33-github-file-search-tag-inspection-and-commit-history-lookup) and [Appendix V](#appendix-v-github-file-search-tag-inspection-and-commit-history-scenarios).

## `git show-ref --tags`

See [33. GitHub File Search, Tag Inspection, and Commit History Lookup](#33-github-file-search-tag-inspection-and-commit-history-lookup) and [Appendix V](#appendix-v-github-file-search-tag-inspection-and-commit-history-scenarios).

## Commit history lookup

See [33. GitHub File Search, Tag Inspection, and Commit History Lookup](#33-github-file-search-tag-inspection-and-commit-history-lookup) and [Appendix V](#appendix-v-github-file-search-tag-inspection-and-commit-history-scenarios).

## `git log --format=%B`

See [33. GitHub File Search, Tag Inspection, and Commit History Lookup](#33-github-file-search-tag-inspection-and-commit-history-lookup) and [Appendix V](#appendix-v-github-file-search-tag-inspection-and-commit-history-scenarios).

## Git pager

See [33. GitHub File Search, Tag Inspection, and Commit History Lookup](#33-github-file-search-tag-inspection-and-commit-history-lookup).


## `git push` vs `git push origin main`

See [32. Push, Tag, Branch, and Repository Hygiene Workflows](#32-push-tag-branch-and-repository-hygiene-workflows) and [Appendix U](#appendix-u-push-tag-branch-and-repository-hygiene-scenarios).

## Branch push

See [32. Push, Tag, Branch, and Repository Hygiene Workflows](#32-push-tag-branch-and-repository-hygiene-workflows).

## Tag push

See [32. Push, Tag, Branch, and Repository Hygiene Workflows](#32-push-tag-branch-and-repository-hygiene-workflows).

## `.gitignore`

See [32. Push, Tag, Branch, and Repository Hygiene Workflows](#32-push-tag-branch-and-repository-hygiene-workflows) and [Appendix U](#appendix-u-push-tag-branch-and-repository-hygiene-scenarios).

## `.gitkeep`

See [32. Push, Tag, Branch, and Repository Hygiene Workflows](#32-push-tag-branch-and-repository-hygiene-workflows) and [Appendix U](#appendix-u-push-tag-branch-and-repository-hygiene-scenarios).

## GitHub topics

See [32. Push, Tag, Branch, and Repository Hygiene Workflows](#32-push-tag-branch-and-repository-hygiene-workflows).


## Commit message prefixes

See [31. Commit Message Prefixes and When to Use Them](#31-commit-message-prefixes-and-when-to-use-them) and [Appendix T](#appendix-t-commit-message-prefix-scenarios).

## Conventional commit style

See [31. Commit Message Prefixes and When to Use Them](#31-commit-message-prefixes-and-when-to-use-them).

## `feat`

See [31. Commit Message Prefixes and When to Use Them](#31-commit-message-prefixes-and-when-to-use-them).

## `fix`

See [31. Commit Message Prefixes and When to Use Them](#31-commit-message-prefixes-and-when-to-use-them).

## `docs`

See [31. Commit Message Prefixes and When to Use Them](#31-commit-message-prefixes-and-when-to-use-them).

## `chore`

See [31. Commit Message Prefixes and When to Use Them](#31-commit-message-prefixes-and-when-to-use-them).


## Commit-message misspellings

See [30. Correcting Commit Message Mistakes](#30-correcting-commit-message-mistakes) and [Appendix S](#appendix-s-commit-message-correction-scenarios).

## `git commit --amend`

See [30. Correcting Commit Message Mistakes](#30-correcting-commit-message-mistakes) and [Appendix S](#appendix-s-commit-message-correction-scenarios).

## Interactive rebase

See [17. Branching, Merging, and Rebasing](#17-branching-merging-and-rebasing), [30. Correcting Commit Message Mistakes](#30-correcting-commit-message-mistakes), and [Appendix S](#appendix-s-commit-message-correction-scenarios).

## `reword`

See [30. Correcting Commit Message Mistakes](#30-correcting-commit-message-mistakes) and [Appendix S](#appendix-s-commit-message-correction-scenarios).

## `git push --force-with-lease`

See [30. Correcting Commit Message Mistakes](#30-correcting-commit-message-mistakes) and [Appendix S](#appendix-s-commit-message-correction-scenarios).


## Canonical URL

See [27. Reconstructing a Repository from Historical Snapshots](#27-reconstructing-a-repository-from-historical-snapshots).

## GitHub Release notes

See [27. Reconstructing a Repository from Historical Snapshots](#27-reconstructing-a-repository-from-historical-snapshots) and [Appendix P](#appendix-p-historical-repository-reconstruction-scenario).

## `RELEASES.md`

See [27. Reconstructing a Repository from Historical Snapshots](#27-reconstructing-a-repository-from-historical-snapshots) and [Appendix P](#appendix-p-historical-repository-reconstruction-scenario).

## `IMPORT-NOTES.md`

See [27. Reconstructing a Repository from Historical Snapshots](#27-reconstructing-a-repository-from-historical-snapshots) and [Appendix P](#appendix-p-historical-repository-reconstruction-scenario).


## Historical reconstruction

See [27. Reconstructing a Repository from Historical Snapshots](#27-reconstructing-a-repository-from-historical-snapshots) and [Appendix P](#appendix-p-historical-repository-reconstruction-scenario).

## Production tags

See [27. Reconstructing a Repository from Historical Snapshots](#27-reconstructing-a-repository-from-historical-snapshots).

## Tag correction

See [28. Correcting Tag Mistakes and Understanding Tag Messages](#28-correcting-tag-mistakes-and-understanding-tag-messages) and [Appendix Q](#appendix-q-tag-correction-and-release-repair-scenarios).

## `git tag -n99`

See [28. Correcting Tag Mistakes and Understanding Tag Messages](#28-correcting-tag-mistakes-and-understanding-tag-messages).

## Line endings

See [29. Line Endings, LF, CRLF, and `.gitattributes`](#29-line-endings-lf-crlf-and-gitattributes) and [Appendix R](#appendix-r-line-ending-and-gitattributes-scenarios).

## `.gitattributes`

See [29. Line Endings, LF, CRLF, and `.gitattributes`](#29-line-endings-lf-crlf-and-gitattributes) and [Appendix R](#appendix-r-line-ending-and-gitattributes-scenarios).


## File renames

See [26. Renaming Files in a Git Repository](#26-renaming-files-in-a-git-repository) and [Appendix N](#appendix-n-file-rename-and-move-scenarios).

## `git mv`

See [26. Renaming Files in a Git Repository](#26-renaming-files-in-a-git-repository).

## Rename detection

See [26. Renaming Files in a Git Repository](#26-renaming-files-in-a-git-repository) and [Appendix N](#appendix-n-file-rename-and-move-scenarios).

## `git add -A`

See [26. Renaming Files in a Git Repository](#26-renaming-files-in-a-git-repository) and [Appendix N](#appendix-n-file-rename-and-move-scenarios).


## Comparing tags

See [24. Comparing Version Tags and Changed Files](#24-comparing-version-tags-and-changed-files) and [Appendix L](#appendix-l-compare-diff-and-tag-inspection-scenarios).

## Changed files between tags

See [24. Comparing Version Tags and Changed Files](#24-comparing-version-tags-and-changed-files).

## GitHub Compare

See [24. Comparing Version Tags and Changed Files](#24-comparing-version-tags-and-changed-files) and [Appendix L](#appendix-l-compare-diff-and-tag-inspection-scenarios).

## Pull Requests

See [25. Pull Requests from Basic to Advanced](#25-pull-requests-from-basic-to-advanced) and [Appendix M](#appendix-m-pull-request-scenarios).

## Draft Pull Requests

See [25. Pull Requests from Basic to Advanced](#25-pull-requests-from-basic-to-advanced) and [Appendix M](#appendix-m-pull-request-scenarios).


## Practical staging

See [23. Practical Staging and Tag Snapshot Example](#23-practical-staging-and-tag-snapshot-example) and [Appendix K](#appendix-k-practical-staging-tag-and-download-scenarios).

## Unchanged tracked files

See [23. Practical Staging and Tag Snapshot Example](#23-practical-staging-and-tag-snapshot-example) and [Appendix K](#appendix-k-practical-staging-tag-and-download-scenarios).

## Tag snapshot downloads

See [23. Practical Staging and Tag Snapshot Example](#23-practical-staging-and-tag-snapshot-example) and [Appendix K](#appendix-k-practical-staging-tag-and-download-scenarios).

## Source ZIP

See [23. Practical Staging and Tag Snapshot Example](#23-practical-staging-and-tag-snapshot-example) and [Appendix K](#appendix-k-practical-staging-tag-and-download-scenarios).

## Release asset ZIP

See [23. Practical Staging and Tag Snapshot Example](#23-practical-staging-and-tag-snapshot-example) and [Appendix K](#appendix-k-practical-staging-tag-and-download-scenarios).


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
