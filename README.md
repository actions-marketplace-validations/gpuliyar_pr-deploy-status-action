# PR Deploy Status Github Action
Github Action to fetch and output the PR's last deploy status to an environment. It is useful to developers to trigger a job only if the PR's last deployment to a PaaS was successful. 
Note: Validated this feature as part of Github - Heroku continuous deployment. Another important factor to remember, when a code pushed to a PR, the PaaS deployment is async. If this action is used in a PR, then there is a high probability that this check will never give the intended result. It is recommended to use this check in a `repository_dispatch` check and trigger the flow as part of the code deployment - post deploy process.

## Inputs

Name | Description | Required
--- | --- | ---
`repository` | Git Repository name (owner/repository name) | `true`
`environment` | Pull Request deployment environment name | `true`

## Outputs

Name | Description
--- | ---
`state` | Pull requests last deployed state

## Example Usage

```
jobs:
  get-pr-deploy-status:
    runs-on: ubuntu-latest
    steps:
    - name: Output PR last deploy status
        uses: gpuliyar/pr-deploy-status-action@v1.0.0
        with:
          # Repository name (Mandatory)
          repository: ${{ github.repository }}

          # Pull Request deployment environment name (Mandatory)
          environment: yabba-da-ba-doo-environment
        env:
          # Default Github Token
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

> `GITHUB_TOKEN` (*required) to make Github API calls to fetch PR deployment status

