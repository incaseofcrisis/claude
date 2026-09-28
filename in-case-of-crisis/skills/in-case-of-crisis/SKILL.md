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

Then:

- If `list_crisis_protocols` returns one option that clearly matches the
  situation, call `get_crisis_protocol` with that option's exact `name`
  and `event_id`, and pass the user's original wording as `asked`.
- If it returns two or more plausible options, or the user asked to browse
  the full plan, call `show_crisis_protocol_list` with the *same* `query`
  and `protocol_type` values used in the `list_crisis_protocols` call, and
  let the user pick from the card. Do not also re-list the options in
  prose.
- If nothing returned is a good match, say so plainly rather than
  substituting general knowledge.

Relay the protocol's guidance as returned. Do not paraphrase or summarize
safety-critical steps in a way that could change their meaning or drop a
step.
