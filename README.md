# VideoAmp Tools

VideoAmp Tools are available via an MCP or CLI interface and expose the same capabilities available in the [VideoAmp Public API](https://docs.videoamp.dev). The use of tools are intended to streamline workflows and integrations with the APIs. 

---

# MCP Getting Started

AI assistants, agents and chatbots compatible with the [MCP protocol](https://modelcontextprotocol.io/docs/getting-started/intro) may use the tools via the remote MCP server at `https://api.videoamp.dev/v1/mcp`.

After connecting with one of the [MCP Configuration Options](#mcp-configuration-options), try a simple prompt like:

* "Show me tools I can use with VideoAmp."
* "List VideoAmp audiences available to me."
* "Help me understand VideoAmp capabilities."
* "Get my VideoAmp user information."

---

# MCP Configuration Options

## Claude Desktop with Remote Server
This option enables use of the remote MCP server via Claude Desktop and does not require local installation of the MCP server.

1. Open Claude Desktop and list available connectors using `Manage Connectors`.
2. Connect to `VideoAmp MCP`.

### Prerequisites
* [Claude Desktop](https://claude.com/download)
* The remote server at `https://api.videoamp.dev/v1/mcp` has been added as a [Custom Connector](https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp) and named `VideoAmp MCP`. Admin privileges may be required.
* Pro, Max, Team, or Enterprise license

---

## Claude.ai with Remote Server
This option enables use of the remote MCP server via [Claude.ai](https://claude.ai) and does not require local installation of the MCP server.

1. Open [Claude.ai](https://claude.ai) and list available connectors using `Manage Connectors`.
2. Connect to `VideoAmp MCP`.

### Prerequisites
* The remote server at `https://api.videoamp.dev/v1/mcp` has been added as a [Custom Connector](https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp) and named VideoAmp MCP. Admin privileges may be required.
* Pro, Max, Team, or Enterprise license

---

## Claude Code with Remote Server
This option enables use of the remote MCP server through Claude Code and does not require local installation of the MCP server.

1. Add the MCP server from the terminal using
```bash
claude mcp add --transport http VideoAmp https://api.videoamp.dev/v1/mcp
```
2. Start `claude` from a terminal and use `/mcp` to find and connect to `VideoAmp`.

### Prerequisites
* [Claude Code](https://claude.com/product/claude-code)

---

## Codespace with Remote Server
This option provides a complete development environment using Copilot connected to the remote MCP server. No additional installation is required.  This options also provides CLI tool access using `videoamp` from a terminal.

1. Create a [GitHub Codespace](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=894753956).
2. In Copilot, select mode `Agent` and a recent model, e.g., `Claude Sonnet 4.5`, `Chat GPT-5`.

   <img src="https://github.com/user-attachments/assets/1673af7b-2642-4c12-9ebc-60413b852ffa" alt="Copilot Agent Mode" width="400">

### Prerequisites
* GitHub account
* GitHub Copilot access

---

## CLI Installation

This option provides the `videoamp` executable for local installation and use from a terminal or automated process.  Additionally this allows the MCP server to be run locally using the `videoamp mcp` CLI interface.

1. Visit the [releases page](https://github.com/VideoAmp/cli/releases) and download the asset that matches your OS and CPU architecture (for example, `videoamp_v0.43.1_linux_amd64.tar.gz`, `videoamp_v0.43.1_darwin_arm64.tar.gz`, or `videoamp_v0.43.1_windows_amd64.zip`).

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

---
