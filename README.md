# Public Reusable Workflows

## Workflow List

### Release Action

This workflow has been created to automate process of releasing new version of custom GitHub Action and/or Reusable Workflow.

**Features**:

* Uses Conventional Commits and SemVer to automatically version the action
* Creates the Release with Changelog
* Creates/Updates major version tag

**Used Actions**:

* [ietf-tools/semver-action@v1](https://github.com/ietf-tools/semver-action/tree/v1/) to calculate the version
* [requarks/changelog-action@v1](https://github.com/requarks/changelog-action/tree/v1/) to generate the changelog
* [ncipollo/release-action@v1](https://github.com/ncipollo/release-action/tree/v1/) to create the release
* [cdqag/update-majorver@v1](https://github.com/cdqag/update-majorver/tree/v1/) to create/update the major version tag

**Usage**:

```yaml
name: 📦 Release

on:
  push:
    branches:
      - master

jobs:
  release:
    uses: cdqag/workflow-public/.github/workflows/release-action.yaml@v1
```

### Release Action to Major Version Branch

This workflow has been created to copy (release) specified directories and files to given branch.
The problem that is solves, is that coposite GitHub Actions are not supporting git submodules.
But what this workflow does, it copies phisical files and directories to the target branch, removing all other files and directories - submodules including.
With that, the composite action works, because it does not contain any submodules.
The downside of it is that because of changes (removing submodules) the history of the target branch is different, so version cannot be calculated properly,
which causes that the workflow has to be triggered manually.
But if you don't mind that, this workflow is for you.

**Features**:

* Copies specified directories and files to given branch
* Removes all other files and directories
* Replaces git submodules with the actual content
* Gets the major version from the input version
* Creates/Updates major version branch

**Used Actions**:

* [cdqag/normalize-version@v1](https://github.com/cdqag/normalize-version/tree/v1/) to normalize the input version
* [actions/checkout@v4](https://github.com/actions/checkout/tree/v4/) to checkout the repository
* [snow-actions/git-config-user@v1.0.0](https://github.com/snow-actions/git-config-user/tree/v1.0.0/) to configure git user
* [cdqag/release-to-branch@v1](https://github.com/cdqag/release-to-branch/tree/v1/) to copy (release) files/directories to branch
* [ncipollo/release-action@v1](https://github.com/ncipollo/release-action/tree/v1/) to create the release

**Usage**:

```yaml
name: 📦 Release

on:
  workflow_dispatch:
    inputs:
      version:
        description: 'Version to release'
        required: true
        type: string

jobs:
  release:
    uses: cdqag/workflow-public/.github/workflows/release-action-to-branch.yaml@v1
    with:
        runs-on: hosted-runner
        version: ${{ inputs.version }}
```

## License

This project is licensed under the Apache-2.0 License. See the [LICENSE](LICENSE) file for details.
