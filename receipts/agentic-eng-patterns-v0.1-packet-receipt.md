# Receipt — Agentic Engineering Patterns v0.1 Packet

This receipt records what was produced for the v0.1 agentic engineering patterns
packet, which issues it closes, and the non-canon posture. It is referenced by
the example and fixtures via `receiptRequirements.receiptPath`.

## Produced artifacts

- `docs/v0.1-boundary.md` — scope, non-goals, adoption boundary, review
  expectations, non-canon posture, required packet pieces, adjacent repo links.
- `docs/prior-art.md` — public prior art, adjacent ecosystem, vocabulary, and
  key concepts.
- `schemas/agentic-eng-patterns-v0.1.json` — JSON Schema for a v0.1 packet.
- `examples/agentic-pattern-packet-v0.1.example.json` — a valid, human-readable
  example packet.
- `fixtures/valid/agentic-pattern-packet-v0.1.valid.json` — a minimal valid
  fixture that must pass schema validation.
- `fixtures/invalid/agentic-pattern-packet-v0.1.invalid.json` — an invalid
  fixture that must fail schema validation because it omits the required
  `patternContract` field.

## Closes issues

- #1 — Define v0.1 scope and boundary.
- #2 — Collect prior art and adjacent ecosystem references.
- #3 — Design minimal schema/examples layout.

## Provenance

- Provenance: `public`.
- No private, internal, or secret operational content is included.
- No vendor concept is canonized. All named projects are referenced, not
  endorsed.

## Non-canon posture

This packet is **candidate namespace only**. `authority.posture` is `non-canon`
and `authority.reviewState` is `unreviewed`. Nothing here is adopted guidance.
Adoption requires a reviewed governance path that does not yet exist in this
repository.

## Validation expectations

- The valid fixture must validate against
  `schemas/agentic-eng-patterns-v0.1.json`.
- The invalid fixture must fail validation with an error naming the missing
  required property `patternContract`.
- The example packet must validate against the schema and is the canonical
  human-readable illustration of a v0.1 packet.
