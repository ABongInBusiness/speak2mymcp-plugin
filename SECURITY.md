# Security policy

## Reporting a vulnerability

Please report security issues privately, not in a public issue:

- GitHub: **Security → Report a vulnerability** on this repository, or
- Email: ceo@speak2mycv.com with "Security" in the subject.

Include what you found, how to reproduce it, and what an attacker could do with it. We acknowledge reports within 3 working days and keep you updated until it is fixed. Please give us a reasonable time to fix an issue before disclosing it publicly.

## Scope

- This plugin's files (manifests, `.mcp.json`, skill).
- The Speak2MyMCP server at `https://speak2mycv.com/api/mcp` and personal servers at `https://<handle>.speak2mycv.com/mcp`, including sign-in (OAuth) and the contact flow.

Out of scope: denial-of-service or load testing, social engineering, and testing against profiles or accounts that are not your own. Do not access, change or delete other people's data; stop and report as soon as you reach any.

## Supported versions

Only the latest release is supported. The plugin runs no local code; fixes to the server apply to every version immediately.
