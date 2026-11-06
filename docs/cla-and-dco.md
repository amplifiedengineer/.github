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

Inputs of the reusable workflow: `signatures-file`, `cla-path`, `statement`, `extra-bots`, `ignored-coauthors`, `extra-ignored-coauthors`, `script`, `tooling-repository` and `tooling-ref`. With no `tooling-ref`, the script is read from the caller repository at `scripts/cla-check.sh`, which is how this repository and the project template run it.

## What `cla-check` verifies

1. The register on the default branch lists the people who already signed.
2. The pull request author and every non-bot commit author in `base..head` must be on that list, or sign in this pull request.
3. Only the pull request author can sign in a pull request: the row must be for the author's login (or account id), the commit that adds it must be authored by that person (host login, noreply address, or the very email on the row), and that commit message holds the sentence `I have read the CLA Document and I hereby sign the CLA.` Case and line wraps do not matter.
4. A pull request may not edit or remove an existing row.

A person matches a row by login, by email, or by the account id inside a GitHub noreply address, which survives a login rename (the pull request author is matched by account id from GitHub). Others who need to sign, such as co-authors, sign in their own pull request. A bot is a commit whose GitHub account is of type Bot; the git name and email are not trusted for that when GitHub answered. A commit that GitHub did not list (past 250 commits) is not treated as a bot. Merge commits are skipped. Maintainers sign like everyone else. An agent commits as its owner, so the owner's row covers it.

## Co-authors

Every line that starts with `Co-authored-by:` in any pull request commit (key in any case, many per commit, bot-authored commits included) names a person who must be signed, matched by email or by the account id or login in a noreply address. The same person as a commit author is checked once, as an author. A co-author who is not on the default branch list, and has not signed in their own pull request first, fails the check. The message names the person and says that they add a row in a commit they author. They sign in their own pull request, which must merge first.

A trailer that is not `Name <email>` fails closed with a clear message, even when it names an AI tool.

AI tools and bots are ignored by email address only. The display name is never used, because anyone can write any name in a trailer, so a person named Claude is still checked. The built-in list is `[bot]` (a GitHub App address), `noreply@anthropic.com`, `noreply@github.com`, `noreply@openai.com`, `noreply@aider.chat`, `cursoragent@cursor.com` and the suffix `+copilot@users.noreply.github.com`. A pattern is one of: `[bot]`, a suffix that starts with `@` or `+`, an exact address, or a bare domain. A human is always named by their own address, so skipping a vendor address never skips a person.

To add tools, set the `extra-ignored-coauthors` input (comma separated). To replace the whole list, set `ignored-coauthors`.

## Rollout for existing repositories

Switching a repository to this workflow keeps all existing rows, so every listed contributor passes with no action. The check names do not change, so rulesets keep working. A pull request opened earlier keeps its old check run until its next push.

## Limits

A pull request that edits the workflow runs its own copy of it. Setting `tooling-ref` pins the script, but the caller workflow still lives in the repository, so code owner review is the control there. `CODEOWNERS` lists `* @igorjs`, which covers `.github/` and `scripts/`, but it only blocks a merge when the ruleset requires code owner review. Unlike a comment-triggered flow, a pull request from a fork cannot read secrets here.

The author name and email of a commit are free text, so git history alone cannot prove who wrote a commit. The check binds a signature to the authenticated pull request author, which a commit cannot fake, and treats other attribution as a declaration.
