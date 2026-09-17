<div align="center">

<img src="assets/careclinic-icon.svg" width="84" height="84" alt="CareClinic" />

<pre>
 ██████╗ █████╗ ██████╗ ███████╗ ██████╗██╗     ██╗███╗   ██╗██╗ ██████╗  ███╗   ███╗ ██████╗██████╗
██╔════╝██╔══██╗██╔══██╗██╔════╝██╔════╝██║     ██║████╗  ██║██║██╔════╝  ████╗ ████║██╔════╝██╔══██╗
██║     ███████║██████╔╝█████╗  ██║     ██║     ██║██╔██╗ ██║██║██║       ██╔████╔██║██║     ██████╔╝
██║     ██╔══██║██╔══██╗██╔══╝  ██║     ██║     ██║██║╚██╗██║██║██║       ██║╚██╔╝██║██║     ██╔═══╝
╚██████╗██║  ██║██║  ██║███████╗╚██████╗███████╗██║██║ ╚████║██║╚██████╗  ██║ ╚═╝ ██║╚██████╗██║
 ╚═════╝╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝ ╚═════╝╚══════╝╚═╝╚═╝  ╚═══╝╚═╝ ╚═════╝  ╚═╝     ╚═╝ ╚═════╝╚═╝
</pre>

**Your own health log, inside the AI assistant you already use.**

[CareClinic MCP page](https://careclinic.io/careclinic-mcp/) &nbsp;·&nbsp; [careclinic.io](https://careclinic.io/) &nbsp;·&nbsp; [Security](./SECURITY.md)

</div>

---

## What this is

CareClinic MCP is a hosted [Model Context Protocol](https://modelcontextprotocol.io/) server. Point any MCP-capable assistant at one URL, sign in with the CareClinic account you already have, and the assistant can read the health data you already track: symptoms, mood, medications, your daily schedule, and short descriptive summaries of your own records.

No package to install. No API key to mint. No developer account. One endpoint, standard OAuth, and you are connected from the assistant you were already typing into.

## Quick start

```
  endpoint   https://mcp.careclinic.io/mcp
  transport  streamable HTTP
  auth       OAuth 2.0  (your CareClinic sign-in)
  account    the CareClinic account you already have
```

**Claude Code**

```
claude mcp add --transport http careclinic https://mcp.careclinic.io/mcp
```

**Cursor, Windsurf, VS Code, Zed**

Add a remote MCP server, transport `http`, URL `https://mcp.careclinic.io/mcp`.

**ChatGPT, Claude web and desktop, Grok, and other hosted assistants**

Add a custom remote MCP connector with the same URL, then complete the CareClinic sign-in prompt when it appears.

**Anything else**

Point the client at `https://mcp.careclinic.io/mcp`. The server publishes standard OAuth protected-resource metadata at

```
https://mcp.careclinic.io/.well-known/oauth-protected-resource/mcp
```

so a compliant client discovers the flow on its own.

## Tools

Read-only. These never change anything.

| Tool | What it does |
| --- | --- |
| `careclinic_capabilities` | Reports what this connection can and cannot do for your account |
| `careclinic_account` | Confirms which CareClinic account is connected |
| `careclinic_today_schedule` | Today's medication and supplement schedule |
| `careclinic_search_catalog` | Finds your saved symptoms, medications, and supplements |
| `careclinic_recent_wellness` | Summarizes recent symptom, mood, and medication activity |
| `careclinic_get_insights` | Returns descriptive patterns from your own records |

Check-in. These write, but only after you confirm the exact change.

| Tool | What it does |
| --- | --- |
| `careclinic_preview_log` | Prepares a check-in for you to review |
| `careclinic_commit_log` | Saves the check-in once you confirm it |

## How the connection behaves

```
  +-------------------+         OAuth 2.0         +----------------------+
  |  your assistant   |  <-------------------->   |   CareClinic login   |
  +-------------------+                           +----------------------+
            |                                                |
            |  read tools: read-only                         |  you approve once
            |  check-in:  writes only after you confirm      |
            v                                                v
        your own records, scoped to the account you signed in with
```

You authenticate against CareClinic, not against the assistant. Your password and session cookie never leave CareClinic. Disconnect from the assistant whenever you want, or revoke access in your CareClinic account, and deny any authorization request you did not start.

## What this is not

CareClinic MCP is a personal health tracking tool. It is not a diagnostic or clinical service, and it is not intended for HIPAA covered-entity use. It does not diagnose, adjust medication instructions, recommend treatment, or provide emergency help. Bring medical decisions to a clinician and emergencies to your local emergency service.

## What is shared

For the request you make, the relevant schedule entries, symptoms, moods, medication activity, and derived summaries are shared with the assistant you connected. The assistant provider may retain results under its own privacy policy.

## Links

- CareClinic MCP: https://careclinic.io/careclinic-mcp/
- CareClinic: https://careclinic.io/
- Privacy policy: https://careclinic.io/privacy-policy/
- Support: https://careclinic.io/contact-us/
- Security reports: see [SECURITY.md](./SECURITY.md)

## License

Proprietary. Copyright CareClinic Software Inc. All rights reserved. See [LICENSE](./LICENSE).

This repository documents how to connect to the hosted service. It does not contain the service source.
