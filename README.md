# OATC: Open AI Threat Catalog

One machine-readable catalog of threats to AI systems. OATC merges the OWASP
Top 10 for LLM Applications, the OWASP Top 10 for Agentic Applications and
MITRE ATLAS into a single JSON catalog, cross-maps the entries to each other,
and maps each threat to the NIST SP 800-53 controls that mitigate it, using
[OCBC](https://github.com/sadayamuthu/ocbc).

> **Status: design stage.** There is no published catalog yet. The schema and
> examples below are the proposal, and they will change. Part of the
> [OpenAstra](https://openastra.org) research agenda, area VII: AI Threat
> Modeling & Risk Assessment.

## The problem

The three main AI threat lists overlap, use different identifiers, and are
published as web pages and spreadsheets. To answer "which controls cover
indirect prompt injection?" today, someone reads all three and builds a
mapping by hand, and every team builds a slightly different one. Tools can't
share findings because they don't share identifiers.

## What's in it

- **Threats** with a stable OATC ID, a name, a description and the source
  entries they come from
- **Cross-maps** between OWASP LLM, OWASP Agentic and ATLAS identifiers, each
  marked `equivalent`, `broader`, `narrower` or `related`
- **Control mappings** to NIST SP 800-53 Rev. 5 controls in OCBC, each with a
  short rationale
- **Detection hints** that tools such as [ThreatDiff](https://github.com/sadayamuthu/threatdiff)
  use to recognise a threat in a configuration or a trace
- **Provenance** for every entry: source URL, source version, date retrieved

## Example entry (proposed)

```json
{
  "id": "OATC-0007",
  "name": "Indirect prompt injection via retrieved content",
  "sources": [
    { "framework": "owasp-llm-2025", "id": "LLM01", "relation": "narrower" },
    { "framework": "mitre-atlas", "id": "AML.T0051.001", "relation": "equivalent" },
    { "framework": "owasp-agentic", "id": "goal-hijack", "relation": "related" }
  ],
  "controls": [
    { "id": "AC-4", "rationale": "Untrusted content must not flow into privileged instructions." },
    { "id": "SI-10", "rationale": "Validate content entering the agent's context." }
  ],
  "detection": { "graph": "untrusted-source -> context -> sensitive-sink" },
  "provenance": { "retrieved": "2026-11-16" }
}
```

## Distribution (planned)

- `oatc.json`, rebuilt daily from the upstream sources, published as a release
  asset with a checksum
- Zero install: fetch one URL, no API key
- A Python and a TypeScript loader with typed models
- A changelog per build, so downstream tools see when a mapping changed

## Design principles

- **Same shape as OCBC and OEBC**, so the three catalogs can be joined.
- **Every mapping is reviewable.** Each cross-map and control mapping has a
  rationale and lives in a plain file that a PR can change.
- **Upstream wins.** OATC adds identifiers and mappings; it never rewrites
  the source frameworks' text.

## Roadmap

1. Schema and identifier scheme
2. Importers for OWASP LLM Top 10, OWASP Agentic Top 10 and MITRE ATLAS
3. Cross-maps and first control mappings to OCBC
4. Daily build and release
5. Loaders and detection hints

## Related OpenAstra projects

- [OCBC](https://github.com/sadayamuthu/ocbc): the control catalog OATC maps to
- [OEBC](https://github.com/sadayamuthu/oebc): the exposure catalog with the same build model
- [ThreatDiff](https://github.com/sadayamuthu/threatdiff): the first consumer

## License

To be decided before the first release. Licensing must respect the terms of
each upstream source.
