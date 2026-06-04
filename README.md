# Personal Trainer DevOps Documentation.

<!--banner image-->
<img src="./assets/banner.png" alt="Improvised project banner" width="100%"/>

This repository is a documentation base for DevOps implementations/processes(e.g. CI/CD pipelines,
infrastructure, monitoring, runbooks, etc.) on the Personal Trainer(FitCall) project.

It is intentionally created and well composed, to help centralize the documentation of all DevOps
implementations done so far - with Github serving as a base for the project's DevOps engineers to
collaborate and contribute to it progressively.

The repository is fragmented to ensure separation of concerns, thereby facilitating easy access,
faster onboardings, and more other benefits.

## Table Of Contents

- [Documentation Guidelines](#documentation-guidelines)
- [Infrastructure Overview](#infrastructure-overview)
- [Known Unavailable Ports](#known-unavailable-ports)

## Documentation Guidelines.

Below are some very important guidelines for contributing documentation to this repository.

- FIRST and most importantly, ensure to read though the whole of this readme for good-to-know
  information such as: the currently available infrastructure being provided and utilized, the
  project's DevOps tech stack, compulsory implementation guidelines, and more other general details
  that will be relevant to you as a DevOps engineer working on the project.

- CAREFULLY read through the [CONTRIBUTING.md](CONTRIBUTING.md) file before contributing, and ensure
  to strictly follow the guidelines as contained in it.

- Add all documentation inside the docs directory([./docs](./docs))

- All documentation must be written in `Markdown format`.

- Ensure separation of concerns: as much as possible, keep each implementation in a separate
  directory. Each directory should be dedicated to a specific topic or implementation, with relevant
  sub-directories(e.g. screenshots) within them.

- All documentation must be written in a clear, concise, and easy-to-understand manner.

- All documentation must be written in a consistent style and format.

- Ensure to add related links or references to external resources when appropriate.

## Infrastructure Overview

The project infrastructure consists of a single **AWS EC2 (Ubuntu)** instance hosting all core
services and environments. Deployment is handled via GitHub Actions as a non-privileged `deploybot`
user, with processes managed by `systemd` and traffic proxied through **Nginx** with TLS
termination.

...

## Known Unavailable Ports

The below table shows a list of known ports that are currently unavailable for use as they are
running various services on our DevOps infrastructure. For parent server reference, it is
recommended that you use "Server Identifier" instead of "Server IP" as the server's IP address is
very liable to change.

> P.S: This list should be kept up to date at all times. Especially considering the fact the
> internal infra state might change.
>
> If using distributed infra: set "Server Identifier" and "Server IP" to a generic value: E.g."all
> BE servers", "all DB servers" etc.

| Port | Server IP     | Server Identifier | Service               |
| :--- | :------------ | :---------------- | :-------------------- |
| 22   | 16.170.96.186 | main              | SSH                   |
| 80   | 16.170.96.186 | main              | Nginx                 |
| 443  | 16.170.96.186 | main              | Nginx                 |
| 3001 | 16.170.96.186 | main              | Frontend (Staging)    |
| 3002 | 16.170.96.186 | main              | Frontend (Production) |
| 4001 | 16.170.96.186 | main              | Backend (Staging)     |
| 4002 | 16.170.96.186 | main              | Backend (Production)  |
| 5432 | 16.170.96.186 | main              | PostgreSQL            |
| 6379 | 16.170.96.186 | main              | Redis                 |
| 8080 | 16.170.96.186 | main              | FitCall               |
| 8090 | 16.170.96.186 | main              | Detrudr               |
