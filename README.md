# .github

Account-level `.github` repo for profile README, default health files, and shared actions.

## Reusable workflows

Shared CI for the `alfred-*` repos.

- **`go-alfred-build.yaml`** — PRs: vet, golangci-lint, build on macOS and Linux.
- **`go-alfred-release.yaml`** — `v*` tags: universal binary, package `.alfredworkflow`, GoReleaser release.

No inputs. Binary name comes from the repo name (`github.event.repository.name`), same as `PROJECT_NAME` in each Makefile.

## Usage

Build/test, in `.github/workflows/build-and-test.yaml`:

```yaml
name: Build and Test
on:
  pull_request:
    branches: [main]
jobs:
  ci:
    uses: rwilgaard/.github/.github/workflows/go-alfred-build.yaml@v1
```

Release, in `.github/workflows/release.yaml`:

```yaml
name: Release
on:
  push:
    tags: [v*]
permissions:
  contents: write
jobs:
  release:
    uses: rwilgaard/.github/.github/workflows/go-alfred-release.yaml@v1
```
