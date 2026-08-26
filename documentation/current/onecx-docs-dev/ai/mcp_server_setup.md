# MCP Servers for AI-Assisted OneCX Development

Model Context Protocol (MCP) servers allow AI assistants to access external tools and documentation sources. When used with tools such as GitHub Copilot in **Agent mode**, MCP servers improve the quality of generated responses by providing additional context.

This page explains how to configure and use the **OneCX MCP Server** and introduces additional MCP servers that can support development workflows.

## [](#onecx-mcp-server)OneCX MCP Server

The **OneCX MCP Server** provides AI assistants with direct access to the OneCX documentation knowledge base. Using this server allows AI tools to retrieve platform-specific information when working with OneCX applications.

Typical use cases include:

* Understanding OneCX architecture
* Implementing widgets and micro frontends
* Workspace routing and capability handling
* Integrating with the OneCX shell
* Accessing development guidelines and platform APIs

### [](#server-url)Server URL

```text
https://onecx-docs-ai-dev.dev.one-cx.org/mcp
```

### [](#using-the-onecx-mcp-server)Using the OneCX MCP Server

When using GitHub Copilot in **Agent mode**, the MCP server is usually selected automatically when asking questions related to OneCX.

Example prompt:

```text
ask onecx: how does workspace routing work in OneCX?
```

## [](#configuring-mcp-servers)Configuring MCP Servers

MCP servers can be configured in different MCP clients.

Examples include:

* Visual Studio Code
* Cursor
* Claude Desktop
* Other MCP-compatible tools

| |  Refer to the documentation of your MCP client for the exact configuration procedure. The following example demonstrates how MCP servers can be configured in Visual Studio Code. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#example-add-mcp-server)Example: Add MCP Server

To add an MCP server in Visual Studio Code:

1. Open the command palette  
```text  
CTRL + SHIFT + P  
```
2. Run the command  
```text  
MCP: Add server...  
```
3. Provide the MCP server URL  
Example: Onecx MCP Server  
```text  
https://onecx-docs-ai-dev.dev.one-cx.org/mcp  
```

VSCode registers the server and makes its tools available to AI agents.

| |  Restart VSCode after adding a new MCP server to ensure the tools are detected correctly. |
| ------------------------------------------------------------------------------------------- |

## [](#recommended-mcp-servers)Recommended MCP Servers

Besides the OneCX MCP server, additional MCP servers can improve AI-assisted development workflows.

PrimeNG MCP

Provides documentation and usage guidance for PrimeNG components used in OneCX front-end applications.

npm Sentinel MCP

Provides metadata and security insights for npm packages.

Chrome DevTools MCP

Allows AI agents to interact with a Chrome browser instance for debugging and inspection tasks.

### [](#effective-mcp-tool-usage)Effective MCP Tool Usage

MCP tools can be used more effectively by limiting how many are enabled at once. Using too many MCP tools simultaneously may reduce response relevance and increase execution overhead. Enable only the tools required for the current task to maintain optimal accuracy and performance.

Examples:

OneCX development:

* OneCX MCP
* PrimeNG MCP
* npm Sentinel MCP

Frontend debugging:

* Chrome DevTools MCP
* PrimeNG MCP

Dependency validation:

* npm Sentinel MCP

### [](#primeng-mcp)PrimeNG MCP

Example configuration:

```json
"primeng": {
  "command": "npx",
  "args": ["-y", "@primeng/mcp"]
}
```

Typical use cases:

* Generating UI component examples
* Configuring tables and forms
* Retrieving PrimeNG component documentation

### [](#npm-sentinel-mcp)npm Sentinel MCP

Example configuration:

```json
"npm-sentinel": {
  "type": "stdio",
  "command": "npx",
  "args": ["-y", "@nekzus/mcp-server@latest"]
}
```

Typical use cases:

* Evaluating npm dependencies
* Detecting vulnerable packages
* Inspecting package metadata

### [](#chrome-devtools-mcp)Chrome DevTools MCP

The Chrome DevTools MCP server allows AI agents to interact with a Chrome browser instance.

