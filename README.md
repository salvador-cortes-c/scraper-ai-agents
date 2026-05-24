# Copilot Agents

Reusable GitHub Copilot agents and prompts for VS Code.

## Usage

**Per-repo** — copy the files you want into that repo's `.github/` folder:

```bash
cp .github/agents/pr-reviewer.agent.md your-repo/.github/agents/
cp .github/prompts/npm-security-fix.prompt.md your-repo/.github/prompts/
```

**Globally** — copy them to your VS Code user prompts folder to make them available in every workspace without touching each repo:

```bash
cp .github/agents/pr-reviewer.agent.md ~/.vscode-remote/data/User/prompts/
cp .github/prompts/npm-security-fix.prompt.md ~/.vscode-remote/data/User/prompts/
```

## Contents

| File | Type | Invoke | Description |
|------|------|--------|-------------|
| `.github/agents/pr-reviewer.agent.md` | Agent | `@PR Reviewer` | Peer-reviews open PRs for correctness, security, and test coverage. Read-only — never edits files or posts comments without confirmation. |
| `.github/prompts/npm-security-fix.prompt.md` | Prompt | `/npm-security-fix` | Interactive npm audit fix workflow: audits, asks approval, fixes, commits to a branch, and opens a PR. Never runs `--force` without explicit confirmation. |
