# 35174

Reproduction for [Renovate issue 35174](https://github.com/renovatebot/renovate/discussions/35174).

## Current behavior

Renovate updates the version of `OpenTelemetry.Instrumentation.Http` even if it is pinned down to `[1.9.0]` in the ItemGroup for net8.0.

``` xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFrameworks>net8.0;net9.0</TargetFrameworks>
    </PropertyGroup>
    <ItemGroup  Condition="'$(TargetFramework)' == 'net9.0'" >
        <PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="1.11.0" />
    </ItemGroup>
    <ItemGroup  Condition="'$(TargetFramework)' == 'net8.0'" >
        <PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="[1.9.0]" />
    </ItemGroup>
</Project>

```
PullRequest: https://github.com/bjuraga/renovate-reproduce-nuget-pinning/pull/1/files

## Expected behavior

Renovate should respect the pinned version of `OpenTelemetry.Instrumentation.Http` in the ItemGroup for `net8.0` and should not updated it. Updating the net9.0 ItemGroup is as expected because in that ItemGroup the version is not pinned.
