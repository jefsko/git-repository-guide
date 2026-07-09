# Git Repository Guide

A beginner-friendly guide to creating Git repositories and managing versioned file sets

## About

This repository contains a standalone Markdown guide that explains how to create a Git repository, connect it to GitHub, commit files, mark versioned snapshots with tags, retrieve earlier versions, and understand the difference between Git tags, GitHub Releases, and production deployments.

The guide is written in a conversational style for novice-to-advanced users. It focuses on practical command-line workflows while also covering Visual Studio Code usage.

## Main Guide

Current guide version: `v1.17.0`

Main guide file:

```text
git-repository-guide.md
```

The active guide file should keep this stable filename. Version history should be tracked through Git commits, tags, releases, and this changelog rather than by renaming the file for each version.

## Which file should I open first?

| Goal | Start here |
|---|---|
| I want the fastest practical setup path. | [`git-repository-guide-quick-start-guide.md`](git-repository-guide-quick-start-guide.md) |
| I want a compact repeat checklist. | [`git-repository-guide-cheat-sheet.md`](git-repository-guide-cheat-sheet.md) |
| I want a command-by-command reference. | [`git-command-quick-reference.md`](git-command-quick-reference.md) |
| I need the full explanation and reference material. | [`git-repository-guide.md`](git-repository-guide.md) |

## Filename Reference Rule

Internal repo links and active file references should use stable filenames. Standalone download filename examples and historical changelog entries may still use versioned filenames when that is the point being explained.

Use stable filenames inside the repository:

```text
git-repository-guide.md
git-repository-guide-quick-start-guide.md
git-repository-guide-cheat-sheet.md
git-command-quick-reference.md
README.md
CHANGELOG.md
```

Use versioned filenames for standalone downloads when helpful, such as files shared outside the repository.

## Repository Contents

| File | Purpose |
|---|---|
| [`README.md`](README.md) | Repository overview and navigation. |
| [`CHANGELOG.md`](CHANGELOG.md) | Version history and notable changes. |
| [`git-repository-guide.md`](git-repository-guide.md) | Full guide with complete explanations, examples, appendixes, and references. |
| [`git-repository-guide-quick-start-guide.md`](git-repository-guide-quick-start-guide.md) | Short, sequential companion guide for the most common Git repository/version-tag workflow. |
| [`git-repository-guide-cheat-sheet.md`](git-repository-guide-cheat-sheet.md) | Compact checklist for repeating the common workflow after learning it. |
| [`git-command-quick-reference.md`](git-command-quick-reference.md) | Alphabetical Git command quick reference with syntax, required parameters, optional parameters, and practical notes. |

## Full Guide vs. Quick-Start vs. Cheat Sheet

- Use the **full guide** when you want complete explanations, edge cases, appendixes, and reference material.
- Use the **quick-start guide** when you want the shortest practical path that is still complete enough to follow.
- Use the **cheat sheet** when you already understand the workflow and want a compact repeat checklist.
- Use the **command quick reference** when you want command syntax, required parameters, optional parameters, and short explanations.

## Topics Covered

- Creating a local Git repository
- Creating a GitHub repository
- Using Git from the command line
- Using Git from Visual Studio Code
- Writing useful commit messages
- Understanding commit summaries, commit bodies, and commit descriptions
- Creating commits with one or multiple `-m` flags
- Distinguishing commit bodies from GitHub repository descriptions
- Creating annotated Git tags
- Marking repository snapshots as versions
- Understanding versioned file sets
- Comparing versions
- Retrieving or downloading older versions
- Creating GitHub Releases
- Understanding production deployment terminology
- Using Git's pager
- Naming GitHub repositories
- Writing GitHub repository descriptions
- Keeping stable filenames inside a Git repository
- Creating and maintaining README.md and CHANGELOG.md
- Understanding first-time setup vs. later update workflows
- Adding new files to a repository
- Updating or replacing existing tracked files
- Adding, deleting, moving, renaming, and replacing folders and files
- Understanding empty folders and `.gitkeep` placeholder conventions
- Understanding delete-then-replace behavior
- Verifying staged and unstaged changes before committing
- Understanding why ordinary file updates usually do not require merging
- Understanding `origin`, `main`, `origin/main`, and working branches
- Creating and using working branches
- Choosing between direct-to-`main` pushes and working-branch pushes
- Understanding `fetch`, `pull`, `merge`, and `rebase`
- Merging with and without conflicts
- Understanding push rejection vs. merge conflicts
- Resolving merge conflicts manually and with tools
- Comparing diff, merge, and Git GUI tools
- Understanding rebasing and when to avoid it
- Understanding practical `git add .` behavior
- Understanding unchanged tracked files in `git status`
- Recovering accidentally deleted tracked files
- Understanding what files are included in a tagged repository snapshot
- Understanding GitHub source ZIP downloads versus custom release asset ZIPs
- Understanding Git push object counts

