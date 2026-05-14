# scry-spec

The scry marker contract — a structured metadata convention for AI-augmented code and documentation.

scry-spec defines a portable marker format that can be embedded in any text file (markdown, source code, configs, etc.) to declare artifact identity, purpose, and traceable relationships between specifications and implementations. It is implementation-agnostic: any tool that reads or writes scry markers can interoperate with any other, regardless of storage backend, query interface, or tooling.

## What scry markers enable

A single scry marker in a source file creates **bidirectional traceability**: tools and agents can answer questions like:

- *"What code implements this requirement?"*
- *"Which test verifies this scenario?"*
- *"Where is this design decision applied?"*
- *"What's the rationale behind this code?"*

…by following lightweight pointers between source code and documentation.

## Repository structure

```
scry-spec/
├── README.md       # This file
├── CHANGELOG.md    # Cross-version change history (Keep a Changelog format)
├── head.md         # Symlink to the latest spec version (possibly unstable)
├── lts.md          # Symlink to the current LTS version
└── v1.0.md         # scry-spec v1.0.x (current LTS and HEAD)
```

### Version policy

scry-spec follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html) with one document per major.minor line:

- **MAJOR** version bump (`v2.0.md`): breaking change — existing markers parse or validate differently.
- **MINOR** version bump (`v1.2.md`): new feature added (e.g., new optional field, new marker kind) — backward compatible.
- **PATCH** version bump: clarifications, typos, examples — the file is edited in place and the metadata version bumped. Git tags capture patch-level immutability.

### Pointers

- **`head.md`**: symlink to the latest spec file. Always points to the most recent version. May be unstable while a new version is being drafted.
- **`lts.md`**: symlink to the designated long-term support version. Implementations targeting stability should pin to whatever `lts.md` points to at the time of integration.

Update these symlinks when promoting a new version to HEAD or designating a new LTS.

## How to use this spec

### As an implementor

1. Read `lts.md` (or whichever version you wish to target).
2. Implement parsing and semantics per the functional requirements (FR1–FRn).
3. Declare conformance by referencing the version you implement (e.g., "implements scry-spec v1.0").

The spec is intentionally backend-agnostic. You may store, query, search, and present marker data however suits your use case — the contract is the marker format and parsing rules, not the implementation strategy.

### Authorship

Scry markers are typically written by AI agents working on a codebase, not by humans directly. Agents generate markers when:

- Creating new documents (design, spec, pattern, etc.) — the agent emits an `@scry.entry` block
- Implementing a spec requirement — the agent emits an `@scry.bind` line connecting code to spec
- Marking a notable point in a file — the agent emits an `@scry.anchor`

Humans usually interact with markers indirectly: through tools that surface marker-indexed data (search, hover, navigation), or by reviewing agent output during code review. Implementations should optimize for agent authorship patterns (mint tools that produce templates, validation that catches common agent mistakes, query interfaces that expose marker metadata to other agents).

Direct human authoring is supported but not the primary use case. The marker syntax is intentionally simple enough that humans can write markers when needed, but agents — generating markers as a side effect of their work — are the dominant authors in practice.

## Versioning and stability

When implementing tools:
- **For long-lived projects**: target `lts.md` for stability across spec revisions.
- **For early adoption or experimentation**: target `head.md` for the latest features.
- **For published packages**: pin to a specific version (e.g., `v1.0.md`) to make compliance claims unambiguous.

The CHANGELOG tracks all changes across versions, including patches.

## Contributing

scry-spec evolves through observation, not prescription. New baseline kinds, statuses, or features are typically added when ecosystem usage has converged on a clear convention. Proposed changes should:

1. Demonstrate existing usage across multiple implementations or projects.
2. Have minimal impact on existing markers (prefer additive changes for minor versions).
3. Avoid coupling the spec to any specific storage backend, tool surface, or workflow.

Breaking changes are reserved for major version bumps and require migration guidance in the CHANGELOG.

## License

MIT
