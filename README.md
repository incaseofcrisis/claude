<p align="center">
  <img src="./assets/in-case-of-crisis-logo.png" alt="In Case of Crisis" width="110">
</p>

<h1 align="center">In Case of Crisis — Claude Plugin</h1>

<p align="center">
  <img src="https://img.shields.io/badge/version-0.1.0-203864" alt="version 0.1.0">
  <img src="https://img.shields.io/badge/platform-Claude%20Cowork%20%7C%20Claude%20Code-3E91C5" alt="Claude Cowork | Claude Code">
  <img src="https://img.shields.io/badge/status-active-27AE60" alt="status active">
</p>

<p align="center"><em>Built by RockDove Solutions</em></p>

---

## What this is

A Claude plugin that surfaces an organization's own approved crisis,
emergency, and incident-response protocols the moment a workplace safety
situation comes up in conversation — fire, severe weather, medical
emergency, security threat, evacuation, lockdown, and similar.

It bundles two components into a single install:

| Component | What it does |
|---|---|
| **Skill** | Teaches Claude when to call the In Case of Crisis connector and how to route between fetching a specific protocol or browsing the full list. |
| **MCP connector** | Connects to the In Case of Crisis directory service and retrieves an organization's own protocol content at runtime. |

No protocol content ships inside this plugin. Every installer connects
their own In Case of Crisis account, and only ever sees their own
organization's data.

## Install

### Claude Cowork (recommended for most users)

1. **Download** `in-case-of-crisis.plugin` from this repository.
2. **Drag** the file into the Cowork sidebar, or open it directly from a
   chat.
3. **Confirm** the install when prompted.

No terminal or marketplace setup required.

### Claude Code

```
/plugin marketplace add <owner>/<marketplace-repo>
/plugin install in-case-of-crisis@<marketplace-repo>
```

Replace `<owner>/<marketplace-repo>` with this repository's path.

## Prerequisite

An active **In Case of Crisis** account with your organization's protocols
already loaded. Without one, the plugin has nothing to connect to.

## First use

The first time the skill calls the connector, Claude prompts you to
authorize your In Case of Crisis account — a one-time OAuth consent. After
that, it's transparent. This is standard for OAuth-gated connectors, not
specific to this plugin.

## Usage

Ask about a workplace safety situation in plain language:

- "There's a fire on the 3rd floor."
- "What's our severe weather protocol?"
- "Walk me through our lockdown plan."

The skill routes the request to your organization's own protocol data
automatically.

## Security and privacy

- **No credentials, tokens, or hostnames are bundled** with this plugin.
  The connector's endpoint is dynamic and resolved per account through
  Claude's connector directory.
- **Data stays with the installer's own account.** This plugin does not
  bundle, cache, or transmit any organization's protocol content on its
  own behalf.
- **Trigger scope is intentionally narrow**, limited to workplace
  physical-safety situations, to avoid misrouting unrelated language from
  end users into this connector.

## Versioning

This plugin follows the version pinned in `plugin.json`. Update checks only
apply to marketplace installs — file-based installs (the Cowork drag-and-drop
path) don't auto-update, so reinstall from a newer release when one's
available.

## Support

Contact your RockDove Solutions account representative for setup help or to
report an issue with this plugin.

## License

<!-- No license has been selected for public distribution yet. Add a
     LICENSE file (e.g., MIT, Apache-2.0, or a RockDove proprietary
     license) before treating this repo as generally reusable. -->

See `LICENSE` for terms.
