# Changelog

All notable changes to this guide are documented here.

This project uses semantic versioning-style document versions. The active guide file should keep a stable filename, such as `git-repository-guide.md`, while versions are tracked through Git commits, tags, releases, and this changelog.

## v1.18.0

### Added

- Added guidance comparing `git add .` and `git add -A`, including current-folder scope versus whole-repository staging.
- Added a practical staged/unstaged review sequence using `git status --short`, `git diff --stat`, `git diff --cached --stat`, and `git diff --cached --name-status --find-renames`.
- Added a working tree, index/staging area, and `HEAD` reminder to clarify why staged and unstaged changes can differ.
- Added rename detection guidance using `git status --short --renames`, `git diff --cached --summary`, and `git diff --cached --name-status --find-renames`.
- Added `git mv` destination-file caution explaining that `git mv` does not overwrite an existing destination by default.
- Added PowerShell folder creation guidance using `New-Item -ItemType Directory -Force`.
- Added `.gitattributes` existence check guidance using `Test-Path .\.gitattributes`.
- Added precise wording guidance recommending `committed locally and pushed to origin` instead of `checked into origin`.
- Added targeted Troubleshooting entries for staging scope, rename display, `git mv` destination conflicts, `.gitattributes` checks, line-ending surprises, and precise `origin` wording.
- Added Knowledge Base entries for staging commands, staged review, rename detection, `git mv`, PowerShell folder creation, `.gitattributes` checks, and `origin` wording.

### Changed

- Updated the guide metadata from `v1.17.0` to `v1.18.0`.
- Expanded existing staging, rename, status, line-ending, and remote/origin wording coverage with practical pre-commit review workflows.
- Updated README version, version history, and topic list for `v1.18.0`.
- Updated quick-start, cheat sheet, and command quick reference companions to align with `v1.18.0`.

### Notes

- This is an additive update from `v1.17.0`.
- Existing staging, file/folder, rename, line-ending, remote, and workflow guidance was preserved.
- No new broad Common Scenarios appendix was created.
- The existing Troubleshooting appendix was used for concrete problem/fix entries from the addendum.
- `How-To` style material was added to the existing Knowledge Base and How-To Reference instead of creating a separate how-to section.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.18.0.md`.

## v1.17.0

### Added

- Added a consolidated recommended-defaults section for common Git guide choices, including `main`, `origin`, annotated version tags, pre-release tags, stable tags, tag messages, and line-ending policy.
- Added a compact remote vocabulary reminder for `origin`, `main`, `origin/main`, local repositories, remote repositories, and working trees.
- Added guidance for choosing `v0.x.0` pre-release snapshots versus `v1.0.0` stable baseline releases.
- Added pre-release and stable annotated tag message examples.
- Added GitHub Release title and release-note structure guidance.
- Added synchronized multi-repo tag guidance for projects that intentionally release related repositories together.
- Added line-ending renormalization guidance using `git add --renormalize .`.
- Added PowerShell repository search recipes for all files, Markdown files, and unique matching paths.
- Added repository publishing readiness and GitHub Pages verification checklists.
- Added final branch, tag, remote, release, and line-ending verification commands.
- Added Knowledge Base entries for beginner-friendly defaults, `origin`/`main`/`origin/main`, pre-release tags, synchronized tags, publishing readiness, and line-ending renormalization.

### Changed

- Updated the guide metadata from `v1.16.0` to `v1.17.0`.
- Expanded existing remote, versioning, tag, release, line-ending, repository publishing, and verification guidance with consolidated checklists.
- Updated README version, version history, and topic list for `v1.17.0`.
- Updated quick-start, cheat sheet, and command quick reference companions to align with `v1.17.0`.

### Notes

- This is an additive update from `v1.16.0`.
- Existing detailed sections and topic-specific scenario appendices were preserved.
- No new broad Common Scenarios appendix was created; the addendum content was integrated as a consolidated defaults and verification section plus targeted companion-file updates.
- Duplicate material from the consolidated addendum was not re-added unless it provided clearer defaults, a useful checklist, or a more practical command sequence.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.17.0.md`.

## v1.16.0

