# CLA and DCO checks

A contributor signs the CLA by adding a row to `.github/CONTRIBUTORS.md` in a commit they author. The commit stays in the repository history, so the record moves with the repository to any Git host. No bot writes it, and no GitHub label or setting holds it.

This repository holds the shared version for every repository in the organization.

## Parts

- `.github/workflows/cla-dco-checks.yml` is the reusable workflow. It has two jobs, `dco` and `cla-check`. It runs on plain `pull_request` with read-only permissions and no secret, and it checks out with `persist-credentials: false`.
- `scripts/cla-check.sh` makes both decisions from git history. `scripts/cla-check.test.sh` tests it on throwaway repositories, and `.github/workflows/cla-check-tests.yml` runs those tests.
- `workflow-templates/cla-dco.yml` is the starter workflow offered to the organization's repositories.
- `.github/workflows/cla-dco.yml` is this repository's own caller.

The caller job is named `cla-dco`, so the required checks read `cla-dco / dco` and `cla-dco / cla-check` in every repository.

## Use it in a repository

1. Copy `.github/CONTRIBUTORS.md`, `ICLA.md` and `CCLA.md` into the repository's `.github` folder, and keep the existing signature rows.
2. Add `workflow-templates/cla-dco.yml` as `.github/workflows/cla-dco.yml`. Replace `COMMIT_SHA` twice with one commit SHA of this repository that contains the workflow. The first sets the workflow version, and the second makes the workflow fetch `scripts/cla-check.sh` at that same commit, so a pull request cannot change the checker it runs under.
3. Require the checks `cla-dco / dco` and `cla-dco / cla-check`.

Inputs of the reusable workflow: `signatures-file`, `cla-path`, `statement`, `extra-bots`, `script`, `tooling-repository` and `tooling-ref`. With no `tooling-ref`, the script is read from the caller repository at `scripts/cla-check.sh`, which is how this repository and the project template run it.

## What `cla-check` verifies

1. The register on the default branch lists the people who already signed.
2. The pull request author and every non-bot commit author in `base..head` must be on that list, or sign in this pull request.
3. A pull request signs for someone only when a row it adds is introduced by a commit authored by that same person, and that commit message holds the sentence `I have read the CLA Document and I hereby sign the CLA.` Case and line wraps do not matter.
4. A pull request may not edit or remove an existing row.

A person matches a row by login, by email, or by the account id inside a GitHub noreply address, which survives a login rename. Bots, merge commits and `Co-authored-by` trailers are not checked. Maintainers sign like everyone else. An agent commits as its owner, so the owner's row covers it.

## Rollout for existing repositories

Switching a repository to this workflow keeps all existing rows, so every listed contributor passes with no action. The check names do not change, so rulesets keep working. A pull request opened earlier keeps its old check run until its next push.

## Limits

A pull request that edits the workflow runs its own copy of it. Setting `tooling-ref` pins the script, but the caller workflow still lives in the repository, so code owner review of `.github/` is the control there.
