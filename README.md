# VideoAmp Tools

VideoAmp Tools includes both the VideoAmp MCP Server and CLI. All are intended to streamline workflows and integrations with VideoAmp's APIs. Detailed API specs can be found at https://docs.videoamp.dev.

---

## Copilot + Codespace (zero install)

This option provides a ready-to-use development environment in the cloud via GitHub Codespaces, allowing interaction with VideoAmp tools through GitHub Copilot without needing any local installation.

1. Create a [GitHub Codespace](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=894753956).
2. In Copilot, select mode `Agent` and a recent model, e.g., `Claude Sonnet 4.5`, `Chat GPT-5`.

   ![Copilot Agent Mode](https://github.com/user-attachments/assets/1673af7b-2642-4c12-9ebc-60413b852ffa)

3. Ask Copilot, "What VideoAmp tools can I use?" or "Show questions I can ask VideoAmp."

### Details

```mermaid
graph LR
    subgraph Cloud [GitHub Codespace Container]
        Copilot[GitHub Copilot Agent Mode]
        MCPServer[videoamp mcp start-server --transport stdio]
        ConfigFile[~/.videoamp/config.yaml]

        Copilot -- stdio --> MCPServer
        MCPServer -- reads --> ConfigFile
    end

    User--> Copilot
    MCPServer -- HTTP/gRPC --> VideoAmpAPI[VideoAmp Public API]
```

**Client Location:** GitHub Codespace

**Server Location:** GitHub Codespace

**Authentication:** If needed, run `videoamp login` within the Codespace terminal (login may occur automatically). The MCP server (using stdio transport) reads the stored access token from its configuration file within the Codespace environment to authenticate subsequent API calls made by tools.

### Prerequisites 

* Requires a GitHub account
* Relies on GitHub Copilot

---

## Claude Desktop (local install)

### Mac(apple silicon)
1. Download [VideoAmp-MCP-darwin-arm64.mcpb](https://github.com/VideoAmp/cli/releases/download/v0.43.1/VideoAmp-MCP-darwin-arm64.mcpb).
2. Double-click the downloaded file.
3. Click Install.

   ![Claude Desktop Install](https://github.com/user-attachments/assets/b57340e2-11b5-44eb-9a43-cbe1b22eaa28)

4. Ask Claude, "What VideoAmp tools can I use?" or "Show questions I can ask VideoAmp."

### Windows

1. Coming soon.

### Details

```mermaid
graph LR
    subgraph UserMachine [User's Local Machine]
        ClaudeDesktop[Claude Desktop App]
        MCPServer[videoamp mcp start-server --transport stdio]
        ConfigFile[~/.videoamp/config.yaml]

        ClaudeDesktop -- launches & stdio comms --> MCPServer
        MCPServer -- reads --> ConfigFile
    end

    User --> ClaudeDesktop
    MCPServer -- HTTP/gRPC --> VideoAmpAPI[VideoAmp Public API]
```

**Client Location:** Anthropic's Claude Desktop application running on the user's local machine.

**Server Location:** The `videoamp mcp start-server --transport stdio` process runs locally on the user's machine, launched by Claude Desktop.

**Authentication:** Relies on the user having previously logged in via the `videoamp login` command in their terminal. The locally running MCP server (using stdio transport) reads the stored access token from the user's local CLI configuration file to authenticate API calls.

### Prerequisites

* Requires installing Claude Desktop.
* Requires downloading and installing the appropriate .mcpb file.
* Requires the user to manage their VideoAmp CLI login state separately via a terminal.
* The MCP server process runs locally, so ensuring the correct version is the user's responsibility.
* Only available for macOS (Apple Silicon) initially, Windows "coming soon".

---

## Claude.ai (remote MCP) (WIP)

This option would allow users to interact with VideoAmp tools directly from the Claude.ai web interface by connecting to a remotely hosted VideoAmp MCP server. Does not exist yet, but is coming soon.

### Details

```mermaid
graph LR
    subgraph UserBrowser [User's Browser]
        ClaudeAI[Claude.ai Web App]
    end

    subgraph RemoteInfra [Remote Infrastructure]
        MCPServer[videoamp mcp start-server --transport http]
    end

    User --> ClaudeAI
    ClaudeAI -- HTTP MCP Request (Auth?) --> MCPServer
    MCPServer -- HTTP/gRPC --> VideoAmpAPI[VideoAmp Public API]
```

**Client Location:** The Claude.ai web application running in the user's browser.

**Server Location:** Remote server hosted at `https://api.videoamp.dev`

**Authentication:** TBD

### Prerequisites

* Requires a stable, remotely hosted, and accessible MCP server instance (i.e., setup, maintenance, potential costs, and security considerations).
* Depends on Anthropic's implementation within Claude.ai for MCP connectivity and secure token management.
* May require a paid Claude.ai subscription.

---

## General CLI Installation

This option describes how to install the videoamp executable locally for direct use from a command line terminal.

1. Visit the [releases page](https://github.com/VideoAmp/cli/releases) and download the asset that matches your OS and CPU architecture (for example, `videoamp_v0.10.0_linux_amd64.tar.gz`, `videoamp_v0.10.0_darwin_arm64.tar.gz`, or `videoamp_v0.10.0_windows_amd64.zip`).

2. Extract the archive and move the `videoamp` executable somewhere on your `$PATH`:

   **macOS/Linux:**
   
   ```bash
   tar -xzf videoamp_<version>_<os>_<arch>.tar.gz
   sudo mv videoamp /usr/local/bin/
   chmod +x /usr/local/bin/videoamp
   ```

   **Windows (PowerShell):**
   
   ```powershell
   Expand-Archive -Path .\videoamp_<version>_windows_amd64.zip -DestinationPath .
   Move-Item -Path .\videoamp.exe -Destination $env:USERPROFILE\AppData\Local\Microsoft\WindowsApps\videoamp.exe
   ```

3. Confirm the installation:

   ```bash
   videoamp --help
   ```

### Details

```mermaid
graph LR
    User[User / Script] -- runs --> CLI[videoamp CLI]
    CLI -- HTTP/gRPC --> VideoAmpAPI[VideoAmp Public API]
```

**Client Location:** The user's terminal or an automation script running on the user's machine.

**Server Location:** N/A - CLI communicates directly with VideoAmp APIs.

**Authentication:** User runs `videoamp login` in the terminal. The CLI manages the `access_token` in ~/.videoamp/config.yaml.

---
