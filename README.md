# Public Reusable Workflows

## Workflow List

### Release Action

```yaml
jobs:
    release:
        uses: cdqag/workflow-public/.github/workflows/release-action.yaml@v1
        with:
            runs-on: my-own-runner
```

**Features**:

* Uses Conventional Commits and SemVer to automatically version the action
* Creates the Release with Changelog
* Creates/Updates major version tag

**Used Actions**:

* [ietf-tools/semver-action@v1](https://github.com/ietf-tools/semver-action/tree/v1/) to calculate the version
* [requarks/changelog-action@v1](https://github.com/requarks/changelog-action/tree/v1/) to generate the changelog
* [ncipollo/release-action@v1](https://github.com/ncipollo/release-action/tree/v1/) to create the release
* [cdqag/update-majorver@v1](https://github.com/cdqag/update-majorver/tree/v1/) to create/update the major version tag
