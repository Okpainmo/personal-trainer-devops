# Contributing

Thank you for contributing to the Personal Trainer DevOps documentation.

This repository is the shared source of truth for DevOps decisions, implementation notes,
operational runbooks, deployment references, and supporting evidence for the Personal Trainer
project.

## Contribution Standard

- Add all documentation inside the docs directory([./docs](./docs))

- A new/dedicated directory must be created for each implementation.

- Place related documents in a dedicated directory when the topic has multiple files.

- All documentation must be written in `Markdown format`.

- Keep every document focused on one implementation, process, or decision.

- All documentation must be written in a clear, concise, and easy-to-understand manner. Write in
  clear Markdown and avoid unexplained acronyms.

- All documentation must be written in a consistent style and format.

- Add supporting screenshots, logs, links, diagrams, or references when they make the work easier to
  verify later. Keep related files in a sub-directory to be created within the main implementation
  directory - E.g. screenshots should be kept in a "screenshots" sub-directory.

- Never commit secrets, credentials, private keys, access tokens, `.env` files, or production-only
  values.

- Prefer reproducible steps over broad descriptions.

## Setup

Install dependencies with pnpm:

```sh
pnpm install
```

Husky is installed through the `prepare` script. If hooks are not active after installing
dependencies, run:

```sh
pnpm run prepare
```

## Local Checks

Format all Markdown files:

```sh
pnpm run format
```

Check Markdown formatting:

```sh
pnpm run format:check
```

Run the local forbidden-pattern scan:

```sh
pnpm run security:forbidden-patterns
```

## Commit Messages

This repository uses Conventional Commits. Use the format:

```text
type(scope): short description
```

Examples:

```text
docs(ci): document staging deployment workflow
chore(tooling): add markdown formatting checks
fix(runbook): correct rollback command
```

Common types are:

- `docs`: documentation-only changes.

- `chore`: tooling, repository maintenance, or non-user-facing updates.

- `fix`: corrections to inaccurate or broken documentation.

- `ci`: workflow and automation changes.

## Git Hooks

The repository uses Husky for local gates:

- `commit-msg`: validates commit messages with commitlint.

- `pre-commit`: runs the repository hygiene checks, formats Markdown, and applies lint-staged.

- `pre-push`: checks that all Markdown files are formatted.

## Pull Requests

Before opening a pull request:

- Run `pnpm run format:check`.

- Run `pnpm run security:forbidden-patterns`.

- Confirm that no secrets or environment-specific private values were added.

- Link the related issue, task, incident, or deployment reference when one exists.

- Add screenshots or logs for visual, terminal, cloud-console, or CI evidence when relevant.

## Documentation Style

- Use sentence case headings unless the document already follows a different established pattern.

- Prefer short sections with concrete steps.

- Use fenced code blocks for commands, configuration, logs, and file examples.

- Include expected outcomes after operational commands where possible.

- Use relative links for files inside this repository.

## Review Expectations

Reviewers should check for accuracy, reproducibility, formatting, security exposure, and whether the
documentation can be followed by another DevOps engineer without private context.
