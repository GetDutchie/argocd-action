GitHub action for executing Argo CD 🦑

## Usage

See the [ArgoCD CLI documentation](https://argoproj.github.io/argo-cd/user-guide/commands/argocd/) for the list of available commands and options.

```yml
- uses: GetDutchie/argocd-action/@main
  with:
    version: 2.5.5
    command: version
    options: --client
```

### With GitHub API authentication

If you are running a lot of workflows/jobs quite frequently, you may run into GitHub's API rate limit due to pulling the CLI from the ArgoCD repository. To get around this limitation, add the `GITHUB_TOKEN` as shown below (or see [here](https://github.com/octokit/auth-action.js#createactionauth) for more examples) to utilize a higher rate limit when authenticated.

```yml
- uses: GetDutchie/argocd-action/@main
  env:
    # Only required for first step in job where API is called
    # All subsequent setps in a job will not re-download the CLI
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
  with:
    command: version
    options: --client
- uses: GetDutchie/argocd-action/@main
  # CLI has already been downloaded in prior step, no call to GitHub API
  with:
    command: version
    options: --client
```