### Added

- Added guidance distinguishing local parent folder renames, tracked file/folder renames, GitHub repository renames, remote URL updates, and project/application name changes.
- Added decision tables explaining which rename types require Git commits and which require remote URL updates.
- Added GitHub repository rename guidance, including when renaming is useful and what risks to check.
- Added `git remote set-url` workflow examples for updating `origin` after a GitHub repository rename.
- Added PowerShell and Git examples for renaming tracked folders and searching for old-name references.
- Added old-name cleanup guidance for README files, docs, badges, scripts, project files, deployment configuration, and GitHub Pages references.
- Added commit-message recommendations for rename work, including `chore:`, `docs:`, and `fix:` examples.
- Added a dedicated topic-specific scenario appendix for repository renaming and rename workflows.
- Added Knowledge Base entries for local folder renames, tracked rename commits, GitHub repo renames, `git remote set-url`, old-name search, and rename troubleshooting placement.

### Changed

- Updated the guide metadata from `v1.15.0` to `v1.16.0`.
- Expanded existing file/folder rename and remote guidance with repository-level and project-level rename scenarios.
- Updated README version, version history, and topic list for `v1.16.0`.
- Updated quick-start, cheat sheet, and command quick reference companions to align with `v1.16.0`.
- Moved the references appendix from Appendix X to Appendix Z so references remain last.
- Refined scenario appendix titles by removing the generic phrase “Common Scenarios” from topic-specific appendix names.

### Notes

- This is an additive update from `v1.15.0`.
- Existing stable filename guidance was preserved.
- Existing related-repository guidance from `v1.15.0` was preserved.
- Existing file rename guidance was not replaced; repository/folder/project rename guidance was added around it.
- Rename guidance was placed in a topic-specific scenario appendix rather than Troubleshooting because most rename work is planned cleanup. Troubleshooting remains appropriate for broken links, stale remotes, GitHub Pages issues, or rename detection surprises.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.16.0.md`.

## v1.15.0

### Added

- Added guidance for linking related GitHub repositories without making them technically nested or dependent.
- Added a ranked strategy for connecting related repos with README links, GitHub topics, GitHub About/website links, tags/releases, submodules, and subtree.
- Added hub-and-example repository guidance using the Simple Website Examples series as a case study.
- Added cross-repository link guidance explaining when to use same-repo relative links versus absolute GitHub URLs.
- Added examples for hub README tables and individual example README previous/next navigation.
- Added guidance for avoiding sibling-folder relative links as the final form for separate GitHub repositories.
- Added GitHub topics and repository description examples for a related repo series.
- Added guidance explaining that tags and releases are repository-specific, even when related repos use consistent version names.
- Added Git CLI, Visual Studio Code, and Visual Studio workflow summaries for committing, pushing, tagging, and releasing.
- Added a common-scenarios appendix for multi-repository linking and release workflows.
- Added Knowledge Base entries for related repos, cross-repo links, submodules, subtree, hub README navigation, tags across repos, and multi-repo check-in workflows.

### Changed

- Updated the guide metadata from `v1.14.0` to `v1.15.0`.
- Expanded existing repository hygiene, README, GitHub topics, commit, tag, and release workflow coverage with multi-repository examples.
- Updated README version, version history, and topic list for `v1.15.0`.
- Updated quick-start, cheat sheet, and command quick reference companions to align with `v1.15.0`.
- Moved the references appendix from Appendix W to Appendix X so references remain last.

### Notes

- This is an additive update from `v1.14.0`.
- Existing stable filename guidance was preserved.
- Existing push/tag/repository hygiene guidance from `v1.13.0` was preserved.
- Existing GitHub file search and commit-history lookup guidance from `v1.14.0` was preserved.
- Submodules and subtree were mentioned as advanced alternatives but not recommended for beginner-friendly educational example repos.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.15.0.md`.

## v1.14.0

### Added

- Added GitHub.com guidance for searching inside the currently open file with `Ctrl+F` or `Cmd+F`.
- Added GitHub web-editor shortcut guidance using `.` for editor-style file navigation.
- Added GitHub `path:` search qualifier examples for limiting search to a specific file path.
- Added expanded tag-inspection commands, including `git tag --sort=-v:refname`, `git show-ref --tags`, `git log --tags --simplify-by-decoration --oneline`, and `git describe --tags`.
- Added guidance distinguishing Git tags from GitHub Releases when listing version markers.
- Added expanded commit-message inspection commands, including `git log --format=%B`, `git log --format=%s`, `git log --author`, and `git log -n`.
- Added beginner reminder to press `q` to exit the `git log` or `git show` pager.
- Added a dedicated appendix for GitHub file search, tag inspection, and commit-history lookup scenarios.
- Added Knowledge Base entries for GitHub file search, tag sorting, tag inspection, commit-message lookup, and exiting the pager.

### Changed

- Updated the guide metadata from `v1.13.0` to `v1.14.0`.
- Expanded existing tag, commit-history, GitHub.com, cheat-sheet, and command-reference coverage with additional inspection and search commands.
- Clarified later-update push examples by showing the difference between plain `git push` and explicit `git push origin main`.
- Updated README version, version history, and topic list for `v1.14.0`.
- Updated quick-start, cheat sheet, and command quick reference companions to align with `v1.14.0`.
- Moved the references appendix from Appendix V to Appendix W so references remain last.

### Notes

- This is an additive update from `v1.13.0`.
- Existing push/tag/repository hygiene guidance from `v1.13.0` was preserved.
- Existing commit-message prefix and correction guidance was preserved.
- Existing stable filename guidance was preserved.
- Duplicate tag, log, and commit-message explanations were not re-added unless the addendum provided more detail, clearer examples, or better placement.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.14.0.md`.

## v1.13.0

### Added

- Added guidance explaining when plain `git push` behaves like `git push origin main`.
- Added a safer mental model for plain `git push` versus explicit branch pushes.
- Added guidance explaining why branch pushes and tag pushes both matter.
- Added consequences of pushing a tag without pushing `main`.
- Added verification commands for branch/tag state, including `git branch -vv`, `git log origin/main..main`, and `git log main..origin/main`.
- Added a recommended commit, push, and tag sequence for careful versioned guide or website repos.
- Added guidance for direct-to-`main`, working branch, and detached `HEAD` workflows.
- Added repository hygiene guidance for `docs/`, `archive/`, `assets/`, `src/`, `public/`, `dist/`, `site/`, `scripts/`, and `.github/`.
- Added `.gitignore` guidance, including the rule that `.gitignore` only ignores untracked files.
- Added `.gitkeep` guidance for preserving intentionally empty folders.
- Added GitHub topics guidance and examples.
- Added a concise line-ending and `.gitattributes` policy reminder that cross-references the existing detailed line-ending section.
- Added a dedicated appendix for push, tag, branch, and repository hygiene scenarios.
- Added Knowledge Base entries for explicit push behavior, branch/tag pushes, `.gitignore`, `.gitkeep`, GitHub topics, and line-ending policy.

### Changed

- Updated the guide metadata from `v1.12.0` to `v1.13.0`.
- Expanded existing push/tag guidance with more explicit branch-vs-tag push examples.
- Expanded repository hygiene guidance with folder conventions and ignore/placeholder file guidance.
- Updated README version, version history, and topic list for `v1.13.0`.
- Updated quick-start, cheat sheet, and command quick reference companions to align with `v1.13.0`.
- Moved the references appendix from Appendix U to Appendix V so references remain last.

### Notes

- This is an additive update from `v1.12.0`.
- Existing line-ending and `.gitattributes` guidance was preserved; only concise policy reminders and static-site examples were added.
- Existing commit-message prefix guidance from `v1.12.0` was preserved.
- Existing stable filename guidance from `v1.11.1` was preserved.
- The addendum's `v1.19.0` and `v1.20.0` examples were treated as case-study examples, not as guide-version targets.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.13.0.md`.

## v1.12.0

### Added

