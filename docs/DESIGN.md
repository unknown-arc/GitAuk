# GitAuk Design Specification

## 1. Project Model

GitAuk should treat a repository as a project that can have:

- identity,
- metadata,
- source files,
- Git history,
- analysis results,
- synchronization state,
- API representation.

The exact database model is TBD.

## 2. Analysis Model

Every analysis should be identifiable by:

```text
project
analyzer
analyzer_version
started_at
completed_at
status
result
```

This makes analysis results traceable when analyzer rules change.

## 3. Score Model

Scores should never exist without their criteria.

Example conceptual result:

```json
{
  "score": 78,
  "version": "1.0",
  "categories": {
    "structure": 82,
    "documentation": 70,
    "testing": 75,
    "git_practices": 85
  }
}
```

The exact categories and weights are TBD.

## 4. AI-Assistance Result

The result should distinguish an estimate from certainty.

Example conceptual model:

```json
{
  "estimated_ai_assisted_percentage": 32,
  "confidence": 0.61,
  "method_version": "0.1",
  "limitations": []
}
```

The number should never be described as definitive authorship attribution.

## 5. Portfolio Data

Portfolio clients should consume GitAuk's normalized API instead of scraping repository pages.

Potential information:

- project name,
- description,
- technologies,
- repository link,
- activity,
- selected files,
- project statistics,
- analysis summaries,
- health information.

The user should not need to manually duplicate information that GitAuk can reliably derive from the repository.

## 6. File Selection

The `.gitauk/` metadata can identify important files when automatic discovery is insufficient.

Example conceptual mapping:

```json
{
  "readme": "README.md",
  "architecture": "docs/ARCHITECTURE.md",
  "documentation": "docs/"
}
```

The implementation should validate paths and prevent traversal outside the repository.

## 7. Versioning

The following should be independently versionable where necessary:

- `.gitauk/` schema.
- Analyzer implementations.
- Health-score rules.
- API.
- Synchronization protocol.

Historical results should retain the versions used to produce them.
