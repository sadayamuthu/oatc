<div align="center">

# OATC

<h3>Open AI Threat Catalog</h3>

[![Status](https://img.shields.io/badge/status-design%20stage-orange?style=flat-square)](ROADMAP.md)
[![Go 1.26+](https://img.shields.io/badge/go-1.26+-00ADD8?style=flat-square)](https://go.dev/dl/)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue?style=flat-square)](LICENSE)

---

[Thesis](THESIS.md) · [Roadmap](ROADMAP.md) · [Contributing](CONTRIBUTING.md) · [Security](SECURITY.md)

</div>

---

## What is OATC?

One machine-readable catalog of threats to AI systems. OATC merges the OWASP
Top 10 for LLM Applications, the OWASP Top 10 for Agentic Applications and
MITRE ATLAS into a single JSON catalog, cross-maps the entries to each other,
and maps each threat to the NIST SP 800-53 controls that mitigate it, using
[OCBC](https://github.com/sadayamuthu/ocbc).

> **Status: design stage.** There is no published catalog yet. The schema and
> examples below are the proposal, and they will change. Part of the
> [OpenAstra](https://openastra.org) research agenda, area VII: AI Threat
> Modeling & Risk Assessment.

---

## The problem

The three main AI threat lists overlap, use different identifiers, and are
published as web pages and spreadsheets. To answer "which controls cover
indirect prompt injection?" today, someone reads all three and builds a
mapping by hand, and every team builds a slightly different one. Tools can't
share findings because they don't share identifiers.

---

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

---

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

---

## Distribution (planned)

- `oatc.json`, rebuilt daily from the upstream sources, published as a release
  asset with a checksum
- Zero install: fetch one URL, no API key
- A Python and a TypeScript loader with typed models
- A changelog per build, so downstream tools see when a mapping changed

---

## Design principles

- **Same shape as OCBC and OEBC**, so the three catalogs can be joined.
- **Every mapping is reviewable.** Each cross-map and control mapping has a
  rationale and lives in a plain file that a PR can change.
- **Upstream wins.** OATC adds identifiers and mappings; it never rewrites
  the source frameworks' text.

---

## Roadmap

The plan, from the first working version to 1.0, is in [ROADMAP.md](ROADMAP.md). The reasoning behind the project, and what would make us stop, is in [THESIS.md](THESIS.md).

---

## Related OpenAstra projects

- [OCBC](https://github.com/sadayamuthu/ocbc): the control catalog OATC maps to
- [OEBC](https://github.com/sadayamuthu/oebc): the exposure catalog with the same build model
- [ThreatDiff](https://github.com/sadayamuthu/threatdiff): the first consumer

---

## Contributing

Design feedback, real-world cases and fixes are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for how to help while the project is at the design stage, and [GOVERNANCE.md](GOVERNANCE.md) for how decisions are made.

---

## Security

Please report vulnerabilities privately through [GitHub security advisories](https://github.com/sadayamuthu/oatc/security/advisories/new), not in a public issue. See [SECURITY.md](SECURITY.md) for what to include and what's in scope.

---

## License

[Apache License 2.0](LICENSE)

The catalog's own identifiers, cross-maps and mappings are under the same license. Text and identifiers imported from upstream sources (OWASP, MITRE ATLAS, NIST) remain under their own terms.

---

<div align="center">

**OATC: Open AI Threat Catalog**

OATC is managed by [OpenAstra](https://openastra.org)

[GitHub](https://github.com/sadayamuthu/oatc) · [Thesis](THESIS.md) · [Roadmap](ROADMAP.md)

</div>
