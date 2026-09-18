# GitAuk

GitAuk is a GitHub-centered platform for analyzing, managing, synchronizing, and exposing software projects.

The goal is to turn a Git repository into a structured, machine-readable project that can be inspected through multiple services instead of relying only on a manually maintained resume or portfolio.

## Core Ideas

GitAuk can:

- Analyze repository structure and project organization.
- Calculate a repository health score using configurable criteria.
- Analyze code quality and project practices.
- Estimate the percentage of code that may have been AI-assisted.
- Fetch and inspect repository code and project metadata.
- Synchronize repositories using GitAuk-defined synchronization rules and commits.
- Expose project information through APIs for portfolios and other applications.
- Use a dedicated `.gitauk/` directory inside supported repositories to store project metadata, configuration, mappings, and other information required by GitAuk.

## Why GitAuk?

Traditional portfolios require developers to manually update project descriptions, technology lists, activity information, and other details.

GitAuk aims to make the repository itself a primary source of project information.

```text
GitHub Repository
       |
       v
   GitAuk Engine
       |
       +--> Repository Analysis
       +--> Health Score
       +--> Code / Structure Analysis
       +--> AI-Assistance Estimation
       +--> GitAuk Sync
       +--> Project Metadata
       |
       v
     GitAuk API
       |
       +--> Portfolio
       +--> Dashboard
       +--> Other Services
```

## Main Components

### Repository Analyzer
Inspects repository structure, languages, files, configuration, Git history, and project conventions.

### Health Analyzer
Produces a score based on defined and documented criteria. The score is intended as an engineering signal, not an absolute measure of project quality.

### Code Analyzer
Examines source code and project-level characteristics such as structure, maintainability signals, testing, documentation, and configuration.

### AI-Assistance Analyzer
Provides an estimate of how much code may have been generated or assisted by AI-based tools. This is probabilistic and must not be presented as definitive proof of authorship.

### GitAuk Sync
Provides a controlled synchronization mechanism based on repository state, Git commits, and GitAuk metadata.

### GitAuk API
Provides structured project information so external applications such as portfolios do not need to manually maintain every project detail.

## `.gitauk/`

A supported repository may contain a special directory:

```text
.gitauk/
├── project.json
├── files.json
├── rules/
├── mappings/
└── ...
```

The exact schema will be defined separately in the GitAuk metadata specification.

The directory should contain only information that is useful to GitAuk and should avoid duplicating information that Git can already provide reliably.

## Project Status

GitAuk is currently in the architecture and specification stage.

Implementation should begin only after the core repository model, metadata format, service boundaries, API contracts, security model, and contribution workflow are sufficiently defined.

## Documentation

- `CONTRIBUTING.md` — contribution workflow and development rules.
- `ARCHITECTURE.md` — system architecture and service boundaries.
- `CODE_OF_CONDUCT.md` — community expectations.
- `SECURITY.md` — security reporting and repository-access principles.
- `ROADMAP.md` — planned development phases.
- `docs/` — detailed technical specifications.
- `.gitauk/` — repository-level GitAuk metadata specification.

## Design Principles

1. Git remains the source of truth for repository history.
2. GitAuk metadata should be explicit and versionable.
3. Analysis results should be reproducible where practical.
4. Scores must be explainable through their underlying criteria.
5. AI-code detection must be presented as an estimate.
6. Repository access must follow least-privilege principles.
7. Services should have clear responsibilities and interfaces.
8. APIs should be versioned.
9. The system should work with repositories without forcing unnecessary project changes.
10. Open-source contributions should be easy to understand and review.

## License

License: TBD.