- Using the quick-start companion guide
- Using the compact cheat sheet
- Choosing between the full guide, quick-start guide, and cheat sheet

- Comparing changed files between version tags
- Comparing version tags on GitHub.com
- Navigating GitHub's Compare page
- Understanding GitHub source comparisons versus local `git diff`
- Creating and using Pull Requests
- Reviewing, updating, merging, and tagging after Pull Requests

- Renaming tracked files with `git mv`
- Updating Markdown links after a file rename
- Using `git add -A` for rename-related changes
- Verifying rename detection with staged diff commands
- Recovering from delete-and-copy rename workflows
- Viewing history after a file rename

- Using the Git command quick reference
- Understanding common Git command syntax
- Identifying required and optional Git command parameters

- Reconstructing a Git repository from historical version folders
- Distinguishing production releases from offline development snapshots
- Creating annotated production tags during historical reconstruction
- Correcting local and pushed tag mistakes
- Understanding `git tag -n99` and annotated tag messages
- Managing GitHub Releases after tag corrections
- Understanding LF vs. CRLF line-ending warnings on Windows
- Using `.gitattributes` to control line endings

- Planning repository identity for domain-based websites
- Choosing canonical URLs and optional aliases
- Structuring GitHub Release titles and release notes
- Using `RELEASES.md` and `IMPORT-NOTES.md` for reconstructed repositories
- Preserving accurate historical domain references

- Searching commit messages for typos
- Correcting the latest commit message with `git commit --amend`
- Correcting older commit messages with interactive rebase and `reword`
- Understanding when commit-message fixes rewrite history
- Using `git push --force-with-lease` safely
- Knowing when not to rewrite shared history

- Understanding commit-message prefixes such as `feat`, `fix`, `docs`, and `chore`
- Choosing the best commit-message prefix for documentation, website, release, and maintenance changes
- Distinguishing commit-message prefixes from Git commands and tag messages
- Using optional commit-message scopes
- Understanding breaking-change notation in commit messages

- Understanding when `git push` behaves like `git push origin main`
- Pushing branches and tags explicitly
- Verifying branch/tag push state
- Choosing direct-to-main versus working-branch workflows
- Using `docs/`, `archive/`, `assets/`, `scripts/`, and `.github/` folders appropriately
- Creating and using `.gitignore`
- Preserving empty folders with `.gitkeep` when needed
- Choosing GitHub repository topics
- Applying line-ending policy reminders with `.gitattributes`

- Searching inside the currently open GitHub file
- Opening GitHub's web editor with `.`
- Using GitHub `path:` search qualifiers
- Listing and sorting tags by version
- Inspecting tagged release/version commits
- Distinguishing Git tags from GitHub Releases
- Viewing and searching commit messages with `git log`
- Printing commit messages only with `git log --format=%B`
- Exiting Git's pager with `q`
- Choosing between plain `git push` and explicit `git push origin main` in later-update examples

- Linking related GitHub repositories through README navigation
- Building hub-and-example repository series
- Choosing cross-repository GitHub links instead of sibling-folder relative links
- Using GitHub topics and About links to connect related repos
- Understanding when not to use Git submodules or Git subtree
- Keeping tags and releases repository-specific across a multi-repo series
- Using Git CLI, VS Code, and Visual Studio for check-in workflows
- Following common multi-repo check-in, tag, and release scenarios

