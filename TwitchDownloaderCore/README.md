# Nuget Package Management

This is just a proxy project for hosting TwitchDownloaderCore library onto Github's package repository.

## Steps

1. Sync solution with the parent solution (https://github.com/lay295/TwitchDownloader)
   - If your OS is not Windows, the TwitchDownloaderWPF project will throw a thousand scary errors. That is OK since we are not building a WPF app.
2. Update the package version number in TwitchDownloaderCore.csproj to the parent's release number.
    - Eg: Change 1.1.16 --> 1.54.2
    - Github repository forbids repeat/duplicate version numbers. So we need to bump up the version number every time.
3. Build TwitchDownloaderCore in **release** mode.
4. Go to the built Nuget package and run the following command.

```txt
dotnet nuget push {{ NEW_NUPKG }} --source "github" --api-key {{ GITHUB_PAT }}
```

## How to add Github feed as a source

### Programmatically (eg. Linux or MacOS)

Edit the `Nuget.config` file, usually located in:

```txt
$HOME/.nuget/NuGet/
```

https://docs.servicestack.net/gh-nuget#requires-github-authentication 

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="github" value="https://nuget.pkg.github.com/GITHUB_USERNAME/index.json" />
  </packageSources>
  <packageSourceCredentials>
        <github-servicestack>
            <add key="Username" value="GITHUB_USERNAME" />
            <add key="ClearTextPassword" value="PERSONAL_ACCESS_TOKEN" />
        </github-servicestack>
    </packageSourceCredentials>
</configuration>
```

### Visual Studio (eg. Windows)

https://docs.servicestack.net/gh-nuget#add-using-vs.net 
