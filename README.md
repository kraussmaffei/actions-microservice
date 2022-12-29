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
    uses: kraussmaffei/actions-microservice/.github/workflows/publish.yml@main
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

to use this workflow two files must be added to the repository

### workflow

add in `.github/workflows` directory

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
    uses: kraussmaffei/actions-microservice/.github/workflows/publish-docker.yml@main
    with:
      aws-account-id: <your-account-id>
    secrets:
      user-token: <your-user-token>
      pip-index-url: <your-pip-index-url>
      pip-extra-index-url: <your-pip-extra-index-url>
```

### semantic release configuration

in the root dir add a `.releaserc` file containing:

```json
{
  "branches": [
    "main"
  ],
  "plugins": [
    "@semantic-release/commit-analyzer",
    "@semantic-release/release-notes-generator",
    "@semantic-release/changelog",
    "@semantic-release/git",
    "@semantic-release/github"
  ]
}
```
