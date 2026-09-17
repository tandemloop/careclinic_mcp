<div align="center">

<img src="assets/careclinic-icon.png" width="88" height="88" alt="CareClinic" />

<pre>
 ██████╗ █████╗ ██████╗ ███████╗ ██████╗██╗     ██╗███╗   ██╗██╗ ██████╗  ███╗   ███╗ ██████╗██████╗
██╔════╝██╔══██╗██╔══██╗██╔════╝██╔════╝██║     ██║████╗  ██║██║██╔════╝  ████╗ ████║██╔════╝██╔══██╗
██║     ███████║██████╔╝█████╗  ██║     ██║     ██║██╔██╗ ██║██║██║       ██╔████╔██║██║     ██████╔╝
██║     ██╔══██║██╔══██╗██╔══╝  ██║     ██║     ██║██║╚██╗██║██║██║       ██║╚██╔╝██║██║     ██╔═══╝
╚██████╗██║  ██║██║  ██║███████╗╚██████╗███████╗██║██║ ╚████║██║╚██████╗  ██║ ╚═╝ ██║╚██████╗██║
 ╚═════╝╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝ ╚═════╝╚══════╝╚═╝╚═╝  ╚═══╝╚═╝ ╚═════╝  ╚═╝     ╚═╝ ╚═════╝╚═╝
</pre>

**We're CareClinic, the world's #1 personal health app.**

Beyond tracking. Take control of your health. CareClinic turns your symptoms, medications, and habits into personalized insights and daily actions, built on clinical frameworks to help you make measurable progress every day.

[CareClinic MCP on careclinic.io](https://careclinic.io/careclinic-mcp/) &nbsp;·&nbsp; [careclinic.io](https://careclinic.io/) &nbsp;·&nbsp; [Security](./SECURITY.md)

</div>

---

## What this is

CareClinic MCP is a hosted [Model Context Protocol](https://modelcontextprotocol.io/) server. Point any MCP-capable assistant at one URL, sign in with the CareClinic account you already have, and the assistant can work with the health record you already keep: symptoms, medications, mood, your daily schedule, and short descriptive summaries of your own data.

The CareClinic app already tracks symptoms, medications, conditions, and reminders, and acts as a Personal Health Record you can share with your care team. This connector brings that same record into whatever assistant you happen to be typing into.

No package to install. No API key to mint. No developer account. One endpoint, standard OAuth, and you are connected.

## Quick start

```
  endpoint   https://mcp.careclinic.io/mcp
  transport  streamable HTTP
  auth       OAuth 2.0  (your CareClinic sign-in)
  account    the CareClinic account you already have
```

## Add it to your assistant

<pre>
   __________  _   ___   ____________________
  / ____/ __ \/ | / / | / / ____/ ____/_  __/
 / /   / / / /  |/ /  |/ / __/ / /     / /
/ /___/ /_/ / /|  / /|  / /___/ /___  / /
\____/\____/_/ |_/_/ |_/_____/\____/ /_/
</pre>

Setup is the same shape everywhere: give your assistant the URL, then approve the CareClinic sign-in once.

**ChatGPT**

Open Settings, go to Connectors, and add a custom connector. Give it a name like `CareClinic` and paste `https://mcp.careclinic.io/mcp` as the server URL. Save it, then start a chat and ask ChatGPT to use CareClinic. It will prompt you to sign in to CareClinic the first time. Custom connectors are available on paid ChatGPT plans, so you need one of those on your account.

**Claude**

Open Settings, go to Connectors, add a custom connector, and paste `https://mcp.careclinic.io/mcp`. Approve the CareClinic sign-in when Claude opens it. Claude web, desktop, and the mobile clients all use the same connector.

**Claude Code**

```
claude mcp add --transport http careclinic https://mcp.careclinic.io/mcp
```

**Cursor, Windsurf, VS Code, Zed**

Add a remote MCP server with transport `http` and URL `https://mcp.careclinic.io/mcp`.

**Grok and other hosted assistants**

Open the assistant's connector or integrations settings, choose to add a custom MCP server, and paste the URL. Complete the CareClinic sign-in prompt when it appears.

**Anything else**

Point the client at `https://mcp.careclinic.io/mcp`. The server publishes standard OAuth protected-resource metadata at

```
https://mcp.careclinic.io/.well-known/oauth-protected-resource/mcp
```

so a compliant client discovers the flow on its own.

Once it is connected, you can ask things like "how has my sleep looked this week", "what did I take today", or "log a 6 out of 10 headache this afternoon".

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
- Get the app: https://careclinic.io/download/
- Privacy policy: https://careclinic.io/privacy-policy/
- Support: https://careclinic.io/contact-us/
- Security reports: dev@careclinic.io, or see [SECURITY.md](./SECURITY.md)

## License

Proprietary. Copyright CareClinic Software Inc. All rights reserved. See [LICENSE](./LICENSE).

This repository documents how to connect to the hosted service. It does not contain the service source.
