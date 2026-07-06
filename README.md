# skill-smithery-ai-cli

A Smithery AI CLI skill for OpenCode agents — find, connect, and use MCP tools and skills through the [Smithery](https://smithery.ai) CLI.

## Overview

This repository packages the `smithery-ai-cli` skill, which teaches an agent how to discover integrations, connect to MCP (Model Context Protocol) servers, and call their tools via the Smithery command-line interface. Smithery is a marketplace for AI agents that exposes 100K+ tools and skills through a single CLI.

Use this skill when you want to:

- Search for new tools or skills
- Discover and connect to integrations
- Install a skill or connect to an MCP server
- Interact with external services such as email, Slack, Discord, GitHub, Jira, Notion, databases, cloud APIs, and monitoring platforms

## Capabilities

The skill covers the following Smithery CLI concepts and workflows:

- **MCP search and connect** — search the marketplace and add managed, long-lived MCP connections by URL or qualified name.
- **Tool discovery and invocation** — browse tools in a tree view, inspect a tool's input/output JSON schema, and call tools with JSON arguments.
- **Namespaces** — organize servers, connections, and skills into per-app/per-environment workspace boundaries and switch the active context.
- **Managed connections** — Smithery Connect handles the OAuth flow, credential storage, token refresh, and session lifecycle, with a status model (`connected`, `auth_required`, `error`).
- **Token scoping** — issue restricted service tokens with policy constraints for browser/mobile/agent usage instead of passing a full API key.
- **Request-level tool restrictions** — use the experimental `rpcReqMatch` to constrain specific MCP JSON-RPC requests by method and tool name.
- **Piped JSONL output** — commands emit one JSON object per line when their output is piped, for easy scripting.

## Requirements

- The `smithery` binary must be available on your system.

## Installation

Install the Smithery CLI globally:

```bash
npm install -g @smithery/cli
```

Then authenticate (this requires a human to confirm in the browser):

```bash
smithery auth login
```

## Usage

A typical workflow with the CLI:

```bash
# Search for MCP servers
smithery mcp search "github"

# Connect to a server (URL or qualified name both work)
smithery mcp add "https://github.run.tools" --id github

# Browse tools (tree view — drill into groups by passing the prefix)
smithery tool list github
smithery tool list github issues.

# Inspect a tool's input/output JSON schema
smithery tool get github issues.create

# Call a tool
smithery tool call github issues.create '{"repo": "owner/repo", "title": "Bug"}'
```

Run `smithery --help` and `<command> --help` for flags, arguments, and full examples.

## Documentation

For the full skill instructions — including namespaces, connection management, token scoping policies, request-level restrictions, and canonical workflows — see [`SKILL.md`](./SKILL.md).

## License

Released under the [MIT License](./LICENSE).
