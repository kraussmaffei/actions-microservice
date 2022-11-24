# actions-publish-microservice

An action to publish microservices and create a pull request on the associated balena repos.

## Usage

```yaml
name: Continuous Integration

on:
  push:
    branches: ["main"]
  pull_request:
    branches: ["main"]

concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: false

jobs:
  publish-microservice:
    uses: kraussmaffei/actions-publish-microservice/.github/workflows/publish.yml@main
    secrets: inherit
```