# Contributing

This repository is the traceable record of our diploma project. The committee checks **who did what, when, and how it was reviewed**.

## Rules

1. **Own account only.** Each member commits from their own GitHub account with their real name and AITU email in `git config user.name` / `user.email`. No shared accounts.
2. **One Notion task (ID `DIP-<n>`) per meaningful work item.** The task states the responsible student, expected outcome, acceptance criteria and deadline.
3. **Branch per task:** `feature/DIP-<id>-short-name`, e.g. `feature/DIP-7-literature-review`.
4. **Commit messages:** `DIP-<id>: <what changed>` in the imperative, e.g. `DIP-7: Add 4 sources on RAG-based test generation`. One coherent change per commit.
5. **Pull request for every change** to `main`, using the template. Another team member reviews and approves before merge. The reviewer leaves real comments; the author answers them with commits.
6. **Link back:** paste the PR link into the "PR link" field of the Notion task and set Status to Done. Close the task only when its acceptance criteria are met.
7. **No secrets or personal data** in the repository. Interview notes are anonymised (P1, P2, …); consent forms stay outside Git.
8. **Diagrams:** commit the editable source (`diagrams/src/*.puml`) together with the export (`diagrams/export/*.svg`).
9. **Tags:** `pre-defense-1`, `pre-defense-2`, `final-pre-defense`. Never move or delete a tag.

## Branch protection on `main` (set by the repository owner)

- Require a pull request before merging, 1 approval, dismiss stale approvals.
- Require conversation resolution before merging.
- Block force pushes and deletions.
- Add the supervisor (and the committee before each pre-defense) as collaborators with read access.

## Example

| Item | Value |
|---|---|
| Task | DIP-12 — Draw use case diagram |
| Branch | `feature/DIP-12-use-case-diagram` |
| Commit | `DIP-12: Add use case diagram source and SVG export` |
| PR title | `DIP-12: Use case diagram` |
