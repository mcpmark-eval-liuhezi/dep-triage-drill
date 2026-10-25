# Dependency Triage Drill

This repository is a **dependency-upgrade drill** for our quarterly security review. It documents an end-to-end demo of our dependency triage process, from vulnerable dependency detection through automated and human review.

## Scenario

- `package.json` pins `lodash` to **4.17.20**, a version with known published security advisories.
- `lodash` 4.17.20 is affected by multiple vulnerabilities, including:
  - **CVE-2020-8203** — prototype pollution in `zipObjectDeep` (fixed in 4.17.19 for that specific vector, but 4.17.20 remained flagged in several advisory feeds due to `merge`/`mergeWith` related prototype pollution reports).
  - **CVE-2021-23337** — command injection in `_.template` (fixed in 4.17.21).
- The patched release **4.17.21** resolves the outstanding advisories and is the target of this drill.

## Triage workflow demonstrated here

1. **Detect** — Dependabot (or a security scanner) flags `lodash@4.17.20` in the dependency manifest.
2. **Track** — open a tracking issue (`Upgrade lodash to a patched version`) describing the risk and remediation target.
3. **Remediate** — create a `chore/bump-lodash` branch that pins `lodash` to `4.17.21` and open a pull request into the default branch.
4. **Automated review** — request a Copilot code review on the pull request before any human reviewer sees it.
5. **Human review & merge** — a maintainer reviews the automated pass, approves, and merges.

## Notes

- This is a drill: the vulnerable pin is intentional and exists only to exercise the triage process.
- No production code depends on this repository.
