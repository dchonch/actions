# actions

Shared reusable GitHub Actions workflows. Update action versions here once — all calling repos pick up the change automatically.

## Workflows

| Workflow | What it runs | Inputs |
|----------|-------------|--------|
| [`security.yml`](.github/workflows/security.yml) | gitleaks (secrets) + trivy (fs scan) | `trivyignore` (bool) |
| [`lint-shell.yml`](.github/workflows/lint-shell.yml) | shellcheck | `path` (string) |
| [`lint-yaml.yml`](.github/workflows/lint-yaml.yml) | yamllint | `config` (string) |
| [`lint-markdown.yml`](.github/workflows/lint-markdown.yml) | markdownlint-cli2 | `glob` (string) |

## Usage

### Security scanning

```yaml
jobs:
  security:
    uses: dchonch/actions/.github/workflows/security.yml@main
    permissions:
      contents: read
      pull-requests: read
```

With a `.trivyignore` file in the calling repo:

```yaml
jobs:
  security:
    uses: dchonch/actions/.github/workflows/security.yml@main
    with:
      trivyignore: true
    permissions:
      contents: read
      pull-requests: read
```

### Shell linting

```yaml
jobs:
  lint-shell:
    uses: dchonch/actions/.github/workflows/lint-shell.yml@main
    with:
      path: scripts/        # optional, defaults to entire repo
    permissions:
      contents: read
```

### YAML linting

```yaml
jobs:
  lint-yaml:
    uses: dchonch/actions/.github/workflows/lint-yaml.yml@main
    with:
      config: .yamllint.yml # optional, defaults to "relaxed"
    permissions:
      contents: read
```

### Markdown linting

```yaml
jobs:
  lint-markdown:
    uses: dchonch/actions/.github/workflows/lint-markdown.yml@main
    with:
      glob: "docs/**/*.md"  # optional, defaults to **/*.md
    permissions:
      contents: read
```

## Updating action versions

Edit the pinned SHAs in `.github/workflows/*.yml` — all callers update on their next run.

Current pins:
- `actions/checkout` — `de0fac2e4500dabe0009e67214ff5f5447ce83dd` (v6)
- `gitleaks/gitleaks-action` — `dcedce43c6f43de0b836d1fe38946645c9c638dc` (v2)
- `aquasecurity/trivy-action` — `57a97c7e7821a5776cebc9bb87c984fa69cba8f1` (v0.35.0)
