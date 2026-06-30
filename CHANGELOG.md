# Changelog

All notable changes to this guide are documented here.

This project uses semantic versioning-style document versions. The active guide file should keep a stable filename, such as `git-repository-guide.md`, while versions are tracked through Git commits, tags, releases, and this changelog.

## v1.2.0

### Added

- Added guidance on stable filenames inside Git repositories.
- Added recommended repository packaging guidance for `README.md`, `CHANGELOG.md`, and `git-repository-guide.md`.
- Added the recommended repository name `git-repository-guide`.
- Added the recommended GitHub repository description: `A beginner-friendly guide to creating Git repositories and managing versioned file sets`.
- Added clearer first-time setup and later update command sequences.
- Added minimal and recommended workflows for new repositories, existing repositories, and versioned updates.
- Added explanation of why a second `git status` after `git add .` is useful.
- Added clarification of `git push`, `git push -u origin main`, `git tag`, and `git push origin <tag>`.
- Added explanation of command variables and common options.
- Added explanation of `origin`, `main`, and `master`.
- Added guidance on whether to rename an existing `master` branch to `main`.
- Added branch workflow guidance, including working branches and temporary branches.
- Added guidance on whether to work directly on `main` or use working branches.
- Added merge explanation, including fast-forward merges, merge commits, conflicts, and conflict resolution.
- Added rebase explanation, including when to use it, when to avoid it, and how it differs from merge.
- Added explanation of Git push object counts versus project file counts.
- Added Git object model basics for commits, trees, blobs, and annotated tag objects.
- Added commands for inspecting tracked files, staged changes, commit statistics, and Git object paths.
- Added a new command-sequence appendix for workflow recipes.
- Added terminology guidance for “repository” vs. “repo.”

### Changed

- Updated the guide metadata from `v1.1.0` to `v1.2.0`.
- Updated README guidance to use `git-repository-guide.md` as the stable main guide filename.
- Clarified version history for `v0.1.0`, `v1.0.0`, `v1.1.0`, and `v1.2.0`.
- Clarified that `Version 0.1.0` is an appropriate annotated tag message even for a pre-release draft.
- Clarified that `git remote -v` is optional verification, not a required command for every update.
- Clarified that direct-to-`main` workflows are simple and acceptable for small solo projects, but branch-based workflows are safer for larger or collaborative work.
- Clarified that version tags should usually be created after final changes are merged into `main`.
- Moved the references appendix from Appendix G to Appendix H so the new command-sequence appendix could be Appendix G.

### Notes

- This is an additive update from `v1.1.0`.
- Existing guide content was preserved except for targeted version, structure, clarity, and consistency updates.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.2.0.md`.

## v1.1.0

### Added

- Added expanded Git tagging and versioned file-set guidance.
- Added a Knowledge Base and How-To Reference appendix.
- Added additional questions and answers for common novice-to-advanced Git scenarios.
- Added explanations for whether tags apply to the whole repository or selected files.
- Added guidance for versioning source code, test cases, and related files in one repository.
- Added guidance for when multiple repositories may be more appropriate.
- Added expanded retrieval/download options for specific versions.
- Added Git pager guidance, including common pager keys and how to bypass the pager.
- Added repository naming and GitHub description guidance.
- Added README and changelog recommendations.

### Changed

- Updated annotated tag message examples to prefer `Version 1.0.0` over `Version v1.0.0`.
- Clarified that the leading `v` belongs to the tag name, while the human-readable version number is usually written without repeating the `v` in the tag message.
- Expanded supporting references and command coverage.

### Notes

- This was an additive update from `v1.0.0`.
- Existing guide content was intended to be preserved except for targeted clarity and consistency updates.

## v1.0.0

### Added

- Established the first complete locked baseline of the guide.
- Added core guidance for creating a Git repository.
- Added command-line setup instructions.
- Added GitHub repository creation guidance.
- Added Visual Studio Code workflow guidance.
- Added Git tag and versioning explanations.
- Added references, appendixes, command summaries, and index structure.

### Notes

- This version represents the first complete version of the guide.

## v0.1.0

### Added

- Created the original pre-release draft of the guide.
- Introduced the basic workflow for creating a Git repository.
- Introduced early guidance for commits, tags, and versioning.

### Notes

- This version is considered an early draft or pre-release guide.
- It predates the more formal versioning and locking approach used for `v1.0.0` and later.
