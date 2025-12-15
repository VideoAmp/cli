# VideoAmp Tools

VideoAmp tools are available via an MCP or CLI interface and expose the same capabilities available in the [VideoAmp public API](https://docs.videoamp.dev). The use of tools are intended to streamline workflows and integrations with APIs. 

---

# MCP Getting Started

AI assistants, agents and chatbots compatible with the [MCP protocol](https://modelcontextprotocol.io/docs/getting-started/intro) may use the remote MCP server at `https://api.videoamp.dev/v1/mcp`.

After connecting to the MCP server using one of the below [MCP Configuration Options](#mcp-configuration-options), try these sample prompts:

* "Show me tools I can use with VideoAmp"
* "List audiences available to me"
* "What campaigns do I have access to?"
* "Help me understand VideoAmp capabilities"

---

# MCP Configuration Options

## Claude Desktop with Remote Server
This option enables use of the remote MCP server through Claude Desktop without requiring local installation.

1. Open Claude Desktop and list available connectors using Manage Connectors, under the tools menu.
2. Connect the VideoAmp MCP server.

### Prerequisites
* [Claude Desktop](https://claude.com/download)
* Pro, Max, Team, or Enterprise license
* The remote server at `https://api.videoamp.dev/v1/mcp` has been added as a [Custom Connector](https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp) (Admin privileges may be needed)

---

## Claude Web with Remote Server
This option enables use of the remote MCP server through the Claude web interface without requiring local installation.

1. Open [Claude.ai](https://claude.ai) and list available connectors using Manage Connectors, under the tools menu.
2. Connect the VideoAmp MCP server.

### Prerequisites
* Pro, Max, Team, or Enterprise license
* The remote server at `https://api.videoamp.dev/v1/mcp` has been added as a [Custom Connector](https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp) (Admin privileges may be needed)

---

## Claude Code with Remote Server
This option enables use of the remote MCP server through Claude Code without requiring local installation.

1. Add the MCP server from the terminal using
```bash
claude mcp add --transport http VideoAmp https://api.videoamp.dev/v1/mcp
```

### Prerequisites
* [Claude Code](https://claude.com/product/claude-code)

---

## Codespace with Remote Server
This option provides a complete development environment with Copilot connected to the remote MCP server. No additional installation is required, and the CLI can be accessed using the `videoamp` command from a terminal.

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
