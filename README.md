# DevantlerTech GitHub Reusable Workflows 🚀

> [!NOTE]
> To see DevantlerTech's Actions, please visit the [devantler-tech/actions](https://github.com/devantler-tech/actions) repository.

Welcome to the DevantlerTech GitHub Reusable Workflows repository! This repository contains [reusable workflows](#reusable-workflows) designed to streamline your CI/CD processes. These actions are used across all DevantlerTech projects, ensuring consistency and efficiency.

The below diagram illustrates the relationship between GitHub Workflows and GitHub Actions.

```mermaid
---
title: GitHub Actions Relationship Diagram
---
flowchart TD
  A[Workflows] --> B[Jobs]
  B --> C([***Reusable Workflows***])
  B --> D[Steps]
  C --> D
  C --> B
  D --> E[Actions]
  E -.- F([Composite Actions])
  F --> D
  E -.- G([JavaScript Actions])
  E -.- H([Docker Container Actions])
```

## Reusable Workflows

[Reusable workflows](https://docs.github.com/en/actions/how-tos/sharing-automations/reuse-workflows#creating-a-reusable-workflow) are designed to encapsulate common CI/CD patterns that can be shared across multiple repositories. They allow you to define a workflow once and reuse it in the job-scope of other workflows. This reduces duplication and enables building generic workflows for common tasks.

### 🎉 Create Release

<details>
<summary>Click to expand</summary>

[.github/workflows/create-release.yaml](.github/workflows/create-release.yaml) is a workflow used to create releases using semantic-release.

#### Usage

```yaml
jobs:
  release:
    uses: devantler-tech/reusable-workflows/.github/workflows/create-release.yaml@{ref} # ref
    secrets:
      APP_PRIVATE_KEY: ${{ secrets.APP_PRIVATE_KEY }}
```

#### Secrets and Inputs

| Key               | Type            | Default | Required | Description                                                  |
|-------------------|-----------------|---------|----------|--------------------------------------------------------------|
| `APP_PRIVATE_KEY` | Secret          | -       | Yes      | GitHub App private key                                       |
| `dry-run`         | Input (boolean) | `false` | No       | Run semantic-release in dry-run mode (no tags or publishes)  |

</details>

### 🗑️ Delete Workflow Runs

<details>
<summary>Click to expand</summary>

[.github/workflows/delete-workflow-runs.yaml](.github/workflows/delete-workflow-runs.yaml) is a workflow used to clean up old workflow runs from a repository.

#### Usage

```yaml
jobs:
  delete-runs:
    uses: devantler-tech/reusable-workflows/.github/workflows/delete-workflow-runs.yaml@{ref} # ref
    permissions:
      actions: write
      contents: read
    with:
      days: 30 # optional
      minimum-runs: 6 # optional
      dry-run: false # required to perform actual deletions (defaults to true)
```

#### Secrets and Inputs

| Key                                | Type            | Default      | Required | Description                                        |
|------------------------------------|-----------------|--------------|----------|----------------------------------------------------|
| `repository`                       | Input (string)  | Calling repo | No       | Repository to target for workflow run deletion     |
| `days`                             | Input (number)  | `30`         | No       | Days-worth of runs to keep for each workflow       |
| `minimum-runs`                     | Input (number)  | `6`          | No       | Minimum runs to keep for each workflow             |
| `delete-workflow-pattern`          | Input (string)  | -            | No       | Name or filename of the workflow to target         |
| `delete-workflow-by-state-pattern` | Input (string)  | `ALL`        | No       | Filter workflows by state (comma-separated)        |
| `delete-run-by-conclusion-pattern` | Input (string)  | `ALL`        | No       | Remove runs based on conclusion (comma-separated)  |
| `dry-run`                          | Input (boolean) | `true`       | No       | Logs simulated changes, no deletions are performed |

> **Note:** The calling workflow must grant `actions: write` and `contents: read` permissions.

</details>

### 🚀 Deploy GitHub Pages

<details>
<summary>Click to expand</summary>

[.github/workflows/deploy-github-pages.yaml](.github/workflows/deploy-github-pages.yaml) is a workflow used to build and deploy a Jekyll site to GitHub Pages.

#### Usage

```yaml
jobs:
  pages:
    uses: devantler-tech/reusable-workflows/.github/workflows/deploy-github-pages.yaml@{ref} # ref
    with:
      ruby-version: "3.3" # optional
      jekyll-env: production # optional
      extra-build-args: "" # optional, e.g. '--future'
      working-directory: "." # optional, e.g. 'docs' if Jekyll site is in a subdirectory
```

#### Secrets and Inputs

| Key                 | Type            | Default      | Required | Description                                                     |
|---------------------|-----------------|--------------|----------|-----------------------------------------------------------------|
| `dry-run`           | Input (boolean) | `false`      | No       | Skip build and deploy (validate workflow interface only)        |
| `ruby-version`      | Input (string)  | `3.3`        | No       | Ruby version to install                                         |
| `jekyll-env`        | Input (string)  | `production` | No       | Jekyll environment                                              |
| `extra-build-args`  | Input (string)  | `""`         | No       | Extra args appended before the automatically supplied --baseurl |
| `working-directory` | Input (string)  | `"."`        | No       | Working directory for the Jekyll site (e.g., 'docs')            |

#### Outputs

| Key        | Description             |
|------------|-------------------------|
| `page-url` | Deployed Pages site URL |

</details>

### 🔀 Enable Auto-Merge

<details>
<summary>Click to expand</summary>

[.github/workflows/enable-auto-merge.yaml](.github/workflows/enable-auto-merge.yaml) is a workflow that approves and enables auto-merge on pull requests from trusted bots and maintainers.

#### Usage

```yaml
jobs:
  auto-merge:
    uses: devantler-tech/reusable-workflows/.github/workflows/enable-auto-merge.yaml@{ref} # ref
    secrets:
      APP_PRIVATE_KEY: ${{ secrets.APP_PRIVATE_KEY }}
```

#### Secrets and Inputs

| Key               | Type   | Default | Required | Description            |
|-------------------|--------|---------|----------|------------------------|
| `APP_PRIVATE_KEY` | Secret | -       | Yes      | GitHub App private key |

</details>

### 📦 Publish App

<details>
<summary>Click to expand</summary>

[.github/workflows/publish-app.yaml](.github/workflows/publish-app.yaml) is a workflow used to build and publish a containerized app and its Kubernetes manifests to GHCR as cosign-signed OCI artifacts. It builds and pushes the container image (tagged with the semantic version derived from the git tag — e.g. `1.2.3` from a `v1.2.3` tag — plus `sha-<sha>` and `latest`), pins the built image digest into the deployment manifest's `app-name` container, pushes the manifests directory as a Flux-compatible OCI artifact (`ghcr.io/<owner>/<repo>/manifests`), and signs both the image and the manifests artifact with keyless cosign (Fulcio/Rekor via GitHub OIDC).

#### Usage

```yaml
on:
  push:
    tags:
      - "v*"

jobs:
  publish-app:
    uses: devantler-tech/reusable-workflows/.github/workflows/publish-app.yaml@{ref} # ref
    permissions:
      contents: read # checkout
      packages: write # push image + manifests OCI artifact
      id-token: write # keyless cosign signing
    with:
      app-name: my-app # container name in deploy/deployment.yaml
      deploy-path: ./deploy # optional
```

> **Note:** Must be invoked from a semver tag (`vX.Y.Z`) — Docker semver tagging and Flux `OCIRepository` semver selection depend on it. The calling job must grant `packages: write` and `id-token: write` (and `contents: read` for checkout); no secrets are required (auth uses the GHCR-scoped `GITHUB_TOKEN`).

#### Secrets and Inputs

| Key           | Type           | Default    | Required | Description                                                                |
|---------------|----------------|------------|----------|----------------------------------------------------------------------------|
| `app-name`    | Input (string) | -          | Yes      | Container name in the deployment manifest to pin to the built image digest |
| `deploy-path` | Input (string) | `./deploy` | No       | Path to the Kubernetes manifests directory packaged as the OCI artifact    |

</details>

### 📦 Publish .NET Library

<details>
<summary>Click to expand</summary>

[.github/workflows/publish-dotnet-library.yaml](.github/workflows/publish-dotnet-library.yaml) is a workflow used to publish .NET libraries to NuGet and GHCR.

#### Usage

```yaml
jobs:
  publish-library:
    uses: devantler-tech/reusable-workflows/.github/workflows/publish-dotnet-library.yaml@{ref} # ref
    secrets:
      NUGET_API_KEY: ${{ secrets.NUGET_API_KEY }}
```

#### Secrets and Inputs

| Key             | Type            | Default | Required | Description                                          |
|-----------------|-----------------|---------|----------|------------------------------------------------------|
| `NUGET_API_KEY` | Secret          | -       | No       | NuGet API key (required when `dry-run` is `false`)   |
| `dry-run`       | Input (boolean) | `false` | No       | Skip publish (validate workflow interface only)      |

</details>

### 🧪 Run .NET Tests

<details>
<summary>Click to expand</summary>

[.github/workflows/run-dotnet-tests.yaml](.github/workflows/run-dotnet-tests.yaml) is a workflow used to test .NET solutions or projects across multiple operating systems. Coverage is merged into a single Cobertura report and uploaded to **GitHub Code Quality** (native PR coverage).

#### Usage

```yaml
jobs:
  dotnet-test:
    uses: devantler-tech/reusable-workflows/.github/workflows/run-dotnet-tests.yaml@{ref} # ref
    permissions:
      contents: read
      packages: read
      code-quality: write # required for GitHub Code Quality coverage upload
    secrets:
      APP_PRIVATE_KEY: ${{ secrets.APP_PRIVATE_KEY }}
```

> **Note:** The calling workflow must grant `code-quality: write` (otherwise the run fails at startup). Coverage requires the repo's **Code Quality** to be enabled (_Settings → Code quality_).

#### Secrets and Inputs

| Key               | Type   | Default | Required | Description            |
|-------------------|--------|---------|----------|------------------------|
| `APP_PRIVATE_KEY` | Secret | -       | Yes      | GitHub App private key |

</details>

### 📝 Scan for TODO Comments

<details>
<summary>Click to expand</summary>

[.github/workflows/scan-for-todo-comments.yaml](.github/workflows/scan-for-todo-comments.yaml) is a workflow used to scan for TODOs in code and create GitHub issues.

#### Usage

```yaml
jobs:
  todos:
    uses: devantler-tech/reusable-workflows/.github/workflows/scan-for-todo-comments.yaml@{ref} # ref
    secrets:
      APP_PRIVATE_KEY: ${{ secrets.APP_PRIVATE_KEY }}
```

#### Secrets and Inputs

| Key               | Type            | Default | Required | Description                                                |
|-------------------|-----------------|---------|----------|------------------------------------------------------------|
| `APP_PRIVATE_KEY` | Secret          | -       | Yes      | GitHub App private key                                     |
| `dry-run`         | Input (boolean) | `false` | No       | Skip issue creation (validate workflow interface only)     |

</details>

### 🔍 Scan for Workflow Vulnerabilities

<details>
<summary>Click to expand</summary>

[.github/workflows/scan-for-workflow-vulnerabilities.yaml](.github/workflows/scan-for-workflow-vulnerabilities.yaml) is a workflow used to perform static analysis on GitHub Actions workflows using [Zizmor](https://github.com/zizmorcore/zizmor).

#### Usage

```yaml
jobs:
  zizmor:
    uses: devantler-tech/reusable-workflows/.github/workflows/scan-for-workflow-vulnerabilities.yaml@{ref} # ref
```

</details>

### 🔄 Sync Cluster Policies

<details>
<summary>Click to expand</summary>

[.github/workflows/sync-cluster-policies.yaml](.github/workflows/sync-cluster-policies.yaml) is a workflow used to sync upstream Kyverno policies to a target directory.

Which policies are synced is controlled by a `.policyignore` file at the repo root. It uses gitignore-style syntax — ordered glob patterns, one per line, where a leading `!` re-includes a previously excluded path — so you can exclude everything by default and whitelist just the policies you want:

```gitignore
# Ignore every category…
other*
# …except these two policies.
!other/create-pod-antiaffinity/create-pod-antiaffinity.yaml
!other/spread-pods-across-topology/spread-pods-across-topology.yaml
```

Patterns are evaluated per file with last-match-wins, so a `!` re-include still applies even when a broad earlier pattern matched its parent directory.

#### Usage

```yaml
jobs:
  sync-cluster-policies:
    uses: devantler-tech/reusable-workflows/.github/workflows/sync-cluster-policies.yaml@{ref} # ref
    secrets:
      APP_PRIVATE_KEY: ${{ secrets.APP_PRIVATE_KEY }}
    with:
      kyverno-policies-dir: policies/kyverno
```

#### Secrets and Inputs

| Key                    | Type            | Default | Required | Description                                              |
|------------------------|-----------------|---------|----------|----------------------------------------------------------|
| `APP_PRIVATE_KEY`      | Secret          | -       | Yes      | GitHub App private key                                   |
| `kyverno-policies-dir` | Input (string)  | -       | Yes      | Directory to sync Kyverno policies to                    |
| `dry-run`              | Input (boolean) | `false` | No       | Skip sync and PR creation (validate workflow interface only) |

</details>

### 🔄 Template Sync

<details>
<summary>Click to expand</summary>

[.github/workflows/template-sync.yaml](.github/workflows/template-sync.yaml) keeps a repository in sync with an upstream template repository via [AndreasAugustin/actions-template-sync](https://github.com/AndreasAugustin/actions-template-sync), opening a PR with any incoming template changes. List the files this repository *owns* (and that must never be overwritten by the template) in a `.templatesyncignore` file at the repo root — everything else the template ships is kept in sync.

#### Usage

```yaml
on:
  schedule:
    - cron: "0 6 * * 1"
  workflow_dispatch:

jobs:
  template-sync:
    uses: devantler-tech/reusable-workflows/.github/workflows/template-sync.yaml@{ref} # ref
    with:
      source-repo-path: devantler-tech/gitops-tenant-template
    secrets:
      APP_PRIVATE_KEY: ${{ secrets.APP_PRIVATE_KEY }}
```

By default the sync PR is opened with a GitHub App token (`use-app-token: true`) so it triggers the caller's CI; this needs the `APP_ID` variable and the `APP_PRIVATE_KEY` secret. Set `use-app-token: false` to fall back to `GITHUB_TOKEN` (the PR then will not trigger `on: pull_request` checks).

#### Secrets and Inputs

| Key                              | Type            | Default                                          | Required | Description                                                                 |
|----------------------------------|-----------------|--------------------------------------------------|----------|-----------------------------------------------------------------------------|
| `APP_PRIVATE_KEY`                | Secret          | -                                                | When `use-app-token` | GitHub App private key (paired with the `APP_ID` variable)      |
| `source-repo-path`               | Input (string)  | -                                                | Yes      | `owner/repo` of the upstream template to sync from                          |
| `upstream-branch`                | Input (string)  | `main`                                           | No       | Branch of the template repository to sync from                              |
| `pr-title`                       | Input (string)  | `chore: sync changes from the upstream template` | No       | Title of the sync PR (Conventional-Commit by default)                       |
| `pr-commit-msg`                  | Input (string)  | `chore: sync changes from the upstream template` | No       | Commit message for the sync PR                                              |
| `pr-labels`                      | Input (string)  | `dependencies,automation`                        | No       | Comma-separated labels for the sync PR                                      |
| `pr-branch-name-prefix`          | Input (string)  | `chore/template-sync`                            | No       | Prefix for the branch the sync PR is opened from                            |
| `template-sync-ignore-file-path` | Input (string)  | `.templatesyncignore`                            | No       | Path to the file listing consumer-owned (non-synced) files                  |
| `use-app-token`                  | Input (boolean) | `true`                                           | No       | Open the sync PR with a GitHub App token so it triggers the caller's CI     |
| `dry-run`                        | Input (boolean) | `false`                                          | No       | Skip the sync and PR creation (validate workflow interface only)            |

> **Note:** The calling workflow runs the sync job with `contents: write` and `pull-requests: write` (declared by the reusable workflow).

</details>

### 🔄 Update Agent Skills

<details>
<summary>Click to expand</summary>

[.github/workflows/update-agent-skills.yaml](.github/workflows/update-agent-skills.yaml) is a workflow used to keep installed agent skills (Copilot, Claude Code, …) up-to-date via [`gh skill update --all`](https://github.blog/changelog/2026-04-16-manage-agent-skills-with-github-cli/), opening a PR with any changes. Each installed `SKILL.md`'s `metadata.github-*` frontmatter is the source of truth — no lockfile is required. Works with any mix of `gh skill`-compatible upstreams.

#### Usage

```yaml
on:
  schedule:
    - cron: "0 6 * * *"
  workflow_dispatch:

jobs:
  update-agent-skills:
    uses: devantler-tech/reusable-workflows/.github/workflows/update-agent-skills.yaml@{ref} # ref
    permissions:
      contents: write
      pull-requests: write
    with:
      dir: .agents/skills
```

The workflow assumes skills were previously installed with [`devantler-tech/actions/setup-agent-skills`](https://github.com/devantler-tech/actions/tree/main/setup-agent-skills) (or `gh skill install` directly) — the committed `SKILL.md` files carry the upstream pointers.

#### Secrets and Inputs

| Key              | Type            | Default                              | Required | Description                                                            |
|------------------|-----------------|--------------------------------------|----------|------------------------------------------------------------------------|
| `dir`            | Input (string)  | `.`                                  | No       | Directory to scan for installed skills (passed to `gh skill update --dir`) |
| `unpin`          | Input (boolean) | `false`                              | No       | When `true`, pass `--unpin` (clear pinned versions)                    |
| `gh-version`     | Input (string)  | `2.90.0`                             | No       | Minimum required `gh` version (must support `gh skill`)                |
| `pr-branch`      | Input (string)  | `deps/agent-skills-update`           | No       | Branch the update PR is opened from                                    |
| `pr-title`       | Input (string)  | `chore(deps): update agent skills`   | No       | Title of the update PR                                                 |
| `pr-labels`      | Input (string)  | `dependencies,automation`            | No       | Comma-separated labels for the update PR                               |
| `commit-message` | Input (string)  | `chore(deps): update agent skills`   | No       | Commit message for the update PR                                       |
| `dry-run`        | Input (boolean) | `false`                              | No       | Skip update and PR creation (validate workflow interface only)         |

> **Note:** The calling workflow must grant `contents: write` and `pull-requests: write` permissions.

</details>

### ✅ Validate Go Project

<details>
<summary>Click to expand</summary>

[.github/workflows/validate-go-project.yaml](.github/workflows/validate-go-project.yaml) is a workflow used to lint and test Go projects across multiple operating systems.

#### Features

- **Automated Linting**: Runs `golangci-lint` and `mega-linter` to ensure code quality
- **Auto-fix**: Automatically applies linter fixes and commits them
- **Copilot Integration**: When linting fails, automatically prompts Copilot on the PR to fix the remaining issues
- **Supply-chain Scanning**: Runs [`govulncheck`](https://go.dev/blog/govulncheck) via a thin SHA-pinned [`devantler/govulncheck-action`](https://github.com/devantler/govulncheck-action) fork to fail the PR on known vulnerabilities your code actually calls (call-graph reachability, so imported-but-unreachable advisories don't block). A consumer can risk-accept a reachable advisory that has no upstream fix (`Fixed in: N/A`) by committing an optional `.govulncheck-allow.txt` at the repo root (one `GO-YYYY-NNNN  # justification` per line; `#` comments and blank lines ignored); with no allowlist file the gate stays strict (byte-equivalent to the upstream action). The fork is used for every repo — not just opt-in ones — because the upstream [`golang/govulncheck-action`](https://github.com/golang/govulncheck-action) tag-pins its own `actions/checkout`/`actions/setup-go`, which breaks consumers that enforce a SHA-pinned-actions ruleset (GitHub resolves every `uses:` in a job regardless of `if:`); the fork SHA-pins its sub-actions. Swap back to the upstream action once it ships the `allow-file` feature and SHA-pins its sub-actions.
- **Code Coverage**: Generates a Cobertura report and uploads it to **GitHub Code Quality** (native PR coverage).

#### Usage

```yaml
jobs:
  go-test:
    uses: devantler-tech/reusable-workflows/.github/workflows/validate-go-project.yaml@{ref} # ref
    permissions:
      contents: write
      code-quality: write # required for GitHub Code Quality coverage upload
    secrets:
      APP_PRIVATE_KEY: ${{ secrets.APP_PRIVATE_KEY }}
    with:
      pr-owner: ${{ github.event.pull_request.user.login }} # optional
```

> **Note:** The calling workflow must grant `code-quality: write` so coverage can be uploaded to GitHub Code Quality. Coverage requires the repo's **Code Quality** to be enabled (_Settings → Code quality_).

#### Secrets and Inputs

| Key               | Type           | Default | Required | Description                                                         |
|-------------------|----------------|---------|----------|---------------------------------------------------------------------|
| `APP_PRIVATE_KEY` | Secret         | -       | No       | GitHub App private key for authenticating the workflow              |
| `pr-owner`        | Input (string) | -       | No       | Pull request author login (used to disable auto-commit for bot PRs) |

</details>
