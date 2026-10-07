---
name: in-case-of-crisis
description: >
  This skill should be used when the user describes an active or imminent
  workplace safety situation — a fire, severe weather, medical emergency,
  security threat, evacuation, lockdown, or other event calling for an
  organization's approved emergency response — or explicitly asks for
  "our crisis plan," "the emergency protocol," "the safety plan," "the
  incident response procedure," or similar. Not for general business
  incidents (outages, PR issues) or personal difficulties unrelated to
  physical workplace safety — only for situations calling on the
  organization's own approved crisis/safety protocols.
metadata:
  version: "0.1.0"
---

Call the In Case of Crisis connector's `list_crisis_protocols` tool first,
before answering from general knowledge or memory. Pass the situation in
the user's own words as `query`. Never guess at protocol content or invent
steps — this connector is the source of truth.

- To browse the organization's whole plan, call `list_crisis_protocols`
  with no `query`.
- Set `protocol_type` only when the user names a type: `Custom` for the
  organization's own plans, `Sponsored` for In Case of Crisis-curated
  protocols that carry a citation. Otherwise leave it unset.

Then:

- If one option clearly matches the situation, call `get_crisis_protocol`
  with that option's `event_id` and pass the user's original wording as
  `asked`. The `event_id` is the only thing that selects the protocol — two
  plans can share a name — so never substitute `name` for it.
- If two or more options plausibly match, list their names in your reply
  and ask which one the user means, then call `get_crisis_protocol` with
  the chosen option's `event_id`.
- If nothing returned is a good match, say so plainly rather than
  substituting general knowledge.

Leave the optional `model` field unset rather than guessing a value; it is
audit metadata only.

Relay the protocol's guidance as returned, including its escalation
contacts and citation. Do not paraphrase or summarize safety-critical steps
in a way that could change their meaning or drop a step.
