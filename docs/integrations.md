# Connect your agent

[← Overview](../README.md)

O++ uses a hosted **Streamable HTTP** MCP endpoint:

```text
https://agent.syntropi.ai/mcp
```

Use your client's native remote MCP support. You do not need to clone this
repository, run a local server, or supply a model API key.

## AI chat apps

Use a published O++ listing when one is available. This repository does not
establish a listing in any host directory. For supported custom connections,
use the endpoint above and the host’s normal browser authorization:

| Host | Custom connection |
| --- | --- |
| [ChatGPT](https://developers.openai.com/plugins/deploy/connect-chatgpt) | **Plugins → + → Add custom MCP server**. Review authentication, create the plugin, then select it with `@` in a new chat. |
| [Claude web / Desktop](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp) | **Customize → Connectors**. Add a remote connector and sign in. Managed accounts may need an authorized owner first. Desktop uses the same remote route; no local server or extension is needed. |
| [Gemini web](https://support.google.com/gemini/answer/17209137?hl=en) | Add a custom app using the MCP URL, then select it with `@`. Current eligibility: US, age 18+, personal account, English, Keep Activity enabled; work/school accounts are excluded. |
| [Grok](https://docs.x.ai/grok/connectors) | Open **grok.com/connectors → New Connector → Custom**. Business/enterprise setups may need an administrator. |

Muse’s [reviewed-connector platform](https://platform.muse.ai/docs) does not
establish an available O++ listing or arbitrary custom-install route. Verify
availability in the actual account rather than guessing a setup procedure.

## Desktop, IDE and CLI

Use only the configuration for the app and agent harness you actually run:

| Client | Setup | Private access |
| --- | --- | --- |
| [Codex](#codex) | Native settings, CLI or TOML | `codex mcp login opp` |
| [Claude Code](#claude-code) | CLI | `/mcp` browser sign-in |
| [Gemini CLI](#gemini-cli) | CLI | `/mcp auth opp` |
| [VS Code](#vs-code) | Add Server command | Native authentication prompt |
| [Cursor](#cursor) | JSON configuration | Native authentication prompt |

Before adding a connection, check whether this exact endpoint is already
configured and reuse it. If `opp` names a different server, choose another name
and use that name in subsequent commands. Merge configuration entries rather
than replacing your other servers. Production and QA are separate connections;
do not replace one with the other to work around a missing tool.

## Codex

Codex desktop, CLI and its IDE integration share native MCP configuration on
the same host. ChatGPT web does not read that local configuration. Use the
app’s MCP settings, or run:

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

## First connected chat

> I just connected O++. Tell me about it and help me take one useful first step.

The agent should call `community_bootstrap`, then retrieve
`skills/use-community-knowledge/SKILL.md` with `get_skill` at the returned
revision and follow **Onboard through the external AI**. That is the current
onboarding flow; it works without locally installed skills.

The introduction stays brief: explain Personal, offer a useful first action,
and help create a shared Space or invite someone when requested. It also shows
how relevant Community skills and optional internal agents can help. The agent
checks any remembered introduction preference; an existing Space is not proof
of completed onboarding. Ask about a feature later without repeating the tour.

## Sign-in and permissions

Community knowledge reads are anonymous. Discussions and private Space tools
use browser OAuth through WorkOS. Browser authorization creates or signs into
your O++ account; use the same account in another AI host to reach your existing
Spaces. The person completes identity and consent in the browser. Do not paste
tokens or passwords into chat or configuration files.

Website sign-in does not authenticate an AI host. After the connection is ready,
ask the agent to confirm your account and current Space membership. Your
Personal Space cannot be shared; create a separate Space for collaboration.

## Let your agent handle setup

Copy this into an agent that can configure your app:

> Connect O++ in this app using the installation skill at
> https://raw.githubusercontent.com/Syntropi-ai/o-plus-plus-mcp/main/skills/connect-to-o-plus-plus/SKILL.md

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| O++ does not appear | Check configuration scope, reload the client, and inspect its MCP connection status. |
| A tool is missing | Inspect the tools your client exposes and its tool settings. A missing tool alone does not mean sign-in expired. |
| Sign-in fails | Use the client's native OAuth flow and check that the connection uses the Production endpoint above. Website sign-in does not authenticate your MCP client. |
| A private Space is unavailable | Confirm your signed-in account and Space membership. Successful sign-in does not grant access to every Space. |
| The name `opp` is already used | Reuse it only if its endpoint matches; otherwise choose a different name. |

Still stuck? See [support](../SUPPORT.md). These setup forms were checked against
the linked official documentation on October 22, 2026; individual client versions
and organization policies can affect availability.
