# Copilot Instructions for devantler-tech/reusable-workflows

## Repository Structure

```text
.github/
├── dependabot.yaml                    # Dependabot configuration (daily, GitHub Actions)
├── fixtures/                          # Test fixtures for workflow testing
│   └── dotnet-test-action/            # .NET test project fixture
├── labels.yaml                        # GitHub issue label definitions
└── workflows/
    ├── .release.yaml                  # Internal: triggers release on push to main
    ├── .sync-labels.yaml              # Internal: daily label sync (scheduled)
    ├── cd-dotnet-library-publish.yaml # Reusable: publish .NET library to NuGet
    ├── cd-pages-publish.yaml          # Reusable: build and deploy Jekyll site to Pages
    ├── ci-auto-merge.yaml             # Reusable: auto-merge trusted bot/maintainer PRs
    ├── ci-docs.yaml                   # Reusable: MegaLinter documentation linting
    ├── ci-dotnet-test.yaml            # Reusable: .NET test across 3 OSes
    ├── ci-go.yaml                     # Reusable: Go lint, build, test, coverage
    ├── delete-workflow-runs.yaml      # Reusable: clean up old workflow runs
    ├── release.yaml                   # Reusable: semantic-release automation
    ├── sync-cluster-policies.yaml     # Reusable: sync Kyverno policies from upstream
    ├── test-delete-workflow-runs.yaml # Test: exercises delete-workflow-runs.yaml with dry-run
    ├── test-zizmor.yaml               # Test: exercises zizmor.yaml with fixtures
    ├── todos.yaml                     # Reusable: scan TODOs and create GitHub issues
    └── zizmor.yaml                    # Reusable: GitHub Actions security analysis
```

## Key Configuration Files

| File                 | Purpose                                    |
|----------------------|--------------------------------------------|
| `.releaserc`         | semantic-release config (main branch)      |
| `.mega-linter.yml`   | MegaLinter config (disables SPELL_CSPELL)  |
| `.yamllint.yml`      | YAML linting rules                         |
| `.cspell.json`       | Spell-checker config and custom words      |
| `.markdownlint.json` | Markdown linting rules                     |
| `zizmor.yml`         | Zizmor security scanner pinning policies   |

## Workflow Development Rules

### All Reusable Workflows Must

1. **Use `workflow_call` trigger** — this is what makes them reusable.
2. **Pin all external actions to commit SHAs** — never use floating tags (`@v4`). Format: `uses: owner/repo@<sha> # <version-comment>`.
3. **Include `step-security/harden-runner`** as the first step of every job with `egress-policy: audit`.
4. **Set `permissions: {}` at the workflow top level** — grant specific permissions per-job using job-level `permissions:`.
5. **Set `persist-credentials: false`** on `actions/checkout` unless the job needs to push commits.
6. **Use conventional commit messages** — `feat:`, `fix:`, `chore:`, `ci:` prefixes for semantic-release.
7. **Document secrets and inputs** in `README.md` with usage examples.

### Required Workflow Triggers

Workflows used as [organization-level repository rulesets](https://docs.github.com/en/organizations/managing-organization-settings/managing-rulesets-for-repositories-in-your-organization) must also include `pull_request` and `merge_group` triggers:

```yaml
on:
  workflow_call:
    # ... inputs/secrets
  ### Required Workflow Triggers ###
  pull_request:
  merge_group:
  ##################################
```

### Test Workflows

Test workflows exercise reusable workflows with safe parameters (dry-run, fixtures). They must:

1. Be named `test-<workflow-name>.yaml`.
2. Trigger on `pull_request` to `main` and `push` to `main`.
3. Use `concurrency` groups to prevent parallel test runs.
4. Include a status aggregation job with `if: ${{ !cancelled() }}`.
5. Use test fixtures from `.github/fixtures/` when applicable.
6. Never perform destructive operations — use dry-run modes or safe defaults.

## Validation Commands

```bash
# Validate YAML syntax
python3 -c "import yaml; yaml.safe_load(open('.github/workflows/<file>.yaml'))"

# Run yamllint
yamllint .github/workflows/

# Check action pinning with zizmor (if installed)
zizmor --config zizmor.yml .github/workflows/
```

## Authentication Patterns

This repository uses **GitHub App tokens** (not `GITHUB_TOKEN`) for operations that need to trigger other workflows or bypass branch protection:

```yaml
- name: 🔑 Generate GitHub App Token
  uses: actions/create-github-app-token@<sha> # <version>
  id: generate-token
  with:
    app-id: ${{ vars.APP_ID }}
    private-key: ${{ secrets.APP_PRIVATE_KEY }}
```

The app credentials are:
- `APP_ID` — stored as a repository/org variable
- `APP_PRIVATE_KEY` — stored as a repository/org secret
