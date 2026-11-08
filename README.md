# VideoAmp MCP Server and CLI

Connect AI assistants and agents to VideoAmp using the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/getting-started/intro). The server exposes the [VideoAmp Public API](https://docs.videoamp.dev) as tools your assistant can call. If a CLI is preferred, see [VideoAmp CLI](#videoamp-cli) below.

There's nothing to install. Add the URL to your MCP client, sign in with your VideoAmp account, and start asking questions.

```
https://api.videoamp.dev/v1/mcp
```

## Connect your client

### Claude (claude.ai and Claude Desktop)

Custom connectors are available on Free (one connector), Pro, Max, Ultra, Team, and Enterprise plans.

**Individual plans**

1. Go to **Customize → Connectors**.
2. Select **+ Add → Add custom connector**.
3. Name it `VideoAmp` and enter the server URL above, then select **Continue**.
4. Select **Add**, then **Connect** and sign in to VideoAmp.

**Team and Enterprise plans**

1. An Owner adds the connector under **Organization settings → Connectors → Add → Custom → Web**, using the server URL above.
2. Members then go to **Customize → Connectors**, find the connector, and select **Connect** to sign in.

See Anthropic's guide to [custom connectors](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).

### Claude Code

```bash
claude mcp add --transport http videoamp https://api.videoamp.dev/v1/mcp
```

Start `claude`, run `/mcp`, select **videoamp**, and sign in. Add `--scope user` to use it in every project, or `--scope project` to share it with your team through `.mcp.json`.

### Cursor

Add to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project), then enable the server in Cursor and sign in:

```json
{
  "mcpServers": {
    "videoamp": { "url": "https://api.videoamp.dev/v1/mcp" }
  }
}
```

### VS Code (GitHub Copilot)

1. Open the Command Palette and run **MCP: Add Server**.
2. Choose **HTTP**, enter the server URL above, and name it `videoamp`.
3. Start the server and sign in when prompted.

To configure it by hand, add this to `.vscode/mcp.json`. Note that VS Code uses `servers` here, not `mcpServers`:

```json
{
  "servers": {
    "videoamp": { "type": "http", "url": "https://api.videoamp.dev/v1/mcp" }
  }
}
```

### Codex

```bash
codex mcp add videoamp --url https://api.videoamp.dev/v1/mcp
codex mcp login videoamp
```

### GitHub Codespaces

A ready-to-use environment with Copilot connected to the MCP server and the `videoamp` CLI installed. [Create a Codespace](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=894753956), then in Copilot choose **Agent** mode and a recent model. Requires a GitHub account with Copilot access.

### Other clients

Use the server URL with Streamable HTTP transport. If your client only supports local (stdio) servers, bridge with [`mcp-remote`](https://github.com/geelen/mcp-remote):

```json
{
  "mcpServers": {
    "videoamp": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://api.videoamp.dev/v1/mcp"]
    }
  }
}
```

## Try it

Once connected, try:

- "Get my VideoAmp user information."
- "List the VideoAmp audiences available to me."
- "Show me the tools I can use with VideoAmp."

## Authentication

The server uses OAuth. Your client opens a browser window, you sign in with your VideoAmp account, and the assistant acts with your existing VideoAmp permissions. No API keys are stored in your client configuration.

## Tools

Tools mostly follow a `<resource>_<action>` pattern, such as `audience_list` or `measurement_get`. A few examples:

| Area | Tools |
| --- | --- |
| **Account** | `user_info_get` |
| **Audiences** | `audience_list`, `audience_get` |
| **Measurement** | `measurement_list`, `measurement_get` |

Ask your assistant to list the tools available to you, or see the [API documentation](https://docs.videoamp.dev) for the full reference. Turn on your client's tool-approval setting so you can review calls before they run, especially tools that create, update, or delete data.

### `user_info_get`

Returns your profile and the organization your session is scoped to. Example response (abridged):

```json
{
  "id": "<user-uuid>",
  "given_name": "Ada",
  "family_name": "Lovelace",
  "email": "ada@example.com",
  "current_organization_id": "<org-uuid>"
}
```

### `audience_list`

Returns a paginated list of audiences. Filter by `statuses`, `classifications`, `ownership`, `useCases`, or `name`. Example response (abridged):

```json
{
  "total_size": 394,
  "results": [
    {
      "id": "5a1c26ae-e74a-419e-90ab-f18a692f2761",
      "name": "Demographic Person Hispanic Adults 18+",
      "classification": "GLOBAL_DEMOGRAPHIC",
      "ownership": "SYSTEM",
      "status": "READY",
      "use_cases": ["CONTENT_MEASUREMENT"]
    }
  ],
  "next_page_token": "…"
}
```

## Troubleshooting

**The connector won't add in Claude.** On Team and Enterprise plans, an Owner must add the connector to the organization before members can connect.

**Connection fails from a local client.** If your device or network is managed, ask your IT team to allow `api.videoamp.dev`. Claude's connectors connect from Anthropic's cloud rather than your machine, so this applies to clients like Claude Code, Cursor, VS Code, and Codex.

**Sign-in loop or stale session.** Disconnect the server in your client's MCP settings, then reconnect. If you use the `mcp-remote` bridge, clear its saved auth with `rm -rf ~/.mcp-auth` and try again.

**Client doesn't support remote servers.** Use the `mcp-remote` bridge under [Other clients](#other-clients).

Still stuck? Open an [issue](https://github.com/VideoAmp/cli/issues) or see the [API documentation](https://docs.videoamp.dev).

---

## VideoAmp CLI

The same tools are available from a terminal or automated process through the `videoamp` executable, which can also run the MCP server locally with `videoamp mcp`.

1. Download the asset for your OS and CPU from the [releases page](https://github.com/VideoAmp/cli/releases), for example `videoamp_<version>_darwin_arm64.tar.gz`.
2. Install it.

   **macOS / Linux**

   ```bash
   tar -xzf videoamp_<version>_<os>_<arch>.tar.gz
   sudo mv videoamp /usr/local/bin/
   chmod +x /usr/local/bin/videoamp
   ```

   **Windows (PowerShell)**

   ```powershell
   Expand-Archive -Path .\videoamp_<version>_windows_amd64.zip -DestinationPath .
   Move-Item -Path .\videoamp.exe -Destination $env:USERPROFILE\AppData\Local\Microsoft\WindowsApps\videoamp.exe
   ```

3. Verify:

   ```bash
   videoamp --help
   ```