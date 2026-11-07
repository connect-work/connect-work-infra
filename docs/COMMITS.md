# Commit message convention

Commit messages are written in English and follow Conventional Commits. The
agent proposes the message and must not run `git commit` unless the developer
explicitly asks.

## Format

```text
<type>(<scope>): <description>

<body: what changed and why, wrapped at 72 characters>

<footer: Refs: #123 / BREAKING CHANGE: ...>
```

## Rules

- Keep the title at or below 72 characters.
- Use imperative mood, lowercase, and no trailing period in the title.
- Explain why the change is needed instead of repeating the diff.
- Keep one logical change per commit.
- Add `BREAKING CHANGE: <explanation>` in the footer when required.
- Reference the issue when one exists with `Refs: #123`.
- Never include secrets or personal data.

## Types

- `feat`: add infrastructure behavior or capability.
- `fix`: correct broken infrastructure behavior.
- `docs`: change documentation only.
- `refactor`: restructure without changing behavior.
- `perf`: improve performance or resource usage.
- `test`: add or correct automated verification.
- `build`: change build or packaging behavior.
- `ci`: change continuous integration or delivery.
- `chore`: perform repository maintenance.
- `revert`: revert an earlier commit.

## Scopes

- `compose`: Docker Compose services, networks, volumes, or healthchecks.
- `caddy`: proxy, HTTPS, headers, or routing.
- `backup`: backup, retention, encryption, or restoration.
- `deploy`: provisioning, releases, rollback, or environment deployment.
- `monitoring`: uptime, logs, alerts, or resource checks.
- `docs`: repository documentation and agent guidance.

## Example

```text
feat(compose): add local postgresql service

Developers need a consistent database version and healthcheck in the local
environment. Bind the development port to loopback so it is not exposed on
the network.

Refs: #42
```
