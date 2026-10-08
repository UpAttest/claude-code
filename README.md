# UpAttest for Claude Code

A Claude Code plugin marketplace with one plugin, `upattest`. It gives Claude Code:

- **The UpAttest MCP server** (hosted, Streamable HTTP, browser sign-in; no key to copy).
- **`request-human-attestation`**, a skill that teaches the agent when a human sign-off is worth suggesting
  (security-sensitive diffs, licensed-domain outputs such as structural calculations, legal, financial or medical
  content), how to choose an attestation type, how to stay inside the owner's spending limits, and how to read
  the findings.
- **Slash commands**: `/upattest:upattest-review [focus] [max $]`, `/upattest:upattest-status`,
  `/upattest:upattest-verify [file | sha256 | att_id]` (also available as `/upattest-review` etc. when no other
  command uses the name).

## Install

```
claude plugin marketplace add upattest/claude-code
claude plugin install upattest@upattest
```

Or inside a session: `/plugin install upattest --marketplace upattest/claude-code`.

Then run `/mcp`, choose `plugin:upattest:upattest` and sign in through your browser. Ask:

> Run upattest_check_connection and tell me which UpAttest account, environment and permissions you are connected with.

Private preview: start Claude Code with `UPATTEST_MCP_URL=https://api-sandbox.upattest.com/mcp` to use the sandbox
(simulated payments, fictional reviewers). Production is `https://api.upattest.com/mcp`, the default.

### Without a browser (CI, headless)

Use the local stdio server with a scoped key instead of the plugin's hosted server. In the project's `.mcp.json`
(the key is expanded from the environment, so the file holds no secret):

```json
{ "mcpServers": { "upattest": { "command": "npx", "args": ["-y", "@upattest/mcp"], "env": { "UPATTEST_API_KEY": "${UPATTEST_API_KEY}" } } } }
```

Keep the key in your shell's secret store, never in a committed file or a prompt.

## Layout

```
.claude-plugin/marketplace.json            marketplace "upattest" (one entry, source ./plugins/upattest)
plugins/upattest/.claude-plugin/plugin.json
plugins/upattest/.mcp.json                 hosted server; URL overridable with UPATTEST_MCP_URL
plugins/upattest/skills/request-human-attestation/SKILL.md
plugins/upattest/skills/upattest-review/SKILL.md
plugins/upattest/skills/upattest-status/SKILL.md
plugins/upattest/skills/upattest-verify/SKILL.md
plugins/upattest/assets/icon.png           directory listing icon
```

## Check before publishing

```
claude plugin validate --strict ./plugins/upattest
claude plugin validate --strict .
```

Both pass on Claude Code 2.1.291 (7 October 2026). Format: <https://code.claude.com/docs/en/plugins-reference>,
<https://code.claude.com/docs/en/plugin-marketplaces>, <https://code.claude.com/docs/en/plugins/publish> (read
7 October 2026). Publishing steps and status are in `docs/89-growth-distribution.md`.

The `request-human-attestation` skill is shared word for word with `integrations/codex/`; a test keeps the copies
identical.
