# VideoAmp CLI + MCP Server
The VideoAmp CLI + MCP Server is intended to streamline workflows and integrations with VideoAmp's APIs. Detailed API specs can be found at https://docs.videoamp.dev.


---

## Copilot + MCP Quickstart
1. <a href="https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=894753956" target="_top">Create a CLI Codespace</a>.

2. Configure Copilot CHAT
In the CHAT panel select mode `Agent` and a recent model, e.g. `Claude Sonnet 4.5`, `Chat GPT-5` or higher.

<img width="539" height="146" alt="image" src="https://github.com/user-attachments/assets/e370ab53-bd97-42ee-aa53-6410f742b97e" />

3. Ask Copilot `What VideoAmp tools can I use?` or `Show questions I can ask VideoAmp.` You should see a list of tools that map to VideoAmp APIs.


---

## Local MCP Installation
1. Visit the [releases page](https://github.com/VideoAmp/cli/releases) and download the asset that matches your OS and CPU architecture (for example `videoamp_v0.10.0_linux_amd64.tar.gz`, `videoamp_v0.10.0_darwin_arm64.targ.gz`, or `videoamp_v0.10.0_windows_amd64.zip`).

2. Extract the archive and move the `videoamp` executable somewhere on your `$PATH` (for example `/usr/local/bin` on macOS/Linux or `%USERPROFILE%\AppData\Local\Microsoft\WindowsApps` on Windows).
	 - macOS/Linux:
		 ```bash
		 tar -xzf videoamp_<version>_<os>_<arch>.tar.gz
		 sudo mv videoamp /usr/local/bin/
		 chmod +x /usr/local/bin/videoamp
		 ```
	 - Windows (PowerShell):
		 ```powershell
		 Expand-Archive -Path .\videoamp_<version>_windows_amd64.zip -DestinationPath .
		 Move-Item -Path .\videoamp.exe -Destination $env:USERPROFILE\AppData\Local\Microsoft\WindowsApps\videoamp.exe
		 ```
3. Confirm the installation:
	 ```bash
	 videoamp --help
	 ```

---

## Claude Desktop w/ Local MCP
To use the VideoAmp MCP server locally with Claude Desktop:

1. Complete the [Local MCP Installation](#local-mcp-installation) steps.
2. Verify the server runs w/ out an error:
```bash
videoamp mcp start-server
```
3. Open Claude Desktop, then go to Settings > Developer > Edit Config. This opens the path of the JSON config. Open the config file.

Add an entry under mcpServers for your computer-use server, using stdio launch via npx:
```json
{
  "mcpServers": {
    "videoamp": {
      "command": "videoamp",
      "args": ["mcp", "start-server"]
    }
  }
}
```
Save the config file and restart Claude Desktop.

4. After restart, open a new chat and look for the tools indicator. Ask Claude `What VideoAmp tools can I use?` or `Show questions I can ask VideoAmp.` You should see a list of tools that map to VideoAmp APIs.


---

## Claude Desktop w/ Remote MCP
A remote server implementation is under development
