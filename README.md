<!-- start title -->

# GitHub Action:Release and Update Chart

<!-- end title -->
<!-- start description -->

This action is intended to run on PR merge. It performs a semantic-release, then creates a PR into a helm chart repository with an updated appVersion, using the same PR title and body as the PR that triggered the workflow

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: catalystcommunity/action-release-update-chart@undefined
  with:
    # Github token to use, this should be a PAT so that it can trigger workflows on
    # the destination helm repository
    token: ""

    # semantic-release release configuration to use
    # Default: @catalystcommunity/release-config-general
    release-config: ""

    # The helm chart git repo to update
    # Default: ${{ github.repository_owner }}/chart-${{ github.event.repository.name }}
    helm-repo: ""

    # The helm chart git repo to branch from and PR into
    # Default: alpha
    helm-repo-branch: ""

    # The path to the helm chart in the helm git repo
    # Default: chart
    path-to-chart: ""

    # Labels to apply to the PR. Should be a comma separated string
    # Default: automerge
    labels: ""

    # Delete PR branch after merge
    # Default: true
    delete-branch: ""

    # The prefix for the name of the feature branch
    # Default: automated-code-release-
    branch-prefix: ""

    # Directory to run semantic-release in
    working-directory: ""

    # Whether to checkout the repo at the beginning of the action
    # Default: true
    checkout-repo: ""
```

<!-- end usage -->
<!-- start inputs -->

| **Input**               | **Description**                                                                                               |                                **Default**                                 | **Required** |
| :---------------------- | :------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------: | :----------: |
| **`token`**             | Github token to use, this should be a PAT so that it can trigger workflows on the destination helm repository |                                                                            |   **true**   |
| **`release-config`**    | semantic-release release configuration to use                                                                 |                  `@catalystcommunity/release-config-general`                   |  **false**   |
| **`helm-repo`**         | The helm chart git repo to update                                                                             | `${{ github.repository_owner }}/chart-${{ github.event.repository.name }}` |  **false**   |
| **`helm-repo-branch`**  | The helm chart git repo to branch from and PR into                                                            |                                  `alpha`                                   |  **false**   |
| **`path-to-chart`**     | The path to the helm chart in the helm git repo                                                               |                                  `chart`                                   |  **false**   |
| **`labels`**            | Labels to apply to the PR. Should be a comma separated string                                                 |                                `automerge`                                 |  **false**   |
| **`delete-branch`**     | Delete PR branch after merge                                                                                  |                                   `true`                                   |  **false**   |
| **`branch-prefix`**     | The prefix for the name of the feature branch                                                                 |                         `automated-code-release-`                          |  **false**   |
| **`working-directory`** | Directory to run semantic-release in                                                                          |                                                                            |  **false**   |
| **`checkout-repo`**     | Whether to checkout the repo at the beginning of the action                                                   |                                   `true`                                   |  **false**   |

<!-- end inputs -->
<!-- start outputs -->

| **Output**              | **Description**                                          | **Default** | **Required** |
| :---------------------- | :------------------------------------------------------- | ----------- | ------------ |
| `new-release-published` | The value of new_release_published from semantic-release |             |              |
| `new-release-version`   | The value of new_release_version from semantic-release   |             |              |

<!-- end outputs -->
<!-- start examples -->

### Example usage

```yaml
on: [push]

jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: A job to say hello
    steps:
      - uses: actions/checkout@v2
      - id: foo
        uses: actions/hello-world-composite-action@v1
        with:
          who-to-greet: "Mona the Octocat"
      - run: echo random-number ${{ steps.foo.outputs.random-number }}
        shell: bash
```

<!-- end examples -->
<!-- start [.github/ghdocs/examples/] -->
<!-- end [.github/ghdocs/examples/] -->
