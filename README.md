# Speak2MyMCP by Speak2MyCV

![Speak2MyMCP](assets/logo.png)

Speak2MyMCP lets Claude read the published profile of a professional on [Speak2MyCV](https://speak2mycv.com), answer questions about their skills, experience, certifications, education and projects using only the CV and documents they uploaded, and send them an enquiry after you confirm it. Every profile on it is opted in by its owner.

## Install

In Claude Code:

```
/plugin install speak2mymcp --marketplace ABongInBusiness/speak2mymcp-plugin
```

In Claude (web, Desktop, mobile), add **Speak2MyMCP by Speak2MyCV** from the Connectors directory, or add a custom connector with the URL `https://speak2mycv.com/api/mcp`.

## What it includes

- **MCP server** (`.mcp.json`): the remote Speak2MyMCP connector at `https://speak2mycv.com/api/mcp` (Streamable HTTP).
- **Skill** (`skills/speak2mymcp`): how to find someone by handle, which tool answers which question, and the preview-then-confirm contact flow.

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

Full policy: [speak2mycv.com/legal/privacy](https://speak2mycv.com/legal/privacy). Terms: [speak2mycv.com/legal/terms](https://speak2mycv.com/legal/terms).

## Support

[speak2mycv.com/legal/contact](https://speak2mycv.com/legal/contact) · ceo@speak2mycv.com

Published by Bong Innovations Pvt Ltd (OPC), India.
