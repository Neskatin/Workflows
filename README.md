# GitHub Actions Reusable Workflows

A collection of reusable GitHub Actions workflows for building, testing, and deploying .NET, NPM, and SPA applications with automated semantic versioning.

## Getting Started

These reusable workflows can be called from your repository's GitHub Actions to standardize your CI/CD pipelines across multiple projects.

### Prerequisites

- GitHub repository with Actions enabled
- Projects using:
  - .NET (with `global.json`)
  - Node.js (with `.nvmrc` and `pnpm`)
  - GitVersion configuration (`GitVersion.yml`)

### Usage

Reference workflows in your `.github/workflows/` directory:

```yaml
name: Build Pipeline

on:
  push:
    branches: [main]

jobs:
  version:
    uses: owner/workflows/.github/workflows/build-semver.yml@v1.0.0

  build:
    needs: version
    uses: owner/workflows/.github/workflows/build-dotnet.yml@v1.0.0
    with:
      rootDirectory: "."
      lint: true
      test: true
      publish: true
```

## Available Workflows

### Versioning

- **`semver.yml`** - Calculate semantic version using GitVersion

### Build Workflows

- **`dotnet.yml`** - Build .NET applications
- **`nuget.yml`** - Build and pack NuGet packages
- **`npm.yml`** - Build and pack NPM packages
- **`spa.yml`** - Build Single Page Applications
- **`docker.yml`** - Build and push Docker containers

### Publishing Workflows

- **`nuget-github.yml`** - Publish NuGet packages to GitHub Packages
- **`npm-github.yml`** - Publish NPM packages to GitHub Packages (private)

### Deployment Workflows

- **`semver.yml`** - Tag repository with semantic version

## Workflow Parameters

All workflows support common parameters:

| Parameter        | Type    | Default         | Description            |
| ---------------- | ------- | --------------- | ---------------------- |
| `rootDirectory`  | string  | `.`             | Project root directory |
| `lint`           | boolean | `true`          | Run linting            |
| `test`           | boolean | `true`          | Run tests              |
| `publish`/`pack` | boolean | `false`         | Create artifacts       |
| `runsOn`         | string  | `ubuntu-latest` | Runner OS              |

See individual workflow files for specific parameters.

## Versioning

All workflows integrate with `build-semver.yml` which uses [GitVersion](https://gitversion.net/) for semantic versioning. Versions are automatically applied to:

- NuGet packages
- NPM packages
- Docker image tags
- Git repository tags

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct and the process for submitting pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