- Added guidance for common commit-message prefixes such as `feat`, `fix`, `docs`, `chore`, `refactor`, `style`, `test`, `build`, `ci`, `perf`, `revert`, and `release`.
- Added clarification that commit-message prefixes are not Git commands and are not enforced by Git by default.
- Added a ranked prefix table for documentation repositories, website repositories, release packages, and small project/versioned file sets.
- Added prefix-specific examples for documentation, website, metadata, release, formatting, testing, build, CI, performance, and revert workflows.
- Added a decision table for choosing the best prefix.
- Added guidance distinguishing commit messages, tag names, annotated tag messages, GitHub Release titles, and GitHub Release notes.
- Added guidance for recommended subject style, optional scopes, and breaking-change notation.
- Added a dedicated appendix for commit-message prefix scenarios and examples.
- Added Knowledge Base entries for `feat`, `fix`, `docs`, `chore`, `style`, scopes, and breaking changes.
- Added quick-start, cheat-sheet, and command quick-reference coverage for commit-message prefix selection.

### Changed

- Updated the guide metadata from `v1.11.1` to `v1.12.0`.
- Expanded commit-message guidance beyond message correction workflows to include prefix selection and consistent commit-history style.
- Updated README version, version history, and topic list for `v1.12.0`.
- Updated quick-start, cheat sheet, and command quick reference companions to align with `v1.12.0`.
- Moved the references appendix from Appendix T to Appendix U so references remain last.

### Notes

- This is an additive update from `v1.11.1`.
- Existing commit-message typo correction guidance was preserved.
- Existing stable filename guidance from `v1.11.1` was preserved.
- Duplicate commit-message style content was not re-added unless it provided more detail, ranking, or examples.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.12.0.md`.

## v1.11.1

### Changed

- Updated internal repo links and active file references to use stable repository filenames.
- Added the filename-reference rule: internal repo links and active file references should use stable filenames, while standalone download filename examples and historical changelog entries may still use versioned filenames when that is the point being explained.
- Preserved versioned standalone download filename examples where they are intentionally used to describe downloadable copies outside the repository.
- Preserved historical changelog entries that mention versioned standalone filenames.

### Notes

- This is a patch correction from `v1.11.0`.
- No substantive Git workflow content was added, removed, or restructured.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may continue to use versioned filenames, such as `git-repository-guide-v1.11.1.md`.

## v1.11.0

### Added

- Added guidance for quickly checking commit messages across a repository.
- Added `git log --grep` examples for finding typo patterns in commit messages.
- Added guidance for fixing the most recent commit message with `git commit --amend`.
- Added guidance for fixing older commit messages with interactive rebase and `reword`.
- Added guidance explaining that changing a commit message rewrites the commit and changes its hash.
- Added pushed-commit guidance, including when `git push --force-with-lease` is appropriate.
- Added warnings for when not to rewrite shared, protected, tagged, released, or deployed history.
- Added guidance for tag and GitHub Release implications when rewriting a tagged commit.
- Added PowerShell examples for amending commit messages with subject/body text.
- Added a dedicated appendix for commit-message correction scenarios.
- Added Knowledge Base entries for commit-message search, amend, reword, force-with-lease, and rebase recovery.
- Added command quick-reference and cheat-sheet examples for commit-message typo workflows.

### Changed

- Updated the guide metadata from `v1.10.0` to `v1.11.0`.
- Expanded commit-message guidance beyond message style and commit bodies to include correction workflows.
- Clarified the difference between correcting commit messages and correcting annotated tag messages.
- Moved the references appendix from Appendix S to Appendix T so references remain last.
- Updated README version, version history, topics, and companion-guide links for `v1.11.0`.
- Updated quick-start, cheat sheet, and command quick reference companions to align with `v1.11.0`.

### Notes

- This is an additive update from `v1.10.0`.
- Existing tag-message correction guidance was preserved.
- Duplicate tag-correction content was not re-added; this update focuses on commit-message correction.
- Existing guide content was preserved except for targeted version, structure, clarity, reference, and consistency updates.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.11.0.md`.

## v1.10.0

### Added