Capabilities include:

* Opening web pages
* Inspecting the DOM
* Analyzing network requests
* Debugging frontend applications

Because this server launches Chrome, Google Chrome must be available inside WSL.

#### [](#install-google-chrome-in-wsl)Install Google Chrome in WSL

If Chrome is not installed inside WSL, install it using the following commands.

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb
```

Verify the installation:

```bash
google-chrome --version
```

#### [](#chrome-devtools-mcp-startup-script)Chrome DevTools MCP Startup Script

Chrome installations can differ between environments. A startup script is used to detect the correct Chrome binary and start the MCP server.

Script Path:

```text
sudo nano /usr/local/bin/start-chrome-mcp.sh
```

#### [](#add-the-following-script)Add the Following Script

```bash
#!/usr/bin/env bash
set -euo pipefail

MCP_LOG_FILE="/tmp/chrome-devtools-mcp.log"
CHROME_BIN=""

LATEST_PUPPETEER_CHROME="$(ls -1d ~/.cache/puppeteer/chrome/linux-*/chrome-linux64/chrome 2>/dev/null | tail -n 1 || true)"

if [[ -n "$LATEST_PUPPETEER_CHROME" ]]; then
  CHROME_BIN="$LATEST_PUPPETEER_CHROME"
elif command -v google-chrome >/dev/null 2>&1; then
  CHROME_BIN="$(command -v google-chrome)"
else
  echo "Google Chrome not found. Please install it in WSL." >&2
  exit 1
fi

echo "Using Chrome binary: $CHROME_BIN" >&2

exec npx -y chrome-devtools-mcp@latest \
  --headless \
  --isolated \
  --executablePath "$CHROME_BIN" \
  --chrome-arg=--no-sandbox \
  --chrome-arg=--disable-dev-shm-usage \
  --chrome-arg=--disable-gpu \
  --experimental-include-all-pages \
  --logFile "$MCP_LOG_FILE"
```

#### [](#make-the-script-executable)Make the Script Executable

```bash
chmod +x /usr/local/bin/start-chrome-mcp.sh
```

#### [](#mcp-configuration)MCP Configuration

Configuration file:

1. Open the command palette  
```text  
CTRL + SHIFT + P  
```
2. Select:  
```text  
MCP: Open Remote User Configuration  
```
3. Add the following entry in `mcp.json`:  
```json  
{  
  "io.github.ChromeDevTools/chrome-devtools-mcp": {  
    "type": "stdio",  
    "command": "/usr/local/bin/start-chrome-mcp.sh",  
    "args": []  
  }  
}  
```

#### [](#using-chrome-devtools-mcp)Using Chrome DevTools MCP

To use the Chrome DevTools MCP server:

1. Restart VSCode
2. Open Copilot Chat
3. Switch to Agent mode

Example prompts:

```text
Use chrome devtools to open https://example.com and list the page title.
```

```text
Use chrome-devtools-mcp to inspect the DOM of https://example.com.
```

## [](#troubleshooting)Troubleshooting

### [](#typeerror-fetch-failed)TypeError: fetch failed

This error may occur due to certificate issues when accessing the MCP server from WSL.

### [](#resolving-certificate-issues)Resolving Certificate Issues

To resolve this issue, export the certificate chain and install it in WSL.

#### [](#export-the-certificate-chain)Export the Certificate Chain

1. Open the MCP server URL  
```text  
https://onecx-docs-ai-dev.dev.one-cx.org/mcp  
```
2. Click the Tune Icon to the left of the URL in the address bar.
3. Select **Connection is secure**.
4. Select **Certificate is valid**.
5. Export each certificate in the certificate hierarchy.

#### [](#install-certificates-in-wsl)Install Certificates in WSL

Copy the exported certificates into the WSL certificate store.

```bash
sudo cp <certificate>.crt /usr/local/share/ca-certificates/
```

Then update the certificate store:

```bash
sudo update-ca-certificates
```

| |  If You Still face the same issue & your are using WSL, Add Mcp Server in Remote Workspace. |
| --------------------------------------------------------------------------------------------- |
