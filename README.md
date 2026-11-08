# .github

Organization profile and default community health files for [The Amplified Engineer](https://github.com/amplifiedengineer).

## What is here

| Path | Purpose |
|---|---|
| `profile/README.md` | The landing page shown on the organization profile. |
| `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`, `SECURITY.md`, `SUPPORT.md` | Defaults GitHub shows for any organization repo that has no file of its own. |
| `.github/ISSUE_TEMPLATE/` | Default bug report and feature request forms. |
| `.github/PULL_REQUEST_TEMPLATE.md` | Default pull request template. |
| `.github/FUNDING.yml` | Default sponsor button. |
| `.github/workflows/` | CI for this repo, plus the reusable `cla-dco-checks.yml` that other repos call by commit. |
| `scripts/cla-check.sh` | The script behind the CLA and DCO checks, with offline tests. |
| `workflow-templates/` | Starter workflow for the CLA and DCO checks, offered to organization repos. |
| `docs/cla-and-dco.md` | How a contributor signs the CLA by commit, and how a repo adopts the checks. |

A repo that adds its own version of a file uses that file instead of the default here. Keep these files generic, and use absolute links, because relative links break when GitHub shows a default file in another repo.

## Changing it

Open a pull request. Commits are signed and carry a sign-off, the PR title follows Conventional Commits, and `main` is protected by rulesets.

## License

Apache-2.0. See [LICENSE](LICENSE).
