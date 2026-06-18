---
name: npm-audit-react
description: Handles npm audit findings in React web applications. Use when npm audit reports vulnerabilities, when dependency upgrades create React build/test risk, or when you need to safely triage and fix frontend package security issues.
---

# NPM Audit for React Apps

Use this skill to triage and fix `npm audit` issues without blindly forcing breaking dependency updates.

## Current Audit

!`npm audit || true`

## Workflow

1. Read the audit output above first; do not rerun unless it is missing, stale, or not JSON.
2. Group findings by vulnerable package, severity, direct vs transitive dependency, and whether a fix is available.
3. Prefer the smallest safe fix:
   - patch/minor direct dependency updates first
   - package-manager overrides/resolutions for transitive-only issues when appropriate
   - major upgrades only after checking changelogs and React/framework compatibility
4. Do not use `npm audit fix --force` unless the user explicitly approves the breaking changes.
5. After changes, run the project’s relevant checks: install/lockfile update, `npm audit`, tests, typecheck, lint, and build where available.
6. Report what changed, remaining vulnerabilities, and any risk the user must accept.

## React-Specific Guardrails

- Protect React, React DOM, bundler, router, testing-library, and framework major versions from accidental upgrades.
- If the app uses Next.js, Vite, CRA, Astro, Remix, or React Router, verify the security fix against that framework’s supported dependency ranges.
- Treat devDependency vulnerabilities as lower deployment risk, but still fix them when a safe patch exists.

## Output

Return a concise summary with:

- vulnerability groups and severity
- exact package changes made
- verification commands and results
- any remaining findings and why they remain
