# CI Templates

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![GitHub Repo Size](https://img.shields.io/github/repo-size/cb0n3y/ci-templates)
![Last Commit](https://img.shields.io/github/last-commit/cb0n3y/ci-templates)
[![.github/workflows/ci.yml](https://github.com/cb0n3y/ci-templates/actions/workflows/ci.yml/badge.svg)](https://github.com/cb0n3y/the-road-to-devops/actions/workflows/ci.yml)

Reusable GitHub Actions workflows for CI/CD pipelines.

This repository contains a collection of reusable GitHub Actions workflows that can be shared across multiple repositories. The goal is to centralize common CI tasks, reduce duplication, and maintain consistent quality checks throughout projects.

## Features

* Reusable GitHub Actions workflows
* Centralized CI/CD logic
* Consistent validation across repositories
* Self-hosted runner support
* Easy integration with existing projects

## Available Templates

| Workflow           | Description                           |
| ------------------ | ------------------------------------- |
| lint-yaml          | Validate YAML files using yamllint    |
| lint-trailing      | Detect trailing whitespace            |
| bandit             | Security analysis for Python projects |
| vagrant-validate   | Validate Vagrantfile syntax           |
| terraform-validate | Validate Terraform configurations     |
| ansible-lint       | Lint Ansible playbooks and roles      |

> The available workflows may change as new templates are added.

## Using a Reusable Workflow

Workflows in this repository are designed to be called using `workflow_call`.

Example:

```yaml
name: CI

on:
  push:
    branches:
      - main

jobs:
  lint-yaml:
    uses: cb0n3y/ci-templates/.github/workflows/lint-yaml.yml@main
```

## Example: Multiple Checks

```yaml
name: CI

on:
  push:
    branches:
      - main

jobs:
  lint-yaml:
    uses: cb0n3y/ci-templates/.github/workflows/lint-yaml.yml@main

  lint-trailing:
    uses: cb0n3y/ci-templates/.github/workflows/lint-trailing.yml@main

  vagrant-validate:
    uses: cb0n3y/ci-templates/.github/workflows/vagrant-validate.yml@main
```

## Self-Hosted Runners

Templates are designed to work with self-hosted runners when required.

Example:

```yaml
jobs:
  validate:
    runs-on:
      - self-hosted
      - nodejs
```

Recommended labels:

* self-hosted
* nodejs
* docker
* terraform
* ansible
* rocky
* ubuntu
* kubernetes

## Versioning

It is recommended to reference workflows using tags instead of the main branch.

Example:

```yaml
jobs:
  lint-yaml:
    uses: cb0n3y/ci-templates/.github/workflows/lint-yaml.yml@v1
```

This ensures stability and prevents unexpected changes from affecting consuming repositories.

## Contributing

Contributions are welcome.

Before submitting changes:

1. Validate workflow syntax.
2. Test workflows on self-hosted runners.
3. Update documentation when adding new templates.
4. Follow GitHub Actions best practices.

## Roadmap

* Additional linting workflows
* Security scanning templates
* Docker build and validation templates
* Terraform plan and apply templates
* Kubernetes validation templates
* Release automation workflows
* Multi-platform runner support

## License

MIT License.
