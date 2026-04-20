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

### 🧹 Lint Documentation

<details>
<summary>Click to expand</summary>

[.github/workflows/lint-documentation.yaml](.github/workflows/lint-documentation.yaml) is a workflow used to lint documentation files using the MegaLinter documentation flavor.

#### Usage

```yaml
jobs:
  docs-lint:
    uses: devantler-tech/reusable-workflows/.github/workflows/lint-documentation.yaml@{ref} # ref
    secrets:
      APP_PRIVATE_KEY: ${{ secrets.APP_PRIVATE_KEY }}
```

#### Secrets and Inputs

| Key               | Type   | Default | Required | Description            |
|-------------------|--------|---------|----------|------------------------|
| `APP_PRIVATE_KEY` | Secret | -       | Yes      | GitHub App private key |

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

[.github/workflows/run-dotnet-tests.yaml](.github/workflows/run-dotnet-tests.yaml) is a workflow used to test .NET solutions or projects across multiple operating systems.

#### Usage

```yaml
jobs:
  dotnet-test:
    uses: devantler-tech/reusable-workflows/.github/workflows/run-dotnet-tests.yaml@{ref} # ref
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
      APP_PRIVATE_KEY: ${{ secrets.APP_PRIVATE_KEY }}
```

#### Secrets and Inputs

| Key               | Type   | Default | Required | Description            |
|-------------------|--------|---------|----------|------------------------|
| `CODECOV_TOKEN`   | Secret | -       | Yes      | Codecov token          |
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

### 🔄 Update Copilot Skills

<details>
<summary>Click to expand</summary>

[.github/workflows/update-copilot-skills.yaml](.github/workflows/update-copilot-skills.yaml) is a workflow used to keep installed Copilot / agent skills up-to-date via [`gh skill update --all`](https://github.blog/changelog/2026-04-16-manage-agent-skills-with-github-cli/), opening a PR with any changes. Each installed `SKILL.md`'s `metadata.github-*` frontmatter is the source of truth — no lockfile is required. Works with any mix of `gh skill`-compatible upstreams.

#### Usage

```yaml
on:
  schedule:
    - cron: "0 6 * * *"
  workflow_dispatch:

jobs:
  update-copilot-skills:
    uses: devantler-tech/reusable-workflows/.github/workflows/update-copilot-skills.yaml@{ref} # ref
    permissions:
      contents: write
      pull-requests: write
    with:
      dir: .agents/skills
```

The workflow assumes skills were previously installed with [`devantler-tech/actions/setup-copilot-skills`](https://github.com/devantler-tech/actions/tree/main/setup-copilot-skills) (or `gh skill install` directly) — the committed `SKILL.md` files carry the upstream pointers.

#### Secrets and Inputs

| Key              | Type            | Default                              | Required | Description                                                            |
|------------------|-----------------|--------------------------------------|----------|------------------------------------------------------------------------|
| `dir`            | Input (string)  | `.`                                  | No       | Directory to scan for installed skills (passed to `gh skill update --dir`) |
| `unpin`          | Input (boolean) | `false`                              | No       | When `true`, pass `--unpin` (clear pinned versions)                    |
| `gh-version`     | Input (string)  | `2.90.0`                             | No       | Minimum required `gh` version (must support `gh skill`)                |
| `pr-branch`      | Input (string)  | `deps/copilot-skills-update`         | No       | Branch the update PR is opened from                                    |
| `pr-title`       | Input (string)  | `chore(deps): update copilot skills` | No       | Title of the update PR                                                 |
| `pr-labels`      | Input (string)  | `dependencies,automation`            | No       | Comma-separated labels for the update PR                               |
| `commit-message` | Input (string)  | `chore(deps): update copilot skills` | No       | Commit message for the update PR                                       |
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

#### Usage

```yaml
jobs:
  go-test:
    uses: devantler-tech/reusable-workflows/.github/workflows/validate-go-project.yaml@{ref} # ref
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
      APP_PRIVATE_KEY: ${{ secrets.APP_PRIVATE_KEY }}
    with:
      pr-owner: ${{ github.event.pull_request.user.login }} # optional
```

#### Secrets and Inputs

| Key               | Type           | Default | Required | Description                                                         |
|-------------------|----------------|---------|----------|---------------------------------------------------------------------|
| `CODECOV_TOKEN`   | Secret         | -       | No       | Codecov token for uploading coverage reports                        |
| `APP_PRIVATE_KEY` | Secret         | -       | No       | GitHub App private key for authenticating the workflow              |
| `pr-owner`        | Input (string) | -       | No       | Pull request author login (used to disable auto-commit for bot PRs) |

</details>
