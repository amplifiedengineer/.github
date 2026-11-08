# amplifiedengineer

> **Renamed.** This organization was `pragmatic-engineer`. It is now `amplifiedengineer`. GitHub redirects the old addresses, but do not rely on that. If you installed Playbook before the rename, remove the old install and install again. Your data stays in `~/.config/playbook`.
>
> - **Homebrew:** `brew uninstall playbook`, then `brew untap pragmatic-engineer/tap`, then `brew install amplifiedengineer/tap/playbook`.
> - **Nix:** `nix profile remove playbook`, then `nix profile install github:amplifiedengineer/nix#playbook`.
> - **Claude Code plugin:** `claude plugin marketplace remove pragmatic-engineer`, then `claude plugin marketplace add amplifiedengineer/marketplace`, then `claude plugin install playbook@pragmatic-engineer`. The marketplace name stays `pragmatic-engineer`.
> - **Install script:** run it again from the new address, shown below.

We build tools for engineering with AI help. Our main project is Playbook, a toolkit for Claude Code. It adds skills, slash commands and subagents for planning, review and memory, plus a small `playbook` binary that runs safety guards and hooks.

## Repos

| Repo | What it does |
|---|---|
| [playbook](https://github.com/amplifiedengineer/playbook) | The Claude Code plugin, the `playbook` binary, the `pbtop` cost dashboard and the docs. |
| [marketplace](https://github.com/amplifiedengineer/marketplace) | The Claude Code plugin marketplace that lists the playbook plugin. |
| [homebrew-tap](https://github.com/amplifiedengineer/homebrew-tap) | Homebrew formulas for `playbook` and `pbtop`. |
| [nix](https://github.com/amplifiedengineer/nix) | Nix flake for `playbook` and `pbtop`. |
| [helios](https://github.com/amplifiedengineer/helios) | A terminal client for reviewing pull requests. Work in progress, with no release yet. |
| [.github](https://github.com/amplifiedengineer/.github) | This profile and the default community files. |

## Install Playbook

Homebrew:

```sh
brew install amplifiedengineer/tap/playbook
playbook setup
```

Install script, if you have no Homebrew:

```sh
curl -fsSL https://raw.githubusercontent.com/amplifiedengineer/playbook/main/install.sh | bash
```

Nix:

```sh
nix profile install github:amplifiedengineer/nix#playbook
```

Claude Code plugin only, with no binary or hooks:

```sh
claude plugin marketplace add amplifiedengineer/marketplace
claude plugin install playbook@pragmatic-engineer
```

The marketplace name is still `pragmatic-engineer` from before the rename, so the plugin id keeps that name.

Read the [playbook README](https://github.com/amplifiedengineer/playbook#readme) and the [docs](https://github.com/amplifiedengineer/playbook/blob/main/docs/README.md) to get started.

## Community

Read the [contributing guide](https://github.com/amplifiedengineer/.github/blob/main/CONTRIBUTING.md), the [security policy](https://github.com/amplifiedengineer/.github/blob/main/SECURITY.md) and the [support page](https://github.com/amplifiedengineer/.github/blob/main/SUPPORT.md).
