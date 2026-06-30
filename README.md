# Git Repository Guide

A beginner-friendly guide to creating Git repositories and managing versioned file sets

## About

This repository contains a standalone Markdown guide that explains how to create a Git repository, connect it to GitHub, commit files, mark versioned snapshots with tags, retrieve earlier versions, and understand the difference between Git tags, GitHub Releases, and production deployments.

The guide is written in a conversational style for novice-to-advanced users. It focuses on practical command-line workflows while also covering Visual Studio Code usage.

## Main Guide

Current guide version: `v1.2.0`

Main guide file:

```text
git-repository-guide.md
```

The active guide file should keep this stable filename. Version history should be tracked through Git commits, tags, releases, and this changelog rather than by renaming the file for each version.

## Topics Covered

- Creating a local Git repository
- Creating a GitHub repository
- Using Git from the command line
- Using Git from Visual Studio Code
- Writing useful commit messages
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
- Understanding `origin`, `main`, and `master`
- Creating and using working branches
- Merging and resolving merge conflicts
- Understanding rebasing and when to avoid it
- Understanding Git push object counts

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

## Versioning Policy

This guide uses document-level semantic versioning.

- Patch updates, such as `v1.2.1`, are for small corrections, typo fixes, formatting fixes, or minor clarifications.
- Minor updates, such as `v1.3.0`, are for additive content, new examples, new appendixes, or meaningful expansions.
- Major updates, such as `v2.0.0`, are for major restructuring, rewritten guidance, or changes that significantly alter the document's organization or recommendations.
- Pre-1.0 versions, such as `v0.1.0`, are early drafts or pre-release versions.

Once this guide is managed in Git, the file should usually keep the stable filename `git-repository-guide.md`. Each meaningful version should be marked with a Git tag, such as `v1.2.0`.

## Suggested Repository Structure

```text
git-repository-guide/
├─ README.md
├─ CHANGELOG.md
└─ git-repository-guide.md
```

## Notes

This README is intentionally short. The full explanation belongs in the guide itself.
