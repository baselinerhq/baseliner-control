# baseliner-control

Control repo that runs [baseliner](https://github.com/baselinerhq/baseliner)
against the `baselinerhq` organization on a schedule — the project dogfooding
its own tool.

## Contents

- [`baseliner.yaml`](baseliner.yaml) — scan config: org scope plus per-repo
  waivers for non-code infra repos.
- [`.github/workflows/baseliner.yml`](.github/workflows/baseliner.yml) — weekly
  scheduled scan + manual `workflow_dispatch`; uploads `results.json` as an
  artifact.

## Setup

Add a repository secret **`BASELINER_TOKEN`** — a token that can read the org's
repositories (and `issues: write` if you later enable `--open-issues`). Then run
the workflow from the **Actions** tab.

## Notes

- The scan is report-only today (artifact). To open/update a findings issue per
  repo, add `--open-issues` to the scan step.
- The workflow installs the released binary via the install script, so it also
  exercises baseliner's distribution.
