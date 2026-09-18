# Contributing to GitAuk

Thank you for contributing to GitAuk.

GitAuk is an open-source project, so changes should be understandable, testable, and easy for other contributors to review.

## Before Starting

1. Read `README.md`.
2. Read `ARCHITECTURE.md`.
3. Check `ROADMAP.md` for the current development phase.
4. Search existing issues and pull requests before creating duplicate work.
5. For significant architectural changes, open or discuss an issue before implementation.

## Development Workflow

```text
Issue / Proposal
      |
      v
Create Branch
      |
      v
Implement
      |
      v
Test
      |
      v
Commit
      |
      v
Pull Request
      |
      v
Review
      |
      v
Merge
```

## Branch Naming

Use descriptive branch names:

```text
feature/<name>
fix/<name>
docs/<name>
refactor/<name>
test/<name>
chore/<name>
```

Examples:

```text
feature/repository-health
feature/gitauk-sync
fix/github-token-validation
docs/api-specification
```

## Commits

Keep commits focused.

Preferred format:

```text
type: short description
```

Examples:

```text
feat: add repository health analyzer
fix: validate repository access token
docs: define gitauk metadata schema
test: add health score test cases
```

Avoid mixing unrelated changes in the same commit.

## Pull Requests

A pull request should explain:

- What changed.
- Why the change was needed.
- How it was tested.
- Any API or schema changes.
- Any security implications.
- Any migration or compatibility requirements.

For large changes, include a short architecture explanation.

## Code Quality

Contributions should:

- Follow the project's established language and formatting conventions.
- Prefer small, testable components.
- Avoid unnecessary duplication.
- Include tests for important behavior.
- Handle errors explicitly.
- Avoid leaking repository contents, credentials, or tokens through logs.
- Keep public APIs documented.

## Repository Access

GitAuk may process private repositories. Contributors must treat repository contents and credentials as sensitive.

Never commit:

- GitHub access tokens.
- API keys.
- Passwords.
- Private repository data.
- Personal credentials.
- Generated secrets.

Use environment variables or the project's approved secret-management mechanism.

## `.gitauk/` Changes

Changes to the `.gitauk/` format can affect compatibility across GitAuk services.

Changes to:

- metadata schemas,
- file mappings,
- synchronization rules,
- version fields,

should include documentation and compatibility considerations.

## Analysis Rules

Health scores, code analysis, and AI-assistance analysis should be explainable.

Do not introduce a score without documenting:

- its criteria,
- weighting,
- expected input,
- limitations,
- versioning behavior.

AI-assisted code detection must be treated as an estimate rather than definitive authorship evidence.

## Reporting Bugs

Include:

- GitAuk version or commit.
- Operating system.
- Relevant service/component.
- Steps to reproduce.
- Expected behavior.
- Actual behavior.
- Relevant logs with secrets removed.

## License

By contributing, contributors agree that their contributions are provided under the project's chosen license.

The project license is currently TBD.