- Added expanded project-identity guidance for reconstructed domain-based repositories.
- Added canonical URL and optional alias guidance using the `demo-jeffskone-com` case study.
- Added guidance for distinguishing repository name, production URL, site heading, browser title, and optional alias.
- Added GitHub Release title and release-notes structure examples.
- Added a practical release-notes template with summary, production publish date, highlights, and notes.
- Added expanded documentation-file guidance for reconstructed repositories, including `RELEASES.md` and `IMPORT-NOTES.md`.
- Added Appendix P examples for website identity, pre-import cleanup, release notes, GitHub Release titles, and documentation files.
- Added Knowledge Base entries for domain-based repository names, canonical URLs, historical domain preservation, GitHub Release notes, and reconstructed-repository documentation files.

### Changed

- Updated the guide metadata from `v1.9.0` to `v1.10.0`.
- Expanded existing historical repository reconstruction guidance without duplicating already-covered tag repair or line-ending material.
- Updated README version, version history, topics, and companion-guide links for `v1.10.0`.
- Updated quick-start, cheat sheet, and command quick reference companions to align with `v1.10.0`.
- Clarified that some v1.10.0 addendum material was already covered in v1.9.0 and only relevant additional details were incorporated.

### Notes

- This is an additive update from `v1.9.0`.
- Existing guide content was preserved except for targeted version, structure, clarity, reference, and consistency updates.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.10.0.md`.
- The v1.10.0 addendum overlapped heavily with v1.9.0 historical reconstruction content; duplicate material was not re-added unless it provided more detail or examples.

## v1.9.0

### Added

- Added guidance for reconstructing a Git repository from historical version folders.
- Added practical `demo-jeffskone-com` case-study guidance for repository naming, repository description, canonical domain context, and historical import decisions.
- Added guidance for distinguishing production releases from offline development snapshots.
- Added guidance to import each historical version folder as a sequential commit while tagging only production-release commits.
- Added recommended production tag strategy using annotated tags.
- Added guidance for optional GitHub Releases created from production tags.
- Added tag correction workflows for local unpushed tags, pushed tags on the current commit, and pushed tags from older commits.
- Added explanation of `$commit = git rev-list -n 1 vX.Y.Z` and why it prevents accidentally moving an older tag to `HEAD`.
- Added guidance for `git tag -n99`, annotated tag messages, and checking tags locally.
- Added guidance for LF vs. CRLF line-ending warnings on Windows.
- Added recommended `.gitattributes` starter content for Windows-managed website/documentation repositories.
- Added guidance for inspecting line endings with `git ls-files --eol`.
- Added dedicated appendixes for historical repository reconstruction, tag correction scenarios, and line-ending scenarios.
- Added Knowledge Base entries for historical imports, production tags, tag correction, `git tag -n99`, LF/CRLF, `.gitattributes`, and `git ls-files --eol`.
- Added related command quick-reference entries for `git rev-list`, `git ls-remote`, `git ls-files`, and `.gitattributes` workflows.

### Changed

- Updated the guide metadata from `v1.8.0` to `v1.9.0`.
- Expanded tag guidance beyond creating and pushing tags to include correction and repair workflows.
- Expanded production-release guidance with a historical reconstruction case study.
- Expanded line-ending guidance with a practical Windows-focused `.gitattributes` policy.
- Moved the references appendix from Appendix O to Appendix S so references remain last.
- Updated README version, version history, topics, and companion-guide links for `v1.9.0`.
- Updated quick-start, cheat sheet, and command quick reference companions to align with `v1.9.0` and include the new practical guidance.

### Notes

- This is an additive update from `v1.8.0`.
- Existing guide content was preserved except for targeted version, structure, clarity, reference, and consistency updates.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.9.0.md`.

## v1.8.0

### Added

