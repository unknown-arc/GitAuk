# GitAuk Architecture

## 1. Overview

GitAuk is a GitHub-centered, multi-service system for repository analysis, synchronization, metadata management, and project information delivery.

The architecture separates repository access, analysis, synchronization, metadata, and API delivery so that individual services can evolve independently.

## 2. High-Level Architecture

```text
                         +----------------------+
                         |      GitHub          |
                         | Repositories / Git   |
                         +----------+-----------+
                                    |
                                    v
                         +----------------------+
                         | Repository Gateway   |
                         | Auth / Fetch / Git   |
                         +----------+-----------+
                                    |
                   +----------------+----------------+
                   |                |                |
                   v                v                v
          +----------------+ +-------------+ +-------------+
          | Repo Analyzer  | | GitAuk Sync | | Metadata    |
          | Structure      | | Commits     | | Manager     |
          +-------+--------+ +------+------+ +------+------+
                  |                 |               |
                  +-----------------+---------------+
                                    |
                                    v
                         +----------------------+
                         | Analysis Engine      |
                         | Health / Code / AI   |
                         +----------+-----------+
                                    |
                                    v
                         +----------------------+
                         | GitAuk API           |
                         +----------+-----------+
                                    |
                         +----------+----------+
                         |                     |
                         v                     v
                  Portfolio / Web        Other Clients
```

## 3. Major Components

### Repository Gateway

Responsible for communicating with GitHub and local Git operations.

Responsibilities:

- Repository identification.
- Authentication.
- Repository cloning/fetching.
- Commit and branch information.
- File retrieval.
- Git operations required by synchronization.

This component should isolate GitHub-specific behavior from the rest of the system.

### Metadata Manager

Reads and validates the `.gitauk/` directory.

Responsibilities:

- Parse metadata.
- Validate schema versions.
- Resolve file mappings.
- Load project configuration.
- Provide normalized metadata to other services.

### Repository Analyzer

Builds a structural representation of a repository.

Potential analysis areas:

- Directory structure.
- Programming languages.
- Framework indicators.
- Dependency files.
- Test structure.
- Documentation.
- Configuration.
- Git activity.
- Project conventions.

### Health Analyzer

Calculates a health score from documented criteria.

A score should be decomposable:

```text
Health Score
├── Structure
├── Documentation
├── Testing
├── Maintainability
├── Dependency / Configuration Hygiene
└── Git Practices
```

The exact weighting must be defined in a versioned scoring specification.

### Code Analyzer

Analyzes source code and project-level code characteristics.

Possible future capabilities include:

- Static analysis.
- Complexity signals.
- Duplication signals.
- Test coverage integration.
- Dependency analysis.
- Language-specific checks.

### AI-Assistance Analyzer

Attempts to estimate AI-assisted code.

Because AI-code detection is inherently uncertain, the output should contain:

```text
estimate
confidence
method
analyzed_files
limitations
```

The system must not represent the estimate as proof that a person or AI wrote specific code.

### GitAuk Sync

Synchronizes GitAuk-managed information using Git state and commits.

The synchronization model should define:

- Source of truth.
- Conflict handling.
- Commit creation rules.
- Idempotency.
- Rollback behavior.
- Branch behavior.
- Metadata version compatibility.

### API Layer

Provides normalized project information to clients.

Potential API resources:

```text
/projects
/projects/{id}
/projects/{id}/health
/projects/{id}/analysis
/projects/{id}/files
/projects/{id}/activity
```

API versioning should be planned from the beginning.

## 4. `.gitauk/` Directory

The `.gitauk/` directory is a repository-level contract between the repository and GitAuk.

Example:

```text
.gitauk/
├── project.json
├── files.json
├── mappings/
├── rules/
└── schema-version
```

The exact structure is intentionally not finalized here.

Important principles:

- Metadata must be versioned.
- Metadata should be human-readable where practical.
- Invalid metadata must fail safely.
- GitAuk should not silently overwrite user files.
- The directory should contain GitAuk-specific information rather than a copy of the entire repository.

## 5. Data Flow

A typical analysis request:

```text
Client
  |
  v
GitAuk API
  |
  v
Repository Gateway
  |
  v
Repository
  |
  v
Metadata Manager + Repository Analyzer
  |
  v
Analysis Engine
  |
  v
Normalized Result
  |
  v
API Response
```

## 6. Service Boundaries

Services should communicate through explicit interfaces rather than directly depending on internal implementation details.

For example:

```text
GitHub Adapter
      |
Repository Interface
      |
Analysis Services
```

This allows GitHub-specific implementations to change without rewriting analysis logic.

## 7. Storage

Storage architecture is TBD.

The eventual design should distinguish:

- Repository metadata.
- Analysis results.
- Historical analysis results.
- User/account data.
- Synchronization state.
- API cache data.

Large repository contents should not automatically be stored permanently by GitAuk.

## 8. Security

Security is a first-class architectural requirement because GitAuk may access private repositories.

Key principles:

- Least-privilege GitHub permissions.
- Secure token handling.
- No secrets in logs.
- Repository access scoped to the requested operation.
- Isolation between users/repositories.
- Validation of webhook/API inputs.
- Protection against malicious repository contents.
- Safe execution of static analysis tools.

## 9. Extensibility

The analysis engine should support additional analyzers without changing the entire system.

Conceptually:

```text
Analyzer
├── HealthAnalyzer
├── StructureAnalyzer
├── CodeAnalyzer
├── DependencyAnalyzer
├── DocumentationAnalyzer
├── GitAnalyzer
└── AIAssistanceAnalyzer
```

Each analyzer should expose a predictable input/output contract.

## 10. Architecture Decisions

Important architectural decisions should be recorded as ADRs in:

```text
docs/adr/
```

Example:

```text
docs/adr/0001-service-boundaries.md
docs/adr/0002-gitauk-metadata-format.md
```
