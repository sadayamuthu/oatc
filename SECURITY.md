# Security Policy

## Reporting a vulnerability

Please don't report security problems in a public issue, pull request or
discussion. Use
[**Report a vulnerability**](https://github.com/sadayamuthu/oatc/security/advisories/new)
on the repository's Security tab instead. Only the maintainers can see the
report.

Include what you can of:

- the OATC version (`oatc version`) or commit, your Go version and OS
- how OATC was used, and its configuration with secrets removed
- steps to reproduce
- what happened and what you expected

You'll get a reply when the report has been read, and again when a fix is
ready. A fix ships as a patch release; the advisory names you unless you'd
rather it didn't.

## Supported versions

OATC is at the design stage and has no releases yet. Once it does,
fixes land in the latest release only, until 1.0.

## What counts

OATC is a data catalog built daily from public upstream sources and published as a release asset with a checksum.

OATC is a security tool, so anything that breaks one of these promises
is a security issue:

- **The published catalog matches its checksum and its sources.** A way to get altered content into a release, or a release that doesn't match its build, is in scope.
- **The build reads only the listed upstream sources.** A build step that fetches or runs anything else is in scope.

These are by design, and not vulnerabilities:

- A mapping you disagree with is a bug or a discussion, not a vulnerability. Open an issue or a pull request.
- Upstream text is reproduced as published; errors in it belong upstream.

A wrong result that isn't covered above is a bug, not a vulnerability. Report
it in a normal issue; see [CONTRIBUTING.md](CONTRIBUTING.md).
