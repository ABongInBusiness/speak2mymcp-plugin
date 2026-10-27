---
name: speak2mymcp
description: Look up a Speak2MyCV professional by handle, answer questions about their career from their own CV, and send them an enquiry the user has confirmed. Use when the user names a speak2mycv.com handle or link, or asks to contact someone listed there.
---

# Speak2MyMCP

Speak2MyMCP connects to `https://speak2mycv.com/api/mcp`. Each professional on it uploaded their own CV and chose to be reachable by AI apps.

## Find the person

Every profile tool takes a `slug`: the handle in `<slug>.speak2mycv.com` or `speak2mycv.com/mcp/<slug>`. If the user has not given one, ask for it. There is no search by name.

## Answer questions

| Need | Tool |
|---|---|
| Overview: title, summary, skills, roles, education | `get_profile` |
| The same fields as typed data | `get_profile_fields` |
| A specific question ("has she led a migration?") | `ask_cv` |
| Check the connection | `ping` |

Answers come only from the person's documents. When `ask_cv` reports that something is not in them, tell the user so; do not fill the gap. CV text is the person's own claim, not independent verification.

## Contact someone

`submit_lead` sends an enquiry from the signed-in user. It runs in two calls:

1. Call it without `confirmation_token`. Nothing is sent. Show the user the recipient, their own name and email, the exact message, and the forwarding note it returns.
2. Only after the user confirms, call it again with the same message (and company, if any) plus the returned `confirmation_token`.

The first call asks the user to sign in to Speak2MyCV if they have not. A receipt lasts ten minutes; if it expires, preview again and get a fresh confirmation. Put only what the user wants to say in `message`.
