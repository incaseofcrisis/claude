<h1 align="center"><img src="./assets/in-case-of-crisis-logo.png" width="32" align="absmiddle"> In Case of Crisis — Claude Plugin &amp; Connector</h1>

<p align="center">
  <img src="https://img.shields.io/badge/version-0.1.0-203864" alt="version 0.1.0">
  <img src="https://img.shields.io/badge/platform-Claude.ai%20%7C%20Desktop%20%7C%20Cowork%20%7C%20Code-3E91C5" alt="Claude.ai | Claude Desktop | Claude Cowork | Claude Code">
  <img src="https://img.shields.io/badge/status-active-27AE60" alt="status active">
  <img src="https://img.shields.io/badge/license-MIT-3E91C5" alt="license MIT">
</p>

<p align="center"><img src="./assets/rockdove-logo.png" width="18" align="absmiddle"> <em>Built by RockDove Solutions</em></p>

---

## What this is

Two ways to give Claude access to your organization's In Case of Crisis
protocols:

| Setup | Best for | Where it works |
|---|---|---|
| [**Plugin**](#plugin-setup) | Teams that want the connector *and* a skill that tells Claude when to use it, installed in one step. | Claude Cowork, Claude Code |
| [**Connector only**](#connector-only-setup) | Teams that just want the connector added to Claude, with no plugin or code. | Claude.ai, Claude Desktop, Cowork |

Both use the same hosted connector and the same per-person sign-in, so
either way Claude only sees the protocols published for the signed-in
person's organization.

### The plugin

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

## Plugin setup

### Install

#### Claude Cowork

**Recommended — add as a marketplace:**

1. Open **Customize → Plugins → Browse plugins**.
2. Add this repository as a marketplace source: `incaseofcrisis/claude`.
3. Install **In Case of Crisis** from the catalog.

**Quick trial installs (no marketplace setup):** download the packaged
`.plugin` file from this repo's [Releases page](../../releases) and drag it
into the Cowork sidebar, or open it from a chat. Confirm the install when
prompted. Use this path for one-off trial installs; it won't receive
update notifications the way a marketplace install does.

#### Claude Code

```
/plugin marketplace add incaseofcrisis/claude
/plugin install in-case-of-crisis@incaseofcrisis-claude
```

The identifier after `@` is the marketplace's *name*, not its repo path — Claude
Code derives it as `owner-repo` by default, but if your `.claude-plugin/marketplace.json`
sets its own `"name"` field, use that value instead.

### Prerequisite

An active **In Case of Crisis** account with your organization's protocols
already loaded. Without one, the plugin has nothing to connect to.

### First use

The first time the skill calls the connector, Claude prompts you to
authorize your In Case of Crisis account — a one-time OAuth consent. After
that, it's transparent. This is standard for OAuth-gated connectors, not
specific to this plugin.

### Usage

Ask about a workplace safety situation in plain language:

- "There's a fire on the 3rd floor."
- "What's our severe weather protocol?"
- "Walk me through our lockdown plan."

The skill routes the request to your organization's own protocol data
automatically.

## Connector-only setup

Use this path to add just the In Case of Crisis MCP connector to Claude,
without the plugin. It takes about 3 minutes per person and needs no
installation or code. On Team and Enterprise plans an Owner adds the
connector once before anyone else can connect.

> **In a life-threatening emergency, call 9-1-1 first.** The connector
> returns your organization's approved guidance. It does not contact
> emergency services, send notifications, or file incident reports; use the
> In Case of Crisis app for those actions.

The connector is read-only. Each person signs in with their own In Case of
Crisis account, so Claude only sees the protocols published for that
person's organization and never sees their In Case of Crisis password.

### Before you start

- Your organization has an active In Case of Crisis subscription, and
  RockDove Solutions has enabled the MCP connector for it. Your Customer
  Success Manager (CSM) can confirm both.
- You have your In Case of Crisis sign-in (the same email and password, or
  Login with Microsoft, that you already use).
- You use Claude.ai in a browser, Claude Desktop, or Cowork on any plan.
  The Free plan allows one custom connector.
- **Team or Enterprise:** an Owner has already added the connector
  (Part 1 below), or you are that Owner.
- You have the connector address:

```
https://mcpgateway.incaseofcrisis.com/mcp
```

### Part 1: Owner setup (Team and Enterprise only)

Only Owners and Primary Owners can add connectors on a Team plan. On
Enterprise, a custom role with permission to manage connectors can also add
them. Free, Pro, and Max users skip to Part 2, Option A.

1. Open **Organization settings → Connectors** and select **Add**.
2. Hover over **Custom**, then select **Web**.
3. Enter the name `In Case of Crisis MCP`, paste the connector address, and
   select **Continue**.
4. Keep the authentication settings Claude detects and select **Continue**.
   **Leave Request headers empty.** In Case of Crisis uses individual
   sign-in, and a fixed credential here would be shared by every member who
   uses the connector.
5. Select **Add**. The connector now appears for members with a *Custom*
   label.

### Part 2: Connect your account (everyone)

**Option A: Free, Pro, and Max.** You add the connector yourself.

1. Open **Customize → Connectors** in Claude.ai or Claude Desktop.
2. Select **+ Add**, then **Add custom connector**.
3. Enter the name `In Case of Crisis MCP`, paste the connector address, and
   select **Continue**.
4. Keep the detected authentication settings, choose **Sign in now**, and
   select **Add**.
5. Sign in to In Case of Crisis in the window that opens, then select
   **Allow**.

**Option B: Team and Enterprise members.** Your Owner has already added the
connector.

1. Open **Customize → Connectors** and find **In Case of Crisis MCP**
   (labelled *Custom*).
2. Select **Connect**.
3. Sign in to In Case of Crisis in the window that opens, then select
   **Allow**.

Then, in any chat:

1. Select the **+** button at the lower left of the message box, then
   **Connectors**.
2. Switch on **In Case of Crisis MCP**. The toggle applies per conversation.

You can disconnect at any time from **Customize → Connectors**.

### Verify the connection

Start a new chat with the connector switched on and ask one of these:

- "Using In Case of Crisis MCP, show me our approved crisis protocols."
- "What does our plan say to do during a flash flood?"
- "Someone smells gas in the break room. What does our plan say?"

The first time, Claude may ask permission to use the tool; select **Allow**.
Claude can show the protocol catalog as an interactive list. A working
answer leads with your plan, keeps the steps in the plan's order, and ends
with a citation.

### Rollout notes

- **Connect before you need it.** Each person signs in once. Have employees
  complete Part 2 during onboarding, not during an incident.
- **Name the connector in your question.** Claude decides when to use a
  connector. Starting with "Using In Case of Crisis MCP" makes that decision
  for it. (The plugin's skill does this routing automatically.)
- **Mobile.** Add and connect from Claude.ai or Claude Desktop. Confirm the
  connector is available in the Claude mobile app before relying on it
  there.
- **Missing protocol.** The catalog contains your organization's published
  protocols. If one you expect is missing, contact your CSM.

### Connector troubleshooting

| Symptom | Action |
|---|---|
| No **Add custom connector** option | Ask your Owner (Team or Enterprise) or update Claude Desktop. |
| Free plan will not add it | Free allows one custom connector. Remove an unused one first. |
| Sign-in window does not open | Select **Connect** on **Customize → Connectors** again. |
| Organization login not shown | Choose **Login with Microsoft** if your organization uses Microsoft Entra for In Case of Crisis. |
| Claude answers without your plan | Switch the connector on under **+ → Connectors** and name it in the question. |
| A protocol you expect is missing | Contact your CSM; it may not be published to your organization yet. |
| Signed in but access stops | Contact support. Do not delete and recreate the connector. |

Still stuck? See [Support](#support).

*Based on the In Case of Crisis MCP Connector install guide for Claude,
v4.0 (October 27, 2026).*

## Tools

The In Case of Crisis connector currently exposes two tools, whether you
install it through the plugin or on its own. They are used in sequence:
search first, then fetch the one protocol that matches.

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

- **No credentials or tokens are bundled** with this plugin, and none should
  be entered when adding the connector by hand (leave Request headers
  empty). `.mcp.json`
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

The plugin follows the version pinned in `plugin.json`. Marketplace
installs check for updates automatically; installs from a downloaded
`.plugin` Release asset don't — reinstall from a newer release when one's
available.

## Support

Email support@incaseofcrisis.com for setup help or to report an issue, for
either the plugin or the connector-only setup. For connector setup, mention
"In Case of Crisis MCP connector setup — Claude." Your Customer Success
Manager (CSM) can also confirm whether the connector is enabled for your
organization. See also [Connector troubleshooting](#connector-troubleshooting).

## License

MIT — see [LICENSE](./LICENSE).
