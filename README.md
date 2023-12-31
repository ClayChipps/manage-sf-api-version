# Manage SF API Version

<a href="https://github.com/ClayChipps/manage-sf-api-version/actions"><img alt="manage-sf-api-version status" src="https://github.com/ClayChipps/manage-sf-api-version/workflows/build-test/badge.svg"></a>

A GitHub action that will automatically find all API version references in a given Salesforce project directory, and upgrade those API version references to the provided API version.

## Usage

### Example

```yml
name: Manage SF API Version
on:
  workflow_dispatch:
    inputs:
      api-version:
        description: 'api version in the format XX e.g 58'
        required: true
        type: string
jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: ClayChipps/manage-sf-api-version@v1
        with:
          api-version: ${{inputs.api-version}}
      - uses: peter-evans/create-pull-request@v5
        with:
          title: 'Bump API Versions to ${{inputs.api-version}}.0'
          body: 'Automatically bumped by GitHub Actions '
          branch: 'devops/bump-api-versions-v${{inputs.api-version}}.0'
          commit-message: 'chore: bump api to v${{inputs.api-version}}.0'
```

You can also pin to a [specific release](https://github.com/ClayChipps/manage-sf-api-version/releases) version in the format `@v1.x.x`

### Action Inputs

| Name          | Description                               | Required |
| ------------- | ----------------------------------------- | -------- |
| `api-version` | The API version as a whole number e.g. 58 | true     |

## License

[MIT](LICENSE)
