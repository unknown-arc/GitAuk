# GitAuk API Specification

## Status

Draft.

## Goals

The API should expose repository-derived project information to portfolios, dashboards, and other clients.

## Principles

- Version the API.
- Return stable resource identifiers.
- Separate current project data from historical analysis results.
- Provide explainable analysis results.
- Enforce authorization for private repositories.
- Avoid exposing raw private repository contents unless explicitly authorized.

## Proposed Endpoints

```text
GET /api/v1/projects
GET /api/v1/projects/{project_id}

GET /api/v1/projects/{project_id}/health
GET /api/v1/projects/{project_id}/analysis
GET /api/v1/projects/{project_id}/files
GET /api/v1/projects/{project_id}/activity
```

## Future Operations

```text
POST /api/v1/projects/{project_id}/analyze
POST /api/v1/projects/{project_id}/sync
GET  /api/v1/projects/{project_id}/sync/status
```

Exact authentication, authorization, pagination, error formats, and rate limits are TBD.

## Portfolio Use Case

A portfolio can request a project's public representation:

```text
Portfolio
   |
   v
GitAuk API
   |
   v
Normalized Project Data
```

This reduces manual portfolio maintenance.

## API Versioning

Breaking changes should require a new API version rather than silently changing an existing contract.
