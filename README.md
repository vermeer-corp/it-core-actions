# IT Core Actions

Core IT GitHub Actions and Workflows

## Workflows

### Build .NET

This workflow is used to build and test .NET Core/5/6 projects with the dotnet CLI.

#### Usage

```yaml
jobs:
  build:
    uses: vermeer-corp/it-core-actions/.github/workflows/build-dotnet.yml@v2
    with:
      publish-project: <ProjectToPublish>.csproj
      publish-path: <ProjectToPublish>/bin/Debug/net6.0/publish/*
      build-configuration: Debug
      dotnet-version: 6.0.x
      upload-artifact: true
    secrets:
      github-token: ${{ secrets.GITHUB_TOKEN}}
```

#### Parameters

##### publish-project

The path to the csproj file within the solution containing the final project to publish.

##### publish-path

The path to the final build outputs to be published.

##### build-configuration

The build configuration to use when building the project.

##### dotnet-version

The version of the dotnet SDK to use when building the project.

##### upload-artifact

A boolean value indicating whether to upload the build artifact to GitHub.

##### github-token

The GitHub Actions token to use to authenticate to the Vermeer GitHub Packages NuGet repository. This should always be set to `${{ secrets.GITHUB_TOKEN}}` in the calling workflow as shown above.

---

### Build .NET Framework 4.x

This workflow is used to build and test .NET Framework 4.x projects with MSBuild.

#### Usage

```yaml
jobs:
  build:
    uses: vermeer-corp/it-core-actions/.github/workflows/build-net-framework.yml@v3
    with:
      publish-project: <ProjectToPublish>.csproj
      publish-path: <ProjectToPublish>/bin/Debug/net6.0/publish/*
      build-configuration: Debug
      msbuild-args: /t:Package /t:TransformWebConfig /p:ExcludeXmlAssemblyFiles=false /p:AutoParameterizationWebConfigConnectionStrings=False
      test-file-glob: "**/*.Test.dll"
      upload-artifact: true
    secrets:
      github-token: ${{ secrets.GITHUB_TOKEN}}
```

#### Parameters

##### publish-project

The path to the csproj file within the solution containing the final project to publish.

##### publish-path

The path to the final build outputs to be published.

##### build-configuration

The build configuration to use when building the project.

##### msbuild-args

Any additional command line arguments to pass to MSBuild. If you are converting a Bamboo build process, see the MSBuild task in the Bamboo build for what these arguments might be. `/p:Configuration=\<Build Configuration\>` is already set with the `build-configuration` parameter.

##### test-file-glob

A glob pattern to match compiled MSTest DLL assemblies to run unit tests. If the parameter is empty, no unit tests will be run.

##### upload-artifact

A boolean value indicating whether to upload the build artifact to GitHub.

##### github-token

The GitHub Actions token to use to authenticate to the Vermeer GitHub Packages NuGet repository. This should always be set to `${{ secrets.GITHUB_TOKEN}}` in the calling workflow as shown above.

---

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

---

### Dotnet NuGet CI/CD

This workflow is used to build, test, and publish all NuGet packages in a .NET Core/5/6 project using the dotnet CLI.

#### Usage

```yaml
nuget:
  uses: vermeer-corp/it-core-actions/.github/workflows/dotnet-nuget-ci-cd.yml@v2
  with:
    dotnet-version: 6.0.x
    publish-package: true
  secrets:
    github-token: ${{ secrets.GITHUB_TOKEN }}
```
