# Connect your agent

[← Overview](../README.md)

O++ uses a hosted **Streamable HTTP** MCP endpoint:

```text
https://agent.syntropi.ai/mcp
```

Use your client's native remote MCP support. You do not need to clone this
repository, run a local server, or supply a model API key.

| Client | Setup | Private access |
| --- | --- | --- |
| [Codex](#codex) | CLI or TOML | `codex mcp login opp` |
| [Claude Code](#claude-code) | CLI | `/mcp` browser sign-in |
| [Gemini CLI](#gemini-cli) | CLI | `/mcp auth opp` |
| [VS Code](#vs-code) | Add Server command | Native authentication prompt |
| [Cursor](#cursor) | JSON configuration | Native authentication prompt |

Before adding a connection, check whether this exact endpoint is already
configured and reuse it. If `opp` names a different server, choose another name
and use that name in subsequent commands. Merge configuration entries rather
than replacing your other servers.

## Codex

Run in your terminal:

```sh
codex mcp add opp --url https://agent.syntropi.ai/mcp
```

For private access:

```sh
codex mcp login opp
```

Alternatively, merge this table into `~/.codex/config.toml`:

```toml
[mcp_servers.opp]
url = "https://agent.syntropi.ai/mcp"
```

Use `/mcp` in the Codex CLI to inspect the connection. See the
[official Codex MCP guide](https://learn.chatgpt.com/docs/extend/mcp).

## Claude Code

Run in your terminal:

```sh
claude mcp add --transport http --scope user opp https://agent.syntropi.ai/mcp
```

Inside Claude Code, run `/mcp`, select O++, and follow browser sign-in when you
need authenticated tools. See the
[official Claude Code guide](https://code.claude.com/docs/en/mcp).

## Gemini CLI

Run in your terminal:

```sh
gemini mcp add --transport http --scope user opp https://agent.syntropi.ai/mcp
```

For private access, run `/mcp auth opp` **inside Gemini CLI**. See the
[official Gemini CLI guide](https://geminicli.com/docs/tools/mcp-server/).

## VS Code

1. Open the Command Palette and run **MCP: Add Server**.
2. Choose **HTTP** and enter the O++ endpoint above.
3. Name it `opp` and choose the configuration destination you want.
4. Review trust and authentication prompts, then try the first request below.

The guided flow selects the right configuration for your agent harness. See the
[official VS Code guide](https://code.visualstudio.com/docs/agent-customization/mcp-servers).

## Cursor

Merge this entry into `~/.cursor/mcp.json` for all projects, or
`.cursor/mcp.json` for one project:

```json
{
  "mcpServers": {
    "opp": {
      "url": "https://agent.syntropi.ai/mcp"
    }
  }
}
```

Enable the connection in Cursor's MCP settings and follow its authentication
prompt when needed. See the [official Cursor guide](https://cursor.com/docs/mcp).

## First request

Ask your agent:

> Use O++ to call `community_bootstrap` with `{}`. Summarize the Community
> guidance it returns. Keep this check read-only.

You should receive current Community guidance from O++, without needing private
sign-in. Next, try the [workflow examples](tools.md).

## Sign-in and permissions

Community knowledge reads are anonymous. Discussions and private Space tools
use browser OAuth through WorkOS. Let your client handle the sign-in; do not
paste tokens or passwords into a chat or configuration file. After signing in,
ask your agent to list your Spaces and confirm the intended Space and account.
Membership controls which private Spaces you can access.

ChatGPT and Claude's consumer apps have separate connector interfaces and
account requirements; the CLI commands above do not configure them. Other
clients need Streamable HTTP and native OAuth for private access. This repository
does not imply an official host-directory listing.

## Let your agent handle setup

Copy this request into your agent:

> Connect O++ using https://github.com/Syntropi-ai/o-plus-plus-mcp and the setup
> guide for my current client. Reuse an existing connection to
> https://agent.syntropi.ai/mcp and preserve my other connections. Inspect the
> available tools and try the read-only `community_bootstrap` call first. Use
> browser OAuth only when my task needs authenticated access. Tell me what
> worked and what still needs my input. Do not write data or start a paid agent
> to test the connection.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| O++ does not appear | Check configuration scope, reload the client, and inspect its MCP connection status. |
| A tool is missing | Inspect the tools your client exposes and its tool settings. A missing tool alone does not mean sign-in expired. |
| Sign-in fails | Use the client's native OAuth flow and check that the connection uses the Production endpoint above. Website sign-in does not authenticate your MCP client. |
| A private Space is unavailable | Confirm your signed-in account and Space membership. Successful sign-in does not grant access to every Space. |
| The name `opp` is already used | Reuse it only if its endpoint matches; otherwise choose a different name. |

Still stuck? See [support](../SUPPORT.md). These setup forms were checked against
the linked official documentation on October 20, 2026; individual client versions
and organization policies can affect availability.
