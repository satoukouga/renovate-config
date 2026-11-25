# renovate-config

Shared [Renovate](https://docs.renovatebot.com/) preset for satoukouga's repositories.

## Use

In a repository's `.github/renovate.jsonc`:

```jsonc
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>satoukouga/renovate-config"],
  // The branch Renovate's pull requests target.
  "baseBranchPatterns": ["dev"]
}
```

Settings in the repository are applied on top of the preset; lists such as `packageRules` and `customManagers` are added to the preset's.

## What the preset sets

* `config:recommended`, the Dependency Dashboard, and GitHub Actions pinned to commit digests.
* Conventional Commits with the `deps` scope: `chore(deps): update ...`.
* A review request to `satoukouga` on every pull request; nothing merges automatically.
* No release younger than 24 hours, the same as pnpm's `minimumReleaseAge`.
* At most 20 open pull requests per repository (security updates are not counted).
* A weekly lockfile refresh, and OSV advisories as well as GitHub's.
* Versions annotated with `# renovate: datasource=<ds> depName=<name>` in workflows and actions.
* pnpm in `package.json`'s `packageManager` and in `mise.toml` as one update.

## Changing the preset

Renovate reads `default.json` from this repository's default branch, so a change reaches every repository on its next run. Change it through a pull request: the `Validate` workflow checks the preset with `renovate-config-validator --strict --no-global`.
