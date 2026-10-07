<h1 align="center"><img src="./assets/in-case-of-crisis-logo.png" width="32" align="absmiddle"> In Case of Crisis — Claude Plugin</h1>

<p align="center">
  <img src="https://img.shields.io/badge/version-0.1.0-203864" alt="version 0.1.0">
  <img src="https://img.shields.io/badge/platform-Claude%20Cowork%20%7C%20Claude%20Code-3E91C5" alt="Claude Cowork | Claude Code">
  <img src="https://img.shields.io/badge/status-active-27AE60" alt="status active">
  <img src="https://img.shields.io/badge/license-MIT-3E91C5" alt="license MIT">
</p>

<p align="center"><img src="./assets/rockdove-logo.png" width="18" align="absmiddle"> <em>Built by RockDove Solutions</em></p>

---

## What this is

A Claude plugin that surfaces an organization's own approved crisis,
emergency, and incident-response protocols the moment a workplace safety
situation comes up in conversation — fire, severe weather, medical
emergency, security threat, evacuation, lockdown, and similar.

It bundles two components into a single install:

| Component | What it does |
|---|---|
| **Skill** | Teaches Claude when to call the In Case of Crisis connector and how to search for, and then fetch, the protocol that matches the situation. |
| **MCP connector** | Connects to In Case of Crisis's hosted gateway (`mcpgateway.incaseofcrisis.com`) over Streamable HTTP. |

No protocol content ships inside this plugin. Every installer still
authorizes their own In Case of Crisis account — the shared gateway URL
tells Claude where to connect, but doesn't skip that per-account consent
step — and only ever sees their own organization's data.

## Install

### Claude Cowork

**Recommended — add as a marketplace:**

1. Open **Customize → Plugins → Browse plugins**.
2. Add this repository as a marketplace source: `incaseofcrisis/claude`.
3. Install **In Case of Crisis** from the catalog.

**Quick trial installs (no marketplace setup):** download the packaged
`.plugin` file from this repo's [Releases page](../../releases) and drag it
into the Cowork sidebar, or open it from a chat. Confirm the install when
prompted. Use this path for one-off trial installs; it won't receive
update notifications the way a marketplace install does.

### Claude Code

```
/plugin marketplace add incaseofcrisis/claude
/plugin install in-case-of-crisis@incaseofcrisis-claude
```

The identifier after `@` is the marketplace's *name*, not its repo path — Claude
Code derives it as `owner-repo` by default, but if your `.claude-plugin/marketplace.json`
sets its own `"name"` field, use that value instead.

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

## Tools

The In Case of Crisis connector currently exposes two tools. The skill uses
them in sequence: search first, then fetch the one protocol that matches.

| Tool | What it does |
|---|---|
| `list_crisis_protocols` | Searches your organization's approved crisis, emergency, and incident-response material — protocols, playbooks, and preparedness plans — and returns the matching options. |
| `get_crisis_protocol` | Returns the full procedure text, escalation contacts, and citation for a single protocol. |

**`list_crisis_protocols` inputs** (all optional)

- `query` — the situation in the user's own words. Omit it to browse the
  whole catalogue.
- `protocol_type` — `All` (the default), `Custom` (your organization's own
  plans), or `Sponsored` (curated by In Case of Crisis, with a citation).

**`get_crisis_protocol` inputs**

- `event_id` — required. Taken from the `list_crisis_protocols` result. Two
  plans can share a name, so the ID is what selects the protocol.
- `asked` — the user's original words, so the connector's life-safety check
  evaluates what was actually asked.
- `name` — informational only.

Both tools also accept an optional `model` field, used only as audit
metadata.

*Tool set last verified October 7, 2026. The connector defines these tools,
not this plugin, so they can change independently of the plugin's version.*

## Security and privacy

- **No credentials or tokens are bundled** with this plugin. `.mcp.json`
  points at In Case of Crisis's public gateway URL, but authentication still
  happens per installer through their own OAuth consent — the URL alone
  grants no access.
- **Data stays with the installer's own account.** This plugin does not
  bundle, cache, or transmit any organization's protocol content on its
  own behalf.
- **Trigger scope is intentionally narrow**, limited to workplace
  physical-safety situations, to avoid misrouting unrelated language from
  end users into this connector.

## Versioning

This plugin follows the version pinned in `plugin.json`. Marketplace
installs check for updates automatically; installs from a downloaded
`.plugin` Release asset don't — reinstall from a newer release when one's
available.

## Support

Contact your RockDove Solutions account representative for setup help or to
report an issue with this plugin.

## License

MIT — see [LICENSE](./LICENSE).
