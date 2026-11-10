# Octri GitHub Action

Push your OpenAPI spec to [Octri](https://octri.dev) from CI. Octri republishes your docs, MCP server and changelog from the new spec, and can build your SDKs in the same run.

The action runs [`@octri/cli`](https://www.npmjs.com/package/@octri/cli). It waits for the spec to finish processing and fails the step if it doesn't.

## Usage

```yaml
name: Publish API
on:
  push:
    branches: [main]
    paths: [openapi.yaml]

jobs:
  octri:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: OctriDev/octri-action@v1
        with:
          api-key: ${{ secrets.OCTRI_API_KEY }}
          project-id: ${{ vars.OCTRI_PROJECT_ID }}
          spec: openapi.yaml
```

## Inputs

| Input | Required | Default | |
|---|---|---|---|
| `api-key` | yes | | An Octri API key, from Settings, API keys. Store it as a secret. |
| `project-id` | yes | | The project to push to. `octri projects list` prints it. |
| `spec` | yes | | Path to the spec, YAML or JSON. |
| `build-sdks` | no | `false` | Also build the SDKs. The step fails if any language fails. |
| `cli-version` | no | `1.0.8` | The `@octri/cli` version to run. |
