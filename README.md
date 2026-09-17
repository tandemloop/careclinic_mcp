# CareClinic MCP

Connect the health records you already keep in CareClinic to the AI assistant you
already use.

CareClinic MCP is a hosted Model Context Protocol server. Your assistant can read
selected information from your own CareClinic account through OAuth, so you can
ask about your day, your symptoms, or your medications without copying anything
between apps.

## Endpoint

```
https://mcp.careclinic.io/mcp
```

Streamable HTTP with OAuth 2.0. You sign in with the CareClinic account you
already have. There is no developer account to create and no separate sign-up.

## Connect your assistant

**Claude Code**

```
claude mcp add --transport http careclinic https://mcp.careclinic.io/mcp
```

**Cursor, Windsurf, VS Code**

Add an MCP server with the URL above and transport type `http`.

**ChatGPT and Claude web or desktop**

Add a custom remote MCP connector with the URL above, then complete the
CareClinic sign-in prompt.

**Other MCP clients**

Point the client at the same URL. Authentication uses the standard OAuth
protected-resource metadata published at
`https://mcp.careclinic.io/.well-known/oauth-protected-resource/mcp`.

## Tools

Read-only:

| Tool | What it does |
| --- | --- |
| `careclinic_capabilities` | Reports what this connection can and cannot do for your account |
| `careclinic_account` | Confirms which CareClinic account is connected |
| `careclinic_today_schedule` | Today's medication and supplement schedule |
| `careclinic_search_catalog` | Finds saved symptoms, medications, and supplements |
| `careclinic_recent_wellness` | Summarizes recent symptom, mood, and medication activity |
| `careclinic_get_insights` | Returns descriptive patterns from your own records |

Check-in tools, which only run after you explicitly confirm the exact change:

| Tool | What it does |
| --- | --- |
| `careclinic_preview_log` | Prepares a check-in for you to review |
| `careclinic_commit_log` | Saves the check-in once you confirm it |

## What this is not

CareClinic MCP is a personal health tracking tool. It is not a diagnostic or
clinical service, and it is not intended for HIPAA covered-entity use. It does
not diagnose, adjust medication instructions, recommend treatment, or provide
emergency help. Contact a clinician for medical decisions and emergency services
for emergencies.

## What is shared

For the request you make, the relevant schedule entries, symptoms, moods,
medication activity, and derived summaries are shared with the assistant you
connected. Your CareClinic password and session cookie are never sent to the
assistant. The assistant provider may retain results under its own privacy
policy.

Disconnect from the assistant whenever you want, or revoke access in your
CareClinic account. Deny any authorization request you did not start.

## Links

- CareClinic: https://careclinic.io/
- Privacy policy: https://careclinic.io/privacy-policy/
- Support: https://careclinic.io/contact-us/
- Security reports: see [SECURITY.md](./SECURITY.md)

## License

Proprietary. Copyright CareClinic Software Inc. All rights reserved. See
[LICENSE](./LICENSE). This repository documents how to connect to the hosted
service; it does not contain the service source.
