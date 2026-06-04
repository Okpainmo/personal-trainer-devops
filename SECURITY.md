# Security Policy

This repository may contain operational documentation, deployment references, screenshots, and
command examples. Treat all contributions as security-sensitive.

## Do Not Commit

- Secrets, passwords, private keys, tokens, or certificates.
- `.env` files or copied environment variables.
- Internal-only hostnames, IP addresses, or access paths unless explicitly approved.
- Screenshots that expose credentials, account IDs, tokens, private URLs, or sensitive project data.
- Production logs containing user data or infrastructure secrets.

## Reporting a Security Issue

Do not open a public issue for sensitive security findings.

Report the issue through the approved internal team channel and include:

- A short description of the exposure or risk.
- The affected file, workflow, or documentation path.
- Whether the value is still active.
- Any immediate mitigation already taken.

## Local Security Checks

Run the local repository scan before pushing:

```sh
pnpm run security:forbidden-patterns
```

CI also runs secret and vulnerability scans on pull requests.
