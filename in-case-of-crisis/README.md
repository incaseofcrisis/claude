# In Case of Crisis

Surfaces an organization's own approved crisis, emergency, and
incident-response protocols the moment a workplace safety situation comes
up in conversation.

## Components

- **Skill** — `skills/in-case-of-crisis/` — teaches Claude when to call the
  In Case of Crisis connector (fire, severe weather, medical emergency,
  security threat, evacuation, lockdown, etc.) and how to search for, and
  then fetch, the protocol that matches.
- **MCP server** — `.mcp.json` — connects to In Case of Crisis's hosted
  gateway (`https://mcpgateway.incaseofcrisis.com/mcp`) over Streamable
  HTTP.

## Setup

Installing this plugin adds both the skill and the connector reference.
Each installer still authorizes their *own* In Case of Crisis account the
first time it's used — the shared gateway URL doesn't skip that; it just
tells Claude where to connect.

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

## Tools

The connector currently exposes two tools, which the skill calls in
sequence — search first, then fetch the one protocol that matches:

- **`list_crisis_protocols`** — searches the organization's approved
  crisis, emergency, and incident-response material and returns matching
  options. Optional inputs: `query` (the situation in the user's own words;
  omit to browse the whole catalogue) and `protocol_type` (`All` by
  default, `Custom` for the organization's own plans, `Sponsored` for In
  Case of Crisis-curated protocols that carry a citation).
- **`get_crisis_protocol`** — returns the full procedure text, escalation
  contacts, and citation for one protocol. Requires `event_id` from the
  list result (two plans can share a name, so the ID is what selects the
  protocol). Also accepts `asked` (the user's original words, for the
  connector's life-safety check) and `name` (informational only).

Both tools also accept an optional `model` field, used only as audit
metadata.

Tool set last verified October 7, 2026. The connector defines these tools,
not this plugin, so they can change independently of the plugin's version.

## Notes for distributors

- **Data stays with the installer's own account.** This plugin doesn't
  bundle or embed any specific organization's protocol content — each
  client sees only the protocols connected under their own In Case of
  Crisis account, not RockDove's.
- **Trigger scope is intentionally narrow.** The skill fires on workplace
  physical-safety situations, not general business incidents or personal
  difficulties, to avoid misrouting unrelated "crisis" language from end
  users into this connector.
- **Verify the transport type before distributing.** `.mcp.json` uses
  `"type": "http"`, inferred from the URL ending in `/mcp` — this hasn't
  been confirmed against a real install. If the connection fails, try
  `"type": "sse"` instead. Confirm with a real test install that the
  OAuth prompt actually appears and the tools resolve correctly.
