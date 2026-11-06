# Contributing

Thank you for helping. This page applies to every pragmatic-engineer repo that has no CONTRIBUTING.md of its own. If a repo has one, follow that file first.

## Before you start

1. Search the existing issues to see if someone already works on it.
2. Open an issue first for significant changes such as new modules, API changes or architecture. Small fixes and documentation changes can go straight to a pull request.
3. Read the [Code of Conduct](https://github.com/pragmatic-engineer/.github/blob/main/CODE_OF_CONDUCT.md).

## Commits and pull requests

- Sign every commit (`git commit -S`) and add a sign-off (`git commit -s`). The sign-off certifies the [Developer Certificate of Origin](https://developercertificate.org/).
- Write the PR title as a [Conventional Commit](https://www.conventionalcommits.org/), 72 characters at most. Allowed types: feat, fix, docs, style, refactor, perf, test, chore, ci, build, revert. The repos squash merge, so the title becomes the commit message on `main`.
- Keep a PR focused on one change and link the issue it closes.
- Fill in the pull request template.
- Write the description yourself and be ready to explain every change.
- Some repos also require a contributor license agreement. The PR will tell you if yours does. Where one is required, you sign by adding your own row to `.github/CONTRIBUTORS.md` in a commit you author, with the sentence `I have read the CLA Document and I hereby sign the CLA.` in its message. See [the CLA and DCO notes](https://github.com/pragmatic-engineer/.github/blob/main/docs/cla-and-dco.md).

## Checks

Pull requests run the repo's CI. The usual checks are the PR title lint, a secret scan and a dependency review. A PR merges after the required checks pass and every review thread is resolved. Never skip hooks or checks with `--no-verify`.

## Security

Report vulnerabilities privately. See the [security policy](https://github.com/pragmatic-engineer/.github/blob/main/SECURITY.md).

## License

Contributions are licensed under the license of the repo you contribute to, which is Apache-2.0 for the pragmatic-engineer projects.
