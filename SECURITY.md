# Security Policy

This policy applies to every repository in The Amplified Engineer organization that has no SECURITY.md of its own.

## Reporting a vulnerability

**Do not open a public GitHub issue for security vulnerabilities.**

Use one of:

- **Private vulnerability reporting**: open the Security tab of the affected repo and choose "Report a vulnerability".
- **Email**: **oss@mail.igorjs.io**

Include:

- Description of the vulnerability
- Steps to reproduce
- Affected versions
- Impact assessment (what can an attacker do?)
- Suggested fix, if you have one

### What to expect

- **Acknowledgement** within 48 hours
- **Assessment** within 7 days (severity, affected scope, fix plan)
- **Fix and disclosure** within 30 days for critical issues, 90 days for others

If the report is accepted, you will be credited in the release notes unless you prefer anonymity. If it is declined (not a vulnerability, or out of scope), you will receive an explanation and may open a public issue.

## Supported versions

Security fixes target the latest release of each repo. Earlier versions do not receive patches. Upgrade to the latest release before reporting.

## Scope

### In scope

Vulnerabilities in the code of any repo in the organization, including:

- Code execution, injection or memory safety issues
- Cryptographic weaknesses
- Authentication or authorization bypasses
- Denial of service through crafted input
- Bypass of any documented security guarantee (sandbox, isolation, hooks that guard commands)
- Compromise of the build, release or signing pipeline

### Out of scope

- Vulnerabilities in third-party dependencies (report them to the upstream maintainer)
- Issues that need an attacker who already has admin or write access to the repo
- Theoretical issues without a practical exploit path
- Social engineering
- Issues that need physical access to the user's machine
- Bugs in development-only tooling that does not ship to users

## Hardening posture

The repos follow a common posture: rulesets protect the default branch and release tags, commits are signed, and third-party actions are pinned by commit SHA.
