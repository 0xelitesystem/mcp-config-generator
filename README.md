# MCP Config Generator

Build and validate MCP (Model Context Protocol) server configuration JSON in your browser. MCP is an open protocol for connecting tools and data sources to LLM clients; clients read a JSON config listing the servers to connect to. Getting that JSON right by hand is fiddly, so this tool builds it from a form, validates it as you type, and shows where the file lives for common clients.

One HTML file, no external dependencies, works offline.

## Live demo

https://0xelitesystem.github.io/mcp-config-generator/

## Features

- Add any number of servers, each stdio (local command) or remote HTTP/SSE
- Stdio servers: command, argument list, and optional env key/value pairs
- Remote servers: URL plus optional headers
- Live JSON output in the `mcpServers` format used by Claude Desktop (`claude_desktop_config.json`) and Claude Code (`.mcp.json`), with a copy button
- Per-client, per-OS config file locations, including the `claude mcp add <name> -- <command>` CLI route for Claude Code
- Validation as you type: empty command or URL, spaces in server names, duplicate names, non-https remote URLs (with a localhost exception), dropped keyless env/header rows
- Paste-and-validate panel for existing configs: JSON syntax errors with hints, missing `mcpServers` key, wrong field types, per-server problems
- Three clearly labeled example presets (filesystem stdio server, generic remote HTTP server, local dev HTTP server)
- A standing security reminder: stdio servers run arbitrary local commands with your user account, so only add servers you trust
- Dark mode toggle, keyboard-friendly UI

## How it works

The form state is a plain array of server objects. On every keystroke the tool rebuilds the `mcpServers` JSON (dropping empty args and keyless pairs), reruns the validation rules, and re-renders the output and warning list. The paste validator runs `JSON.parse`, then walks the structure checking shape and field types, reporting each problem with the server name attached. There is no server and no build step; open `index.html` in any modern browser and it works, including with no network connection.

## Privacy

Everything runs client-side in your browser. Server names, commands, URLs, headers, and env values (including API keys) never leave the page. No analytics, no tracking, no network requests of any kind.

## License

MIT. Copyright 0xelitesystem 2026.
