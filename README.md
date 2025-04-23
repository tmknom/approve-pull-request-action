# approve-pull-request-action

Approve a pull request.

<!-- actdocs start -->

## Description

This action approves a specified pull request.

> [!IMPORTANT]
> Before using this action, ensure that GitHub Actions is allowed to create and approve pull requests in the repository.
> For more details, see: [Preventing GitHub Actions from creating or approving pull requests][approve_settings].

## Usage

```yaml
  steps:
    - name: Approve Pull Request
      uses: tmknom/approve-pull-request-action@v0
      with:
        pull-request: 10
```

## Inputs

| Name | Description | Default | Required |
| :--- | :---------- | :------ | :------: |
| pull-request | Specifies the pull request to approve as a `number`, `url`, or `branch`. | n/a | yes |

## Outputs

N/A

<!-- actdocs end -->

## Permissions

| Scope         | Access |
| :------------ | :----- |
| contents      | write  |
| pull-requests | write  |

## FAQ

### How to fix the `GitHub Actions is not permitted to approve pull requests` error

If the `Allow GitHub Actions to create and approve pull requests` setting is disabled,
you might encounter the following error:

```shell
failed to create review: GraphQL: GitHub Actions is not permitted to approve pull requests. (addPullRequestReview)
```

To resolve this issue, update your repository settings via the GitHub web UI or GitHub CLI.

#### Web UI

Follow these steps in your browser:

1. On GitHub, navigate to the main page of the repository.
2. Under your repository name, click `Settings`
3. In the left sidebar, click `Actions`, then click `General`.
4. Under "Workflow permissions", use the **Allow GitHub Actions to create and approve pull requests** setting to configure whether `GITHUB_TOKEN` can create and approve pull requests.
5. Click `Save` to apply the settings.

For more details, see: [Preventing GitHub Actions from creating or approving pull requests][approve_settings].

#### GitHub CLI

Run the following command in your terminal:

```shell
REPOSITORY="<OWNER>/<REPO>"

gh api \
  --method PUT \
  -H "Accept: application/vnd.github+json" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  "/repos/${REPOSITORY}/actions/permissions/workflow" \
  -F can_approve_pull_request_reviews=true
```

For more details, see: [API Document][https://docs.github.com/en/rest/actions/permissions?apiVersion=2022-11-28#set-default-workflow-permissions-for-a-repository].


## Related projects

- [merge-pr-action](https://github.com/tmknom/merge-pr-action): Merge a pull request.
- [merge-workflows](https://github.com/tmknom/merge-workflows): Collection of merge workflows.

## Release notes

See [GitHub Releases][releases].

[approve_settings]: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#preventing-github-actions-from-creating-or-approving-pull-requests
[releases]: https://github.com/tmknom/approve-pull-request-action/releases
