# Changelog

All notable changes to scry-spec will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.1] - 2026-05-15

### Added

- FR11.7: Code-construct exclusion. Parsers MUST NOT extract markers from fenced code blocks (``` and ~~~ delimiters), inline code spans (Markdown), source-language string literals (JS/TS/JSX/TSX), and Python triple-quoted strings. Markers inside these constructs MUST be silently ignored.

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
