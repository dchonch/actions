# Contributing

## Updating pinned action versions

Each reusable workflow pins its upstream actions to a full commit SHA for supply-chain safety. When a new version of an upstream action is released:

1. Find the new commit SHA from the action's release page
2. Update the `uses:` line in the relevant workflow file:
   ```yaml
   uses: actions/checkout@<new-sha> # v7
   ```
3. Update the "Current pins" section in `README.md`
4. Open a pull request — CI will self-validate the updated workflows

## Adding a new reusable workflow

1. Create `.github/workflows/<name>.yml` with `on: workflow_call`
2. Document inputs in the file's header comment block
3. Add a usage example and workflow row to `README.md`
4. Self-test by calling it from `.github/workflows/ci.yml`

## Workflow design rules

- **Pin all action SHAs** — no floating tags like `@v3` or `@main`
- **Minimal permissions** — declare only what the job needs
- **No secrets passed in** — use `secrets: inherit` only when strictly necessary
- **Inputs have defaults** — callers should work with zero `with:` configuration
