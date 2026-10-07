# Installing the Banger MCP server

Banger is a hosted, remote MCP server. There is nothing to clone, build, or run
locally, and no API key to paste: sign-in is OAuth in the browser.

- URL: `https://api.bangermail.com/mcp`
- Transport: Streamable HTTP
- Auth: OAuth 2.1 (PKCE, dynamic client registration). The client registers
  itself; no client ID or secret is needed.

## Cline

Add this entry to `cline_mcp_settings.json`, keeping any servers already there:

```json
{
  "mcpServers": {
    "banger": {
      "type": "streamableHttp",
      "url": "https://api.bangermail.com/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Or, in the Cline panel: MCP Servers → Remote Servers → add `banger` with the
URL above.

On the first tool call Cline opens Banger's authorization page in the browser.
The user signs in to Banger (or creates a free account), chooses the workspace,
and approves the scopes shown. Do not ask the user for a password, token, or
API key in chat.

## Verify

Call `banger_get_workspace`. It returns the workspace name and the caller's
role. Then `banger_onboarding_open_setup` starts or resumes Banger's guided
setup.

## Notes

- Leave `autoApprove` empty. Sends, Broadcasts, and Journey activations follow
  the workspace's approval policy, and the user should see each tool call.
- The only network endpoint is `https://api.bangermail.com` (MCP plus its OAuth
  and `/.well-known/*` metadata).
- More setup guides: https://bangermail.com/banger-mcp/
