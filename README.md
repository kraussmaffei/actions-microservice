# actions-publish-microservice

An action to publish microservices and create a pull request on the associated balena repos.

## Publish a python microservice

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
    uses: kraussmaffei/actions-microservice/.github/workflows/publish-python.yml@main
    with:
      aws-account-id: <your-account-id>
      codeartifact-repository: <your-codeartifact-repository>
    secrets:
      pip-index-url: <your-pip-index-url>
      pip-extra-index-url: <your-pip-extra-index-url>
      user-token: <your-user-token>
      sonar-token: <your-sonar-token>
```

## Publish a third party docker microservice

```yaml
name: Continuous Integration

on:
  push:
    branches: ["main"]

concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: false

jobs:
  publish-microservice:
    uses: kraussmaffei/actions-microservice/.github/workflows/publish-docker.yml@main
    with:
      aws-account-id: <your-account-id>
    secrets:
      user-token: <your-user-token>
      pip-index-url: <your-pip-index-url>
      pip-extra-index-url: <your-pip-extra-index-url>
```

### Advanced semantic release settings

We use [semantic release](https://github.com/semantic-release/semantic-release) for automated versioning and release creation. For an andvanced usage of semantic release it is possible to provide a semantic release [configuration](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/configuration.md#configuration-file) in your repository. If you want to enable this option use the workflow below.

```yaml
name: Continuous Integration

on:
  push:
    branches: ["main"]

concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: false

jobs:
  publish-microservice:
    uses: kraussmaffei/actions-microservice/.github/workflows/publish-docker.yml@main
    with:
      aws-account-id: <your-account-id>
      use-semantic-release-configuration-file: true
    secrets:
      user-token: <your-user-token>
      pip-index-url: <your-pip-index-url>
      pip-extra-index-url: <your-pip-extra-index-url>
```
