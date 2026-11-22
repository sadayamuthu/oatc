# OATC: thesis

**In one line:** AI security tools can't share findings until they share
identifiers, and one open, machine-readable catalog of AI threats fixes that.

## The problem

OWASP LLM Top 10, OWASP Agentic Top 10 and MITRE ATLAS overlap, use
different identifiers, and ship as web pages and spreadsheets. Every team
that needs "which controls cover indirect prompt injection?" builds its own
mapping by hand, and the mappings disagree.

## The bet

1. **The missing piece is plumbing, not content.** The frameworks are good;
   what's missing is stable IDs, explicit cross-maps and control mappings in
   one JSON file a tool can fetch.
2. **Reviewable mappings earn trust.** Every cross-map and control mapping
   has a rationale and lives in a plain file a PR can change, so experts
   correct it instead of rebuilding it.
3. **Same shape as OCBC and OEBC** lets threats, controls and exposures be
   joined, which is where the value compounds.
4. **Upstream wins.** OATC adds IDs and links and never rewrites the source
   text, so it stays a complement to the frameworks, not a competitor.

## Why now

The agentic threat lists are new and still moving, compliance teams are
being asked to map AI risks to controls like NIST SP 800-53, and a growing
number of tools (ThreatDiff first) need machine-readable labels.

## What success looks like

- The daily build runs reliably and the changelog shows each upstream change.
- ThreatDiff and at least one tool outside OpenAstra label findings with
  OATC IDs.
- External contributors propose and review mapping changes.

## What would prove us wrong

- Upstream licences or formats make a faithful daily rebuild impractical.
- The frameworks converge on shared identifiers themselves.
- Nobody consumes the catalog, so mappings go unreviewed and drift.

## Not a bet on

Writing new threat taxonomy or replacing the upstream frameworks.

## Where it fits

Area VII, AI Threat Modeling & Risk Assessment. Maps to
[OCBC](https://github.com/sadayamuthu/ocbc); consumed by
[ThreatDiff](https://github.com/sadayamuthu/threatdiff).
