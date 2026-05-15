# Changelog

All notable changes to scry-spec will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.3] - 2026-05-15

### Changed

- FR4: `implements` and `supersedes` fields are now formally specified as arrays (`[]` default), not scalars (`null`). Conforming parsers MUST reject scalar values for these fields. Aligns spec with both reference implementations (scry-parse-ts v1.0.6, scry-parse-py v1.0.6) which already enforced array form.

## [1.0.2] - 2026-05-15

### Clarified

- FR11.7: added a non-normative note on host-language string-literal exclusion, distinguishing parsers that declare host-language support (expected to exclude that language's string literals) from pure-markdown parsers (conformant without host-language detection).
- FR11.7: added a normative "Behavior on match" clause — marker syntax inside an inert region MUST produce zero records and MUST NOT emit diagnostics, regardless of syntactic completeness.

No conformance change; both clarifications document already-implemented reference behavior.

## [1.0.1] - 2026-05-15

### Added

- FR11.7 (Inert Context Detection): parsers MUST NOT extract markers from fenced code blocks or inline code spans; SHOULD NOT extract from host-language string literals. Codifies behavior already implemented in scry-parse v1.0.4.
- Tests 20–22 covering inert-context detection.

## [1.0.0] - 2026-05-14

### Added

- Initial release of scry-spec.
- Marker taxonomy: `@scry.entry`, `@scry.anchor`, `@scry.bind`.
- Two semantic categories: declarative markers and binding markers.
- 14 functional requirements (FR1–FR14) covering syntax, parsing, references, kinds, statuses, relationships, and soft references.
- Baseline kinds: design, pattern, spec, lesson, internal, task, milestone, report, audit, research, code.
- Baseline statuses: draft, active, deprecated.
- Loose-mode and strict-mode reference resolution.
- Comment field on bindings (single-line or block form).
- Soft references explicitly defined as out-of-scope formal references.
