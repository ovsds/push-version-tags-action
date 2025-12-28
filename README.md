# Push Version Tags Action

[![CI](https://github.com/ovsds/push-version-tags-action/workflows/Check%20PR/badge.svg)](https://github.com/ovsds/push-version-tags-action/actions?query=workflow%3A%22%22Check+PR%22%22)
[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Push%20Version%20Tags-blue.svg)](https://github.com/marketplace/actions/push-version-tags)

Pushes supplementary (major, minor) version tags to a repository. It is useful for creating tags for major and minor versions based on a base version.
For example, if the base version is `v1.2.3`, it will create tags `v1` and `v1.2`.

## Usage

### Example

```yaml
name: Push version tags

on:
  release:
    types: [published]

jobs:
  push-version-tags:
    permissions:
      contents: write

    steps:
      - name: Push Version Tags
        id: push-version-tags
        uses: ovsds/push-version-tags-action@v1
        with:
          version: ${{ github.event.release.tag_name }}
```

### Action Inputs

```yaml
inputs:
  github_token:
    description: |
      Github token used for API calls. Required scope - 'contents: write'
    default: ${{ github.token }}

  owner:
    description: |
      Owner of the repository
    default: ${{ github.repository_owner }}

  repo:
    description: |
      Repository name
    default: ${{ github.event.repository.name }}

  version:
    description: |
      Base version to be used for tags. Should be in format {major}.{minor}.{patch} or v{major}.{minor}.{patch} (e.g. 1.2.3 or v1.2.3)
    required: true

  major:
    description: |
      Weather to push major version tag
    default: "true"

  minor:
    description: |
      Weather to push minor version tag
    default: "true"
```

### Action Outputs

```yaml
outputs:
  major_version:
    description: |
      Major version tag
    value: ${{ steps.prepare-versions.outputs.major_version }}

  minor_version:
    description: |
      Minor version tag
    value: ${{ steps.prepare-versions.outputs.minor_version }}
```

## Development

### Global dependencies

- [Taskfile](https://taskfile.dev/installation/)
- [nvm](https://github.com/nvm-sh/nvm?tab=readme-ov-file#install--update-script)

### Taskfile commands

For all commands see [Taskfile](Taskfile.yaml) or `task --list-all`.

## License

[MIT](LICENSE)
