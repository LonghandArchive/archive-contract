# Archive Contract

The specification of what collectors in The Longhand Archive produce, and what platforms built on top of those archives can rely on consuming.

For context on The Longhand Archive as a whole, see the [organisation profile](https://github.com/longhandarchive).

## Status

In early drafting. Version 0.1 of the contract is being written based on the shape of the first concrete collector, `civilservicejobs-collector`. The contract will stabilise once a second collector exists and the generalisable patterns are proven.

## Why this repository exists

The Longhand Archive separates two concerns: the capture of public sector data (collectors) and the derivation of queryable or analytical views from that data (platforms). The boundary between them is defined here.

Without an explicit contract, the boundary drifts. Collectors produce whatever shape is convenient at the time; platforms reach into collector internals that were never meant to be external interfaces; changes in either repository silently break the other. A versioned, published specification prevents this by giving both sides an interface to produce to and consume from — and a shared language for changing it deliberately.

## What the contract specifies

The contract defines the shape of a collector's archive on disk: the directory layout, the file formats, the field schemas for records and events, the expected invariants (append-only event logs, content-addressed assets, immutable history snapshots), and the provenance metadata that ties captured data to the run that produced it.

The contract is the *only* interface through which a platform consumes a collector's output. Platforms do not read collector state, configuration, logs, or implementation details. Collectors do not adjust their output to accommodate platform preferences. Changes to what either side relies on are changes to the contract.

## What the contract does not specify

The contract does not specify how a collector captures its data. Scraping strategy, authentication, rate limiting, parsing, retry logic — all of these are internal to the collector and free to vary. The contract governs the output of that work, not the work itself.

The contract does not specify how a platform projects archives into derived forms. Database schema, query patterns, redaction strategies, presentation — all of these are internal to the platform. The contract governs what the platform reads from, not what it produces.

The contract does not mandate a single collector implementation language or framework. Any tool that produces a conforming archive is a conforming collector.

## Versioning

The contract is versioned. Each published version is immutable once released; changes produce a new version, not a revision of an existing one.

Collectors and platforms declare the contract version they conform to. During transitions, a platform may support multiple contract versions concurrently while collectors migrate. A collector and a platform that both claim conformance to the same version can be assumed to interoperate.

The versioning discipline is strict by design. A specification that silently changes is worse than no specification at all, because it creates the illusion of stability while removing it. The cost of a new version number is small; the cost of undetected drift is large.

## Repository structure

*To be populated as the contract takes shape. Expected contents include the versioned specification documents, JSON schemas for record and event formats, example archive structures drawn from real collector output, and a CHANGELOG recording the evolution of the contract across versions.*

## Relationship to other repositories

- [`civilservicejobs-collector`](https://github.com/longhandarchive/civilservicejobs-collector) — the first concrete collector. Its current output is the reference implementation from which version 0.1 of the contract is being drawn.
- [`platform`](https://github.com/longhandarchive/platform) — the first consumer of archives produced under this contract. Its sync layer reads collector archives only through the shape guaranteed here.
- [`governance`](https://github.com/longhandarchive/governance) — cross-cutting decisions that apply across the organisation, including the licensing rule for documentation repositories and the personal data redaction policy at the projection boundary.

## Licence and contribution

This repository is available under [Creative Commons Attribution 4.0 International](./LICENSE). Read, quote, adapt, and reuse the specification with attribution.

External contribution to the contract is not currently accepted. See [`CONTRIBUTING.md`](./CONTRIBUTING.md) for the current posture and the channels available for discussion.

## Contact

This is a personal project by [Andrew Allen](https://www.linkedin.com/in/andrewallen), undertaken in a personal capacity. It is not affiliated with or endorsed by any UK government department or any employer.
