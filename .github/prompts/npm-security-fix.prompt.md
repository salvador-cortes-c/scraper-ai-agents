---
description: "Audit npm dependencies in react-supermarket-purchase-helper for security vulnerabilities, apply fixes, commit to a new branch, push, and open a GitHub PR for review. Use when: npm audit, security vulnerabilities, CVE, npm fix, package vulnerabilities, dependency security."
mode: agent
tools: [execute, read, edit, github-pull-request/*]
---

Run an interactive npm security audit and fix workflow for the `react-supermarket-purchase-helper` Next.js project. Follow the steps below in order. Report findings after each step before proceeding.

## Step 1 — Audit

```bash
cd /workspaces/react-supermarket-purchase-helper && npm audit
```

Show the vulnerability summary (critical / high / moderate / low counts).

## Step 2 — Review

List each affected package, its severity, and whether `npm audit fix` can resolve it automatically or requires `--force`. Flag any that need `--force` separately.

## Step 3 — Get approval

Ask: **"Proceed with `npm audit fix`? (yes / no / show details)"**

Do not continue until the user confirms. If they say "show details", run `npm audit --json` and display a readable summary, then ask again.

## Step 4 — Fix

If approved, run:

```bash
cd /workspaces/react-supermarket-purchase-helper && npm audit fix
```

Never run `npm audit fix --force` unless the user explicitly says "use force". If `--force` is needed for remaining vulnerabilities, list them and ask separately.

## Step 5 — Verify

Run `npm audit` again. Confirm the vulnerability count decreased. If count is unchanged, report and stop — do not open a PR for a no-op fix.

## Step 6 — Commit and push

Only if vulnerabilities were fixed:

```bash
cd /workspaces
BRANCH="security/npm-audit-fix-$(date +%Y-%m-%d)"
git config user.name "github-actions[bot]"
git config user.email "github-actions[bot]@users.noreply.github.com"
git checkout -b "$BRANCH"
git add react-supermarket-purchase-helper/package.json \
        react-supermarket-purchase-helper/package-lock.json
git commit -m "fix(security): npm audit fix $(date +%Y-%m-%d)"
git push origin "$BRANCH"
```

Only stage `package.json` and `package-lock.json`. Do not stage any other files.

## Step 7 — Open PR

Use `github-pull-request_create_pull_request` with:
- **Title**: `fix(security): npm audit fix YYYY-MM-DD`
- **Body**: list each fixed package name, old version → new version, and severity
- **Base branch**: `main`
- **Head branch**: the branch created in step 6

Present the full PR details in chat before opening it and ask: **"Open this PR? (yes / no)"**