- Added Git command quick reference `git-command-quick-reference-v1.8.0.md` with common commands, descriptions, syntax, required parameters, optional parameters, and practical notes.
- Added top-ranked common Git command section in the command quick reference.
- Added alphabetical Git command reference covering frequently used commands.
- Added placeholder and status-code reference tables in the command quick reference.
- Added expanded guidance for renaming tracked files in a Git repository.
- Added `git mv` workflow examples for intentional file renames.
- Added PowerShell rename examples using `git mv`, `Rename-Item`, and `ren`.
- Added guidance for updating Markdown links and references after a file rename.
- Added explanation of why `git add -A` is preferred for rename-related changes.
- Added staged verification commands using `git diff --cached --summary` and `git diff --cached --name-status --find-renames`.
- Added explanation that Git stores snapshots and usually infers renames from deleted and added paths with similar content.
- Added guidance for when a rename may appear as delete plus add.
- Added troubleshooting workflow for accidentally deleting the old file and copying in the renamed file manually.
- Added guidance for viewing file history after a rename with `git log --follow`.
- Added optional commit-body examples for rename commits.
- Added a dedicated appendix for file rename and move scenarios.
- Added Knowledge Base entries for `git mv`, `git add -A`, rename detection, delete/add displays, and rename history.

### Changed

- Updated the guide metadata from `v1.7.0` to `v1.8.0`.
- Expanded existing file/folder rename coverage with a dedicated tracked-file rename workflow.
- Clarified when `git mv` is recommended and when manual rename plus `git add -A` can still work.
- Clarified that versioned standalone filenames are different from stable active repository filenames.
- Moved the references appendix from Appendix N to Appendix O so references remain last.
- Updated README version, version history, topics, and companion-guide links for `v1.8.0`.
- Updated quick-start and cheat-sheet companions to align with `v1.8.0` and include practical rename guidance.
- Updated README navigation and repository contents to include the command quick reference.
- Updated quick-start and cheat sheet links to mention the command quick reference.

### Notes

- This is an additive update from `v1.7.0`.
- Existing guide content was preserved except for targeted version, structure, clarity, reference, and consistency updates.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.8.0.md`.
- The command quick reference was added as an additional `v1.8.0` companion file rather than a new version bump.

## v1.7.0

### Added

- Added expanded guidance for identifying files changed between version tags.
- Added `git diff --name-status` examples for added, modified, deleted, renamed, and copied files.
- Added `--diff-filter` examples for showing only added, modified, or added-and-modified files.
- Added clarification of the difference between files contained in a tag and files changed between tags.
- Added GitHub.com Compare page navigation for comparing tags.
- Added GitHub compare URL patterns, including explicit `tags/` comparison.
- Added troubleshooting guidance for compare URLs that do not work.
- Added guidance for comparing releases from GitHub's Releases page.
- Added expanded Pull Request guidance from beginner workflows through more common and advanced scenarios.
- Added guidance for Pull Request titles, descriptions, reviews, follow-up commits, out-of-date branches, merge options, cleanup, and tagging after merge.
- Added dedicated appendixes for compare/diff/tag inspection scenarios and Pull Request scenarios.
- Added Knowledge Base entries for tag comparison and Pull Request workflows.
- Added official GitHub documentation references for comparing commits/tags, comparing releases, Pull Requests, reviews, merge options, and draft Pull Requests.

### Changed

- Updated the guide metadata from `v1.6.0` to `v1.7.0`.
- Expanded existing compare guidance beyond command-line examples.
- Expanded existing Pull Request coverage beyond the basic branch-and-merge workflow.
- Clarified when direct-to-`main` is acceptable and when Pull Requests are preferred.
- Clarified that version tags should usually be created from `main` after a Pull Request has been merged.
- Moved the references appendix from Appendix L to Appendix N so references remain last.
- Renumbered duplicate Knowledge Base entries so Appendix F remains sequential and unambiguous.
- Updated README version, version history, topics, and companion-guide links for `v1.7.0`.
- Updated quick-start and cheat-sheet companions to align with `v1.7.0` and include compare/Pull Request guidance.

### Notes

- This is an additive update from `v1.6.0`.
- Existing guide content was preserved except for targeted version, structure, clarity, reference, and consistency updates.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.7.0.md`.

## v1.6.0

### Added

