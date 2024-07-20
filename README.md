# Push Version Tags Action

[![CI](https://github.com/ovsds/push-version-tags-action/workflows/Check%20PR/badge.svg)](https://github.com/ovsds/push-version-tags-action/actions?query=workflow%3A%22%22Check+PR%22%22)
[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Push%20Version%20Tags-blue.svg)](https://github.com/marketplace/actions/push-version-tags)

Pushes supplementary (major, minor) version tags to a repository. It is useful for creating tags for major and minor versions based on a base version.
For example, if the base version is `v1.2.3`, it will create tags `v1` and `v1.2`.

## Usage

### Example workflow

```yaml
name: Push version tags

on:
  release:
    types: [published]

jobs:
  push-version-tags:
    runs-on: ubuntu-20.04

    permissions:
      contents: write

    steps:
      - name: Push Version Tags
        uses: ovsds/push-version-tags-action@v1
        with:
          version: ${{ github.event.release.tag_name }}
```

### Action Inputs

| Name           | Description                                                                                                                      | Default             |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------- |
| `github_token` | Github token used for API calls. Required scope - 'contents: write'                                                              | ${{ github.token }} |
| `version`      | Base version to be used for tags. Should be in format {major}.{minor}.{patch} or v{major}.{minor}.{patch} (e.g. 1.2.3 or v1.2.3) |                     |
| `major`        | Weather to push major version tag.                                                                                               | true                |
| `minor`        | Weather to push minor version tag.                                                                                               | true                |

### Action Outputs

| Name            | Description        |
| --------------- | ------------------ |
| `major_version` | Major version tag. |
| `minor_version` | Minor version tag. |

## Development

### Global dependencies

- nvm
- node

### Taskfile commands

For all commands see [Taskfile](Taskfile.yaml) or `task --list-all`.

## License

[MIT](LICENSE)
