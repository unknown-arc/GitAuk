# Security Policy

## Scope

GitAuk may interact with GitHub repositories, including potentially private repositories. Security issues involving repository access, credentials, API authorization, data isolation, or unsafe code analysis are especially important.

## Reporting a Vulnerability

Please do not publicly disclose an unpatched security vulnerability.

Use the project's private security reporting mechanism once configured.

Until that mechanism is available, contact the project maintainers privately rather than opening a public issue containing sensitive details.

## Important Security Areas

Contributors should pay particular attention to:

- GitHub access tokens.
- OAuth permissions.
- Repository authorization.
- Private repository contents.
- API authentication and authorization.
- Webhook validation.
- Path traversal.
- Malicious repository files.
- Unsafe execution of repository code.
- Dependency vulnerabilities.
- Log leakage.

## Secrets

Never commit credentials, tokens, private keys, or other secrets.

Use environment variables or an approved secret-management solution.

## AI-Code Analysis

AI-assisted code detection results are estimates and should not be treated as security or authorship proof.

## Disclosure

The project's vulnerability disclosure and supported-version policy will be finalized before production release.
