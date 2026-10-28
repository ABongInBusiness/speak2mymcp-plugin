# Speak2MyMCP by Speak2MyCV

![Speak2MyMCP](assets/logo.png)

Speak2MyMCP lets Claude read the published profile of a professional on [Speak2MyCV](https://speak2mycv.com), answer questions about their skills, experience, certifications, education and projects using only the CV and documents they uploaded, and send them an enquiry after you confirm it. Every profile on it is opted in by its owner.

## Install

In Claude Code:

```
/plugin marketplace add ABongInBusiness/speak2mymcp-plugin
/plugin install speak2mymcp
```

Recent Claude Code versions also accept one line: `/plugin install speak2mymcp --marketplace ABongInBusiness/speak2mymcp-plugin`.

In Claude (web, Desktop, mobile), add **Speak2MyMCP by Speak2MyCV** from the Connectors directory, or add a custom connector with the URL `https://speak2mycv.com/api/mcp`.

To remove it: `/plugin uninstall speak2mymcp`, or remove the connector in Claude's settings.

## Try it

- "Check the Speak2MyMCP connection."
- "Show the skills and experience for handle `<handle>`."
- "Has `<handle>` led a cloud migration? Then draft an enquiry about a six-week project and show it to me before sending."

Replace `<handle>` with the part before `.speak2mycv.com` in the person's link.

## What it includes

- **MCP server** (`.mcp.json`): the remote Speak2MyMCP connector at `https://speak2mycv.com/api/mcp` (Streamable HTTP).
- **Skill** (`skills/speak2mymcp`): how to find someone by handle, which tool answers which question, the preview-then-confirm contact flow, and what to do when a call fails.

## Tools

| Tool | Access | What it does |
|---|---|---|
| `ping` | read-only | Health check |
| `get_profile` | read-only | Published profile by handle |
| `get_profile_fields` | read-only | The same profile as typed fields |
| `ask_cv` | read-only | Answers one question from the person's documents |
| `submit_lead` | write, needs sign-in | Previews, then on your confirmation sends, an enquiry |

## Sign-in

Reading profiles needs no account. Contacting someone asks you to sign in to Speak2MyCV (OAuth 2.1 via Clerk, permissions `profile` and `email`) so the recipient sees a verified sender.

## Data and privacy

The plugin talks only to `speak2mycv.com`. It runs no local code, reads no files, and sends no conversation history.

- **Reads:** each call records the tool, the profile handle, the outcome, a salted hash of the client (never the IP), and your account ID if you are signed in. The question text is not stored with it; server logs keep at most its first 80 characters for abuse moderation.
- **Contact:** your verified name, email and the exact message you confirm are stored in the recipient's enquiry inbox and forwarded by email and any webhook they configured. Sending cannot be recalled.
- **Retention:** usage events are deleted after 90 days.
- **Access or deletion:** ask through [speak2mycv.com/legal/contact](https://speak2mycv.com/legal/contact).

Full policy: [speak2mycv.com/legal/privacy](https://speak2mycv.com/legal/privacy). Terms: [speak2mycv.com/legal/terms](https://speak2mycv.com/legal/terms).

## Troubleshooting

| Problem | Fix |
|---|---|
| "No MCP-enabled Speak2MyCV profile found" | Check the handle. The owner may also have switched AI access off |
| Asked to sign in again | Your sign-in expired; reconnect and retry |
| "This confirmation expired" | Previews last ten minutes. Ask for a new preview and confirm it |
| "Rate limit reached" | Wait a minute and try again |
| Tools don't appear in Claude Code | Run `/plugin` to check it is enabled, then `/mcp` to check the `speak2mymcp` server is connected |

## Versions and security

Changes are listed in [CHANGELOG.md](CHANGELOG.md); releases are tagged `vX.Y.Z`. To report a vulnerability, see [SECURITY.md](SECURITY.md).

## Support

[speak2mycv.com/legal/contact](https://speak2mycv.com/legal/contact) · ceo@speak2mycv.com

Published by Bong Innovations Pvt Ltd (OPC), India.