- Added quick-start companion guide `git-repository-guide-quick-start-guide-v1.6.0.md`.
- Added compact cheat sheet `git-repository-guide-cheat-sheet-v1.6.0.md`.
- Added README navigation showing which file to open first.
- Added README repository contents table covering the full guide, quick-start guide, and cheat sheet.
- Added a practical staging example showing modified files, new untracked files, and unchanged tracked files.
- Added explanation that unchanged tracked files do not appear in `git status` but remain part of the repository snapshot.
- Added clarification that `git add .` stages new, modified, and deleted files under the current directory, including subfolders.
- Added warning not to delete unchanged tracked files just to simplify `git add .`.
- Added recovery commands for accidentally deleted tracked files.
- Added explicit `git rm` workflow for intentionally removing tracked files from the repository.
- Added explanation that tags point to full repository snapshots, not only files changed in the tagged commit.
- Added clarification that GitHub automatic source ZIP downloads for a tag contain the tracked repository snapshot at that tag.
- Added distinction between GitHub automatic source ZIPs and custom release asset ZIPs.
- Added a dedicated appendix for practical staging, tag, and download scenarios.
- Added Knowledge Base entries for `git add .`, unchanged files, staged deletions, tag downloads, and release asset ZIPs.

### Changed

- Updated README repository contents and navigation for the new companion files.
- Clarified the difference between the full guide, quick-start guide, and cheat sheet in README.
- Updated the guide metadata from `v1.5.0` to `v1.6.0`.
- Expanded practical staging guidance with a real-world documentation repository example.
- Clarified how repository snapshots explain why a tag download may include unchanged files.
- Clarified the difference between source archive downloads and manually uploaded release assets.
- Added a new Appendix K for practical staging, tag, and download scenarios.
- Moved the references appendix from Appendix K to Appendix L so references remain last.

### Notes

- This is an additive update from `v1.5.0`.
- Existing guide content was preserved except for targeted version, structure, clarity, and consistency updates.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.6.0.md`.

## v1.5.0

### Added

- Added guidance explaining the difference between a commit message summary/title and an optional commit body/description.
- Added clarification that a Git commit only requires a summary; a longer body is optional.
- Added examples of one-line commits using a single `-m` flag.
- Added examples of two-part commits using multiple `-m` flags.
- Added explanation that the first `-m` creates the summary and the second `-m` creates the body.
- Added practical guidance for when a one-line commit is enough and when a commit body is useful.
- Added clarification that commit bodies, repository descriptions, README summaries, and changelog entries are different artifacts with different purposes.
- Added a recommended initial-commit pattern for documentation projects.
- Added a dedicated appendix with commit message and commit body examples.
- Added Knowledge Base entries for commit summaries, commit bodies, commit descriptions, and repository descriptions.

### Changed

- Updated the guide metadata from `v1.4.0` to `v1.5.0`.
- Expanded commit-message guidance beyond short commit summaries.
- Clarified that a commit body is useful for context but is not required.
- Clarified that the README and CHANGELOG do not replace a useful commit summary or optional commit body.
- Added a new Appendix J for commit message and commit body examples.
- Moved the references appendix from Appendix J to Appendix K so references remain last.

### Notes

- This is an additive update from `v1.4.0`.
- Existing guide content was preserved except for targeted version, structure, clarity, and consistency updates.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.5.0.md`.

## v1.4.0

### Added

- Added expanded guidance for adding files and folders to a repository.
- Added explanation that Git tracks files and file paths, not empty folders directly.
- Added guidance for adding empty folders using placeholder files such as `.gitkeep`.
- Added expanded guidance for updating tracked files with verification commands.
- Added expanded guidance for drop-in replacing existing files with newer local versions.
- Added explanation of delete-then-replace behavior before staging or committing.
- Added explanation of how delete-then-replace differs from committing a deletion and adding a replacement later.
- Added guidance for removing/deleting files with `git rm`.
- Added guidance for removing/deleting folders with `git rm -r`.
- Added guidance for stopping tracking while keeping files locally with `git rm --cached`.
- Added guidance for moving and renaming files and folders with `git mv`.
- Added guidance for moving files or folders outside Git and staging the result with `git add -A`.
- Added comparison of multiple file/folder move methods and when to use each.
- Added verification commands for reviewing adds, updates, deletions, moves, renames, and replacements before committing.
- Added guidance comparing direct pushes to `main` with pushing a working branch to `origin`.
- Added explanation of `git push -u origin main` versus `git push -u origin <branch-name>`.
- Added pros and cons for pushing directly to `main`.
- Added pros and cons for pushing a working branch.
- Added a decision table for when to push directly to `main` and when to use a working branch.
- Added clarification that `origin/main` is a remote-tracking reference, while `main` is the local branch.
- Added guidance that version tags should usually be created on `main` after the working branch has been merged.
- Added a dedicated appendix for file and folder operation scenarios.
- Added Knowledge Base entries for file/folder operations and push-target decisions.

