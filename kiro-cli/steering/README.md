# Kiro CLI Steering (Global)

This folder contains global steering files intended for `~/.kiro/steering/`. Steering files give Kiro persistent project knowledge so you do not have to repeat conventions in every chat, and they make responses more consistent and task-focused.

This project exists because AI tools often lose track of how they themselves are configured: where settings live, which MCPs are enabled, and which CLIs or integrations you rely on most. Steering files keep those reminders close at hand, so the AI stays aligned with your preferred connections and workflows. You can also use simple, consistent keywords in the files to shape behavior without long prompts.

## How Steering Works (Kiro CLI)

- **Scope:** Steering files can be workspace-scoped (`.kiro/steering/` in a project) or global (`~/.kiro/steering/`).
- **Precedence:** Workspace steering overrides global steering when instructions conflict.
- **Always-included:** `AGENTS.md` files are always included. They can live in the workspace root or in `~/.kiro/steering/`.
- **Foundational files:** Kiro automatically loads `product.md`, `structure.md`, and `tech.md` when present.
- **Custom files:** Any `.md` file in the steering directory is available to Kiro for guidance.
- **File references:** You can reference project files with `#[[file:path/to/file]]`.

## Files In This Folder

- `aws-cli.md` - Standardizes AWS CLI usage and credential handling.
- `atlassian-mcp.md` - Sets up hosted Atlassian MCP usage (Jira/Confluence).
- `github-cli.md` - Safe, repeatable GitHub CLI (`gh`) workflows.
- `kiro-configuration.md` - Kiro config paths and debug references.

## How These Files Help (Examples)

The goal is to make Kiro answer with your preferred tools and guardrails by default, without extra prompting.

### AWS CLI Steering Example

**You ask:** "List S3 buckets in my account."

**Kiro behavior shaped by `aws-cli.md`:**
- Uses `aws` commands (not SDKs or MCP servers).
- Prompts only for access keys if missing.
- Runs a connectivity check like `aws sts get-caller-identity` if auth fails.

### GitHub CLI Steering Example

**You ask:** "Open a PR from my branch."

**Kiro behavior shaped by `github-cli.md`:**
- Uses `gh pr create` with explicit flags.
- Avoids interactive prompts.
- Avoids force pushes or risky actions without confirmation.

### Atlassian MCP Steering Example

**You ask:** "Create a Jira ticket and link a Confluence page."

**Kiro behavior shaped by `atlassian-mcp.md`:**
- Uses the hosted Atlassian MCP endpoint only.
- Initiates OAuth if needed.
- Avoids asking you to install extra MCP servers.

### Kiro Configuration Example

**You ask:** "Where do I put MCP config for Kiro?"

**Kiro behavior shaped by `kiro-configuration.md`:**
- Points to `~/.kiro/settings/mcp.json` and `.kiro/settings/mcp.json`.
- Explains how `mcpServers` should be structured.

## Install (Global Steering)

Copy these files into your global steering directory:

```bash
mkdir -p ~/.kiro/steering
cp -a kiro-cli/steering/*.md ~/.kiro/steering/
```

## Best Practices

- Keep files focused on one domain (auth, API patterns, testing, deployment).
- Explain the "why" behind conventions, not only the "what."
- Include examples and file references where useful.
- Never include secrets or credentials in steering files.

## References

- Steering (CLI): https://kiro.dev/docs/cli/steering/
