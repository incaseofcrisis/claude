# In Case of Crisis

Surfaces an organization's own approved crisis, emergency, and
incident-response protocols the moment a workplace safety situation comes
up in conversation.

## Components

- **Skill** — `skills/in-case-of-crisis/` — teaches Claude when to call the
  In Case of Crisis connector (fire, severe weather, medical emergency,
  security threat, evacuation, lockdown, etc.) and how to browse or fetch a
  specific protocol from it.
- **MCP server** — `.mcp.json` — references the "In Case of Crisis"
  connector from Claude's connector directory by name.

## Setup

Each person who installs this plugin connects their own In Case of Crisis
account — Claude prompts for that the first time the connector's tools are
used. No API keys, tokens, or hostnames are bundled with this plugin: the
connector's endpoint is dynamic and resolved per-account, not a fixed URL.

**Prerequisite:** the installer needs an existing In Case of Crisis account
with their organization's protocols loaded. Without one, the plugin has
nothing to connect to — it does not ship or embed any protocol content of
its own.

**First use:** the first time the skill calls the connector, Claude will
prompt the installer to authorize their In Case of Crisis account (a
one-time OAuth consent). After that, it's transparent — this is a standard
step for OAuth-gated connectors, not specific to this plugin.

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
- **Verify the name-only `.mcp.json` reference before distributing.** The
  connector is referenced by name (no `url`/`type`) because it's a
  dynamic-endpoint directory server rather than a static remote server.
  Confirm this resolves correctly in your target install environment
  (`claude plugin validate`, or a real test install that surfaces the
  connector's authorization prompt) before shipping to clients.
