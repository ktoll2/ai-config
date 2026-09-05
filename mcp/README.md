# MCP Configuration

Shareable, credential-free MCP (Model Context Protocol) server definitions: which servers exist and how to launch them, without any secrets. This directory is currently empty; it's reserved for the day this repo wants to share an MCP server list across tools instead of everyone configuring it by hand per machine.

## Format

Most tools that support MCP read a server list as JSON with a `mcpServers`-style object keyed by server name. A credential-free entry references secrets through environment variables rather than embedding them:

```jsonc
{
  "mcpServers": {
    "example-server": {
      "command": "npx",
      "args": ["-y", "@example/mcp-server"],
      "env": {
        "EXAMPLE_API_KEY": "${EXAMPLE_API_KEY}"
      }
    }
  }
}
```

Check each tool's current documentation for its exact schema (key name, `local`/`remote` transport options, etc.) before relying on this shape verbatim - it can drift between tools and versions.

## Adding a server definition

1. Add `mcp/<server-name>.json` (or a shared `mcp/servers.json`, if several are meant to be installed together) with the command, args, and any `env` keys the server needs - values, not secrets: reference an environment variable name, never a literal token.
2. Document what environment variable(s) the server expects in the file itself or this README, so installing it is just "set this variable, then merge this config."
3. If a tool needs its MCP config in a specific top-level file or under a specific key, document that tool's exact filename, key, and merge/symlink step in its own adapter README under `tools/<tool>/` - not here. This directory only holds the shared, credential-free server definitions; how a given tool consumes them is that tool's concern.

Never commit an actual API key, token, or other credential here, even temporarily - use environment variables or a local, untracked override instead.