- Renaming local parent folders versus tracked repo folders
- Renaming tracked files and folders with `git mv` or `git add -A`
- Renaming GitHub repositories through repository settings
- Updating local remotes after a GitHub repo rename
- Searching for old names after a rename
- Handling project/application name cleanup
- Understanding when rename work belongs in scenario appendices versus Troubleshooting

- Consolidated recommended Git workflow defaults
- Clarifying `origin`, `main`, and `origin/main`
- Choosing pre-1.0 tags versus stable `v1.0.0` tags
- Using pre-release and stable annotated tag messages
- Coordinating synchronized tags across related repositories
- Renormalizing line endings after `.gitattributes` changes
- Searching repositories with Git and PowerShell
- Checking repository publishing readiness
- Verifying GitHub Pages settings after rename or publication changes
- Running final branch, tag, release, and line-ending verification commands

## Recommended Repository Details

Recommended repository name:

```text
git-repository-guide
```

Recommended GitHub description:

```text
A beginner-friendly guide to creating Git repositories and managing versioned file sets
```

## Version History

| Version | Description |
|---|---|
| `v0.1.0` | Original pre-release draft |
| `v1.0.0` | First complete locked baseline |
| `v1.1.0` | Additive expansion with expanded Git reference and Knowledge Base |
| `v1.2.0` | Additive expansion covering repository packaging, push workflows, branch workflows, and Git object-count guidance |
| `v1.3.0` | Additive expansion covering file update workflows, fetch/pull/merge/rebase workflows, merge scenarios, conflict resolution, and Git tooling |
| `v1.4.0` | Additive expansion covering file/folder operations and direct-to-main vs. working-branch push workflows |
| `v1.5.0` | Additive expansion covering commit message/body guidance and initial commit documentation examples |
| `v1.6.0` | Additive expansion covering practical staging, unchanged tracked files, tag snapshot downloads, source ZIP vs. release asset ZIP behavior, plus quick-start and cheat-sheet companions |
| `v1.7.0` | Additive expansion covering GitHub.com tag comparison, version-diff workflows, and Pull Request workflows |
| `v1.8.0` | Additive expansion covering tracked-file rename workflows, `git mv`, rename detection, Markdown reference updates, and a Git command quick reference companion |
| `v1.9.0` | Additive expansion covering historical repository reconstruction, production tags, tag correction workflows, GitHub Releases, and LF/CRLF line-ending guidance |
| `v1.10.0` | Additive expansion covering project identity, canonical URL, GitHub Release notes, release documentation files, and import-note examples for reconstructed repositories |
| `v1.11.0` | Additive expansion covering commit-message typo detection, amend/rebase correction workflows, pushed-history safety, and force-with-lease guidance |
| `v1.11.1` | Patch correction updating internal links and active file references to use stable repository filenames while preserving intentional versioned standalone filename examples |

## Versioning Policy

This guide uses document-level semantic versioning.

- Patch updates, such as `v1.17.1`, are for small corrections, typo fixes, formatting fixes, or minor clarifications.
- Minor updates, such as `v1.18.0`, are for additive content, new examples, new appendixes, or meaningful expansions.
- Major updates, such as `v2.0.0`, are for major restructuring, rewritten guidance, or changes that significantly alter the document's organization or recommendations.
- Pre-1.0 versions, such as `v0.1.0`, are early drafts or pre-release versions.

Once this guide is managed in Git, the file should usually keep the stable filename `git-repository-guide.md`. Each meaningful version should be marked with a Git tag, such as `v1.17.0`.

## Suggested Repository Structure

```text
git-repository-guide/
├─ README.md
├─ CHANGELOG.md
├─ git-repository-guide.md
├─ git-repository-guide-quick-start-guide.md
└─ git-repository-guide-cheat-sheet.md
```

## Notes

This README is intentionally short. The full explanation belongs in the guide itself.
