# Banger plugin

All your company email, operated by agents and reviewed by you.

This one directory is the Banger plugin for every agent host that reads the
open plugin layout: **Claude Code and Claude Cowork** (`.claude-plugin/`),
**Grok Build / Grok Bot** (`.grok-plugin/`), and **ChatGPT / Codex**
(`.codex-plugin/`). Each host reads its own manifest; they all share the same
skill and the same hosted MCP server.

## What it ships

- **MCP server** `banger` at `https://api.bangermail.com/mcp` (Streamable HTTP,
  OAuth 2.1 with PKCE and dynamic client registration). Declared in
  [`.mcp.json`](./.mcp.json). The registry descriptor is
  [`server.json`](./server.json) (`com.bangermail/banger`).
- **Skill** `operate-company-email`: how to onboard a workspace, configure a
  company domain safely, turn business context into a reviewable email growth
  plan, and operate Mailboxes, Journeys, Broadcast, Product email, Approvals,
  and Logs with evidence.

No hooks, no local processes, no shell commands. Nothing runs on your machine;
the plugin only points your agent at the hosted server and teaches it how to
use it.

## Install

Claude Code:

```bash
claude plugin marketplace add bangermail/banger-plugin
claude plugin install banger@banger
```

Grok Build / Grok Bot:

```bash
grok plugin install bangermail/banger-plugin --trust
```

Codex: install **Banger** from the Codex plugin directory, or add the server
directly:

```bash
codex mcp add banger --url https://api.bangermail.com/mcp
codex mcp login banger
```

Claude Cowork and ChatGPT install Banger from their plugin directories once it
is listed there.

On first use the host opens Banger's authorization page. Sign in, choose the
workspace, and approve the scope set shown. Banger never asks for credentials
in chat.

## Network and data

- The only endpoint the plugin talks to is `https://api.bangermail.com`
  (MCP over HTTPS plus its OAuth endpoints under `/oauth/*` and
  `/.well-known/*`).
- Authentication is a per-workspace OAuth grant issued to your agent. Revoke it
  from the Banger app at any time.
- Governed actions (sending, launching a Broadcast, activating a Journey) honor
  the workspace approval policy; the agent cannot bypass a required approval.

## Links

- Product: https://bangermail.com/banger-mcp/
- Privacy: https://bangermail.com/privacy/
- Terms: https://bangermail.com/terms/
- Support: hello@team.bangermail.com

## License

Proprietary; see [LICENSE](LICENSE). Copyright BangerMail Inc. Use of the hosted service is governed by
the Banger Terms of Service.
