# Renovate guidelines

Rules for `renovate.json5` at the repo root and the dependency updates it opens. Renovate is the only dependency updater; Dependabot is not used because it cannot update `mise.toml`, `mise.lock`, or `prek.toml`.

## What Renovate updates

| Manager | Files | Notes |
| --- | --- | --- |
| `github-actions` (built in) | `.github/workflows/*.yml` | Pins actions to full commit SHAs (`helpers:pinGitHubActionDigests`). |
| `mise` (built in) | `mise.toml` `[tools]`, `mise.lock` | `lockFileMaintenance` refreshes `mise.lock`. |
| `regex` (custom) | `prek.toml` remote `rev` values | Built-in pre-commit manager reads only `.pre-commit-config.yaml`. |

The custom manager matches `repo = "https://github.com/<owner>/<name>"` followed by `rev = "<tag>"`. Keep that adjacency in `prek.toml`; a repo entry with other keys between `repo` and `rev` will not be matched.

## Cooldown

`minimumReleaseAge` is `7 days`, the same window as `minimum_release_age` in `mise.toml` and `[update] cooldown_days` in `prek.toml`. Change all three together.

## Validation

Run the validator after editing `renovate.json5`:

```sh
bunx -p renovate renovate-config-validator renovate.json5
```

## Installation

The Renovate GitHub App must be installed on the repo by an org admin. Config changes take effect on the next Renovate run; the Dependency Dashboard issue lists pending updates.
