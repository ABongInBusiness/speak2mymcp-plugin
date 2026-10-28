# Changelog

All notable changes to this plugin. Versions follow [Semantic Versioning](https://semver.org); each release is tagged `vX.Y.Z` in this repository.

## 1.0.2 — 2026-10-28

- README: shorter install and uninstall commands, `/plugin install speak2mymcp` and `/plugin uninstall speak2mymcp` (the `@speak2mycv` marketplace suffix is optional).

## 1.0.1 — 2026-10-28

- Manifests: `repository` in `plugin.json`; `$schema`, version, category, homepage, repository and license on the marketplace entry.
- Skill: what to do when a call fails (sign-in, not found, expired confirmation, rate limit, timeout), a worked example, neutral wording.
- README: both install forms, example prompts, troubleshooting, uninstall, data deletion.
- Added `SECURITY.md` and `CHANGELOG.md`.

No change to the connector URL, the tools or the data the plugin sends.

## 1.0.0 — 2026-10-28

- First release: remote MCP connector at `https://speak2mycv.com/api/mcp` (`ping`, `get_profile`, `get_profile_fields`, `ask_cv`, `submit_lead`) and the `speak2mymcp` skill.
