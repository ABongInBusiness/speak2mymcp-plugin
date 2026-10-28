---
name: speak2mymcp
description: Look up a Speak2MyCV professional by handle, answer questions about their career from their own CV, and send them an enquiry the user has confirmed. Use when the user names a speak2mycv.com handle or link, or asks to contact someone listed there.
---

# Speak2MyMCP

Speak2MyMCP connects to `https://speak2mycv.com/api/mcp`. Each professional on it uploaded their own CV and chose to be reachable by AI apps.

## Find the person

Every profile tool takes a `slug`: the handle in `<slug>.speak2mycv.com` or `speak2mycv.com/mcp/<slug>`. If the user has not given one, ask for it. There is no search by name; do not guess a handle.

## Answer questions

| Need | Tool |
|---|---|
| Overview: title, summary, skills, roles, education | `get_profile` |
| The same fields as typed data | `get_profile_fields` |
| A specific question ("have they led a migration?") | `ask_cv` |
| Check the connection | `ping` |

Answers come only from the person's documents. When `ask_cv` reports that something is not in them, tell the user so; do not fill the gap. CV text is the person's own claim, not independent verification.

## Contact someone

`submit_lead` sends an enquiry from the signed-in user. It runs in two calls:

1. Call it without `confirmation_token`. Nothing is sent. Show the user the recipient, their own name and email, the exact message, and the forwarding note it returns.
2. Only after the user confirms, call it again with the same message (and company, if any) plus the returned `confirmation_token`.

The first call asks the user to sign in to Speak2MyCV if they have not. A receipt lasts ten minutes. Put only what the user wants to say in `message`.

## When a call fails

| The tool says | Do this |
|---|---|
| Sign-in needed, or "sign-in expired" | Let Claude show the Connect prompt; once the user signs in, retry the same call |
| "No MCP-enabled Speak2MyCV profile found" | Tell the user; the handle may be wrong or its owner switched AI access off. Ask them to check the handle |
| "This confirmation expired or … changed" | Preview again and get a fresh confirmation; never resend with the old token |
| "Rate limit reached" | Tell the user to wait a minute; do not retry in a loop |
| "took too long to answer" | Retry once with a shorter, more specific question |

## Example

User: "Has jane-doe run an Azure migration? If so, ask whether they're free in March."

1. `ask_cv` with slug `jane-doe` and the migration question; report the answer and its sources.
2. `submit_lead` without a token; show the preview and ask "Send this?"
3. On "yes", `submit_lead` again with the same message and the `confirmation_token`; report that it was sent.
