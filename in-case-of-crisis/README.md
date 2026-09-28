# In Case of Crisis

Surfaces an organization's own approved crisis, emergency, and
incident-response protocols the moment a workplace safety situation comes
up in conversation.

## Components

- **Skill** — `skills/in-case-of-crisis/` — teaches Claude when to call the
  In Case of Crisis connector (fire, severe weather, medical emergency,
  security threat, evacuation, lockdown, etc.) and how to browse or fetch a
  specific protocol from it.

This plugin does not bundle an MCP server config. In Case of Crisis is a
directory-listed connector app with a dynamic, OAuth-gated endpoint — those
are connected through Claude's own connector flow, not declared in a
plugin's `.mcp.json`. This is a skill-only plugin by design, not an
omission.

## Setup

Installing this plugin does not connect In Case of Crisis for you — it only
adds the skill. Each person connects their own In Case of Crisis account
separately, through Claude's connector directory (Settings → Connectors),
or via the connect prompt Claude surfaces automatically the first time the
skill reaches for a tool that isn't connected yet.

**Prerequisite:** the installer needs an existing In Case of Crisis account
with their organization's protocols loaded. Without one, the connector has
nothing to connect to — this plugin does not ship or embed any protocol
content of its own.

**First use:** the first time the skill calls the connector, expect a
one-time OAuth consent prompt for that account. After that, it's
transparent — standard for OAuth-gated connector apps generally, not
specific to this plugin.

## Usage

Ask about a workplace safety situation — "there's a fire on the 3rd floor,"
"what's our severe weather protocol," "walk me through our lockdown plan" —
and the skill routes it to the connector automatically.

## Notes for distributors

- **Data stays with the installer's own account.** This plugin doesn't
  bundle or embed any specific organization's protocol content — each
  client sees only the protocols connected under their own In Case of
  Crisis account, not RockDove's.
- **Trigger scope is intentionally narrow.** The skill fires on workplace
  physical-safety situations, not general business incidents or personal
  difficulties, to avoid misrouting unrelated "crisis" language from end
  users into this connector.
- **Test the connect prompt before distributing.** Because this plugin
  doesn't declare the connector, confirm — with a real install — that
  Claude actually offers to connect In Case of Crisis when the skill fires
  for someone who hasn't connected it yet. Don't assume; verify.