### Changed

- Updated the guide metadata from `v1.3.0` to `v1.4.0`.
- Expanded the existing file update workflow coverage beyond basic file examples.
- Clarified the distinction between editing, replacing, deleting, removing, moving, renaming, and stopping tracking.
- Clarified that Git records the final staged snapshot, not every intermediate local file-manager action.
- Clarified that a same-path drop-in replacement is usually treated like a modification.
- Clarified that the direct-to-`main` workflow is a beginner-friendly baseline, not the safest default for all projects.
- Clarified that branch-based workflows are preferred for reviewed, collaborative, risky, or deployment-related changes.
- Added a new Appendix I for file and folder operation scenarios.
- Moved the references appendix from Appendix I to Appendix J so references remain last.
- Cleaned up a duplicated introductory paragraph in the changelog source while preserving prior version entries.

### Notes

- This is an additive update from `v1.3.0`.
- Existing guide content was preserved except for targeted version, structure, clarity, and consistency updates.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.4.0.md`.

## v1.3.0

### Added

- Added explicit guidance for adding new files to a repository.
- Added explicit guidance for updating, replacing, deleting, renaming, and moving tracked files.
- Added explanation that ordinary single-user file updates usually do not require merging when history has not diverged.
- Added clarification that Git does not normally use old-style exclusive file checkout or locking.
- Added distinction between `git add`, `git commit`, `git push`, `git fetch`, `git pull`, `git merge`, and `git rebase`.
- Added dedicated explanation of `git fetch`, `git pull`, `git merge`, and `git rebase`.
- Added syntax tables showing required and optional parts of fetch, pull, merge, and rebase commands.
- Added decision guidance for when to use fetch vs. pull, merge vs. rebase, and pull vs. fetch-plus-merge.
- Added explanation that push rejection is not the same as a merge conflict.
- Added multi-user scenarios showing when merges happen and when conflicts appear.
- Added examples for same-file edits, different-line edits, same-line conflicts, delete/modify conflicts, add/add conflicts, rename/edit conflicts, binary conflicts, and semantic/logical conflicts.
- Added multiple conflict-resolution strategies, including manual editing, VS Code merge editor, Git mergetool, choosing one side, aborting, and resolving simple conflicts on GitHub.
- Added guidance for diff, comparison, merge, and conflict-resolution tools.
- Added ranked Git tool recommendations with pros and cons.
- Added a dedicated appendix for file update, merge, and conflict scenarios.
- Added additional Knowledge Base entries for file updates, fetch, pull, merge, rebase, and conflict-resolution concepts.

### Changed

- Updated the guide metadata from `v1.2.0` to `v1.3.0`.
- Expanded the existing merging discussion from a brief conceptual overview into a scenario-based explanation.
- Clarified that merging is about combining histories, not merely replacing a file with a newer local version.
- Clarified that two users editing the same file does not always create a conflict.
- Clarified that `git pull` performs fetch plus integration, commonly merge by default or rebase with `--rebase`.
- Clarified that beginners should generally use merge as the safer default and treat rebase as an advanced/private-branch tool.
- Added a new Appendix H for file update, merge, and conflict scenarios.
- Moved the references appendix from Appendix H to Appendix I so references remain last.

### Notes

- This is an additive update from `v1.2.0`.
- Existing guide content was preserved except for targeted version, structure, clarity, and consistency updates.
- The active repository filenames remain stable: `git-repository-guide.md`, `README.md`, and `CHANGELOG.md`.
- Standalone downloadable copies may use versioned filenames, such as `git-repository-guide-v1.3.0.md`.

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
