# VideoAmp Tools

VideoAmp Tools includes both the VideoAmp MCP Server and CLI.  All are intended to streamline workflows and integrations with VideoAmp's APIs. Detailed API specs can be found at https://docs.videoamp.dev.
  
---
  
## Copilot + Codespace (zero install)
The following steps will launch a codespace (virtual) machine and requests no installation by a user.

1. <a href="https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=894753956" target="_top">Create a Codespace</a>.
2. In Copilot, select mode `Agent` and a recent model, e.g. `Claude Sonnet 4.5`, `Chat GPT-5`.
3. Ask Copilot `What VideoAmp tools can I use?` or `Show questions I can ask VideoAmp.`
  
---
  
## Claude Desktop (local install)
The following steps require Claude Desktop and the maintenance of a MCP server running locally.

### Mac(apple silicon)
1. Download [VideoAmp-MCP-darwin-arm64.mcpb](https://github.com/VideoAmp/cli/releases/download/v0.34.0/VideoAmp-MCP-darwin-arm64.mcpb).
2. Double-click the downloaded file.
3. Click Install 
<img width="802" height="269" alt="image" src="https://github.com/user-attachments/assets/b57340e2-11b5-44eb-9a43-cbe1b22eaa28" />
3. Ask Copilot `What VideoAmp tools can I use?` or `Show questions I can ask VideoAmp.`

### Windows
1. Coming soon..
  
---
  
## Claude.ai (remote MCP)
The following may require a Pro Claude account.

1. Coming soon...
  
---
  
## General CLI Installation


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
