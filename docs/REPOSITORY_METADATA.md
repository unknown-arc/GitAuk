# GitAuk Repository Metadata Specification

## Purpose

The `.gitauk/` directory provides repository-level information that GitAuk cannot always determine reliably from source files alone.

## Proposed Structure

```text
.gitauk/
├── project.json
├── files.json
├── mappings/
├── rules/
└── schema-version
```

This structure is a proposal and is not yet a stable contract.

## Requirements

Metadata should be:

- versioned,
- validated,
- readable,
- minimal,
- backward-compatible where practical,
- safe to process from untrusted repositories.

## `project.json`

Potential information:

```json
{
  "name": "example-project",
  "description": "Example project",
  "version": "1.0"
}
```

## `files.json`

Potential purpose:

Identify important project files when GitAuk needs deterministic file discovery.

```json
{
  "readme": "README.md",
  "architecture": "docs/ARCHITECTURE.md"
}
```

## Rules

The final specification must define:

- required fields,
- optional fields,
- schema versions,
- path validation,
- unknown-field behavior,
- migration rules,
- conflict behavior,
- ownership of generated fields.

Until finalized, `.gitauk/` should be considered experimental.
