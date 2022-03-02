# IT Core Actions

Core IT GitHub Actions and Workflows

## Workflows

### Build .NET

This workflow is used to build and test .NET Core projects.

#### Usage

```yaml
jobs:
  build:
    uses: vermeer-corp/it-core-actions/.github/workflows/build-dotnet.yml@v1
    with:
      publish-project: <ProjectToPublish>.csproj
      publish-path: <ProjectToPublish>/bin/Debug/net6.0/publish/*
      build-configuration: Debug
      dotnet-version: 6.0.x
      upload-artifact: true
```

### Refresh Axway

This workflow is used to refresh an API definition in Axway.

#### Usage

```yaml
refresh-axway:
  uses: vermeer-corp/it-core-actions/.github/workflows/refresh-axway.yml@v1
  with:
    deploy-environment: development
    axway-environment: dev
    axway-api-name: <API Name> API
    swagger-url: https://devapi.vermeer.com/<api-name>/swagger/v1/swagger.json
  secrets:
    axway-username: ${{ secrets.AXWAY_DEV_USERNAME }}
    axway-password: ${{ secrets.AXWAY_DEV_PASSWORD }}
    axway-org-id: ${{ secrets.AXWAY_DEV_IT_DEVELOPERS_ORG_ID }}
```
