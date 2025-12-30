# GitHub CLI Steering

Purpose: Standardize safe, repeatable GitHub CLI usage.

## General Rules
- Prefer `gh` for GitHub operations over direct API calls.
- Do NOT use MCP or GitHub keys unless explicitly asked.
- Assume GitHub CLI is the default interface for GitHub tasks.
- You may run bash commands directly to complete tasks; do not ask the user to run them unless necessary.
- Use explicit flags; avoid interactive prompts in automation.
- Keep output readable; use `--json` + `jq` for structured data when needed.
- Never print or log tokens or secrets.

## Auth
- Use `gh auth status` to confirm authentication.
- The authenticated user may have access to multiple GitHub organizations via their CLI login; use `gh auth status` and repo visibility to verify access.
- If auth fails, help resolve it via `gh auth login` and confirm success.
- Document the method used (browser, token, SSH) when troubleshooting.

## Repos
- Clone with `gh repo clone owner/name`.
- View repo metadata with `gh repo view owner/name`.

## Issues
- List: `gh issue list` with labels/milestones as filters.
- View: `gh issue view <id> --comments`.
- Create/update with clear titles and concise bodies.

## Pull Requests
- Create: `gh pr create --title --body --base --head`.
- View: `gh pr view <id> --comments`.
- Review: `gh pr review <id> --approve|--request-changes --body`.
- Merge: `gh pr merge <id> --squash|--merge|--rebase` (choose explicitly).

## Safety
- Confirm the target repo/branch before destructive actions.
- Avoid force pushes unless explicitly approved.
- For bulk actions, run a dry-run or list targets first.
