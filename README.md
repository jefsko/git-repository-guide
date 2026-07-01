# Git Repository Guide

A beginner-friendly guide to creating Git repositories and managing versioned file sets

## About

This repository contains a standalone Markdown guide that explains how to create a Git repository, connect it to GitHub, commit files, mark versioned snapshots with tags, retrieve earlier versions, and understand the difference between Git tags, GitHub Releases, and production deployments.

The guide is written in a conversational style for novice-to-advanced users. It focuses on practical command-line workflows while also covering Visual Studio Code usage.

## Main Guide

Current guide version: `v1.6.0`

Main guide file:

```text
git-repository-guide.md
```

The active guide file should keep this stable filename. Version history should be tracked through Git commits, tags, releases, and this changelog rather than by renaming the file for each version.

## Which file should I open first?

| Goal | Start here |
|---|---|
| I want the fastest practical setup path. | [`git-repository-guide-quick-start-guide-v1.6.0.md`](git-repository-guide-quick-start-guide-v1.6.0.md) |
| I want a compact repeat checklist. | [`git-repository-guide-cheat-sheet-v1.6.0.md`](git-repository-guide-cheat-sheet-v1.6.0.md) |
| I need the full explanation and reference material. | [`git-repository-guide.md`](git-repository-guide.md) |

## Repository Contents

| File | Purpose |
|---|---|
| [`README.md`](README.md) | Repository overview and navigation. |
| [`CHANGELOG.md`](CHANGELOG.md) | Version history and notable changes. |
| [`git-repository-guide.md`](git-repository-guide.md) | Full guide with complete explanations, examples, appendixes, and references. |
| [`git-repository-guide-quick-start-guide-v1.6.0.md`](git-repository-guide-quick-start-guide-v1.6.0.md) | Short, sequential companion guide for the most common Git repository/version-tag workflow. |
| [`git-repository-guide-cheat-sheet-v1.6.0.md`](git-repository-guide-cheat-sheet-v1.6.0.md) | Compact checklist for repeating the common workflow after learning it. |

## Full Guide vs. Quick-Start vs. Cheat Sheet

- Use the **full guide** when you want complete explanations, edge cases, appendixes, and reference material.
- Use the **quick-start guide** when you want the shortest practical path that is still complete enough to follow.
- Use the **cheat sheet** when you already understand the workflow and want a compact repeat checklist.

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

## Versioning Policy

This guide uses document-level semantic versioning.

- Patch updates, such as `v1.6.1`, are for small corrections, typo fixes, formatting fixes, or minor clarifications.
- Minor updates, such as `v1.7.0`, are for additive content, new examples, new appendixes, or meaningful expansions.
- Major updates, such as `v2.0.0`, are for major restructuring, rewritten guidance, or changes that significantly alter the document's organization or recommendations.
- Pre-1.0 versions, such as `v0.1.0`, are early drafts or pre-release versions.

Once this guide is managed in Git, the file should usually keep the stable filename `git-repository-guide.md`. Each meaningful version should be marked with a Git tag, such as `v1.6.0`.

## Suggested Repository Structure

```text
git-repository-guide/
├─ README.md
├─ CHANGELOG.md
├─ git-repository-guide.md
├─ git-repository-guide-quick-start-guide-v1.6.0.md
└─ git-repository-guide-cheat-sheet-v1.6.0.md
```

## Notes

This README is intentionally short. The full explanation belongs in the guide itself.
