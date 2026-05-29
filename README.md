# deslicer/dap-pipelines

Public CI/CD templates for running the [`deslicer`](https://github.com/deslicer/cli) CLI on non-GitHub platforms.

| Directory | Platform | Templates |
|-----------|----------|-----------|
| `gitlab/` | GitLab CI | `deslicer.gitlab-ci.yml`, `deslicer-multi-env.gitlab-ci.yml` |
| `azure/` | Azure DevOps | `deslicer.yml`, `_steps/install-deslicer.yml` |
| `bitbucket/` | Bitbucket Pipelines | `deslicer-snippet.yml` |
| `circleci/` | CircleCI | Placeholder — not v1 |

GitHub Actions customers use [`deslicer/change-action`](https://github.com/deslicer/change-action) instead of this repo.

## GitLab

```yaml
include:
  - remote: 'https://raw.githubusercontent.com/deslicer/dap-pipelines/main/gitlab/deslicer.gitlab-ci.yml'

reconcile_prod:
  extends: .deslicer-change-plan
  variables:
    DESLICER_ENVIRONMENT: production
  id_tokens:
    DESLICER_OIDC_TOKEN:
      aud: https://api.deslicer.ai
```

## Azure DevOps

Reference `azure/deslicer.yml` as a template extension. See `azure/federated-credential-runbook.md`.

## Bitbucket

Copy `bitbucket/deslicer-snippet.yml` into your `bitbucket-pipelines.yml`.

## Development

Nested checkout: `deslicer-automation-platform/dap-pipelines/` (separate git repo).
