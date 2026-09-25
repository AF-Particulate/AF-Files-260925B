<p align="center">
  <img alt="Files hero image" src="./assets/ReadmeHero.png" />
</p>

<p align="center">
  <a style="text-decoration:none" href="https://files.community/">
    <img src="https://img.shields.io/badge/Files-Website-F9B81F" alt="Files Website" /></a>
  <a style="text-decoration:none" href="https://github.com/files-community/Files/actions/workflows/ci.yml">
    <img src="https://github.com/files-community/Files/actions/workflows/ci.yml/badge.svg" alt="Files CI Status" /></a>
  <a style="text-decoration:none" href="https://crowdin.com/project/files-app">
    <img src="https://badges.crowdin.net/files-app/localized.svg" alt="Files Localization Status" /></a>
  <a style="text-decoration:none" href="https://discord.gg/files">
    <img src="https://img.shields.io/discord/725513575971684472?label=Discord&color=7289da" alt="Files Discord" /></a>
</p>

Files is a modern file manager that helps users organize their files and folders. Our mission with Files is to build the best file manager for Windows, and we’re proud to be building it out in the open so everyone can participate. User feedback helps shape the features we work on, & the bug reports on GitHub help to make Files more reliable. Built and maintained by the open-source community, Files features robust multitasking experiences, file tags, deep integrations, and an intuitive design.

## Installing and running Files

Files is a community-driven project that depends on your support to grow and improve. Please consider purchasing Files through the Microsoft Store or supporting us on GitHub if you use the classic installer.

You can also use the preview version alongside the stable release to get early access to new features and improvements.

<p align="left">
  <!-- Store Badge -->
  <a style="text-decoration:none" href="https://apps.microsoft.com/detail/9NGHP3DX8HDX?launch=true&mode=full">
    <picture>
      <source media="(prefers-color-scheme: light)" srcset="./assets/StoreBadge-dark.png" height="80" />
      <img src="./assets/StoreBadge-light.png" height="80" /></picture></a>
  &ensp;
  <!-- Classic Installer Badge -->
  <a style="text-decoration:none" href="https://files.community/download">
    <picture>
      <source media="(prefers-color-scheme: light)" srcset="./assets/ClassicInstallerBadge-dark.png" height="80" />
      <img src="./assets/ClassicInstallerBadge-light.png" height="80" /></picture></a>
</p>

## Building from source

Instructions for building the source code can be found on our [documentation site](https://files.community/docs/contributing/building-from-source).

### Packaging a Windows-installable artifact

GitHub Actions now includes a **Files Package Artifact** workflow that builds the existing MSIX packaging configuration and uploads the result as a workflow artifact. Open the workflow run in the **Actions** tab and download the **Files-MSIX-Package** artifact from the run summary.

For local Windows packaging, use a Visual Studio 2026 Developer PowerShell and run the same steps as CI:

```powershell
.\.github\scripts\Generate-SelfCertPfx.ps1 -Destination .\artifacts\signing\Files.Package.SelfSigned.pfx
msbuild -restore Files.slnx -p:Configuration=Release -p:Platform=x64 -v:quiet -clp:ErrorsOnly
nuget restore .\src\Files.App.Launcher\Files.App.Launcher.vcxproj -SolutionDirectory $PWD
msbuild .\src\Files.App.Launcher\Files.App.Launcher.vcxproj -t:Build -p:Configuration=Release -p:Platform=x64 -v:quiet -clp:ErrorsOnly
```

Then build the app packages for `x64` and `arm64`, run `.\.github\scripts\Create-MsixBundle.ps1`, and sign the resulting `.msixbundle` with the same certificate. If you configure the optional GitHub Actions secrets `WINDOWS_PACKAGE_CERTIFICATE_PFX_BASE64` and `WINDOWS_PACKAGE_CERTIFICATE_PASSWORD`, the workflow will use that certificate instead of the temporary self-signed one. The certificate must match the manifest publisher (`CN=Files` for the current dev package).

## Contributing to Files

Want to contribute to this project? Let us know with an [issue](https://github.com/files-community/Files/issues) that communicates your intent to create a [pull request](https://github.com/files-community/Files/pulls). Also, view our [contributing guidelines](https://github.com/files-community/Files/blob/main/.github/CONTRIBUTING.md) to make sure you're up to date on the coding conventions.

Looking for a place to start? Check out the [task board](https://github.com/orgs/files-community/projects/3/views/2), where you can sort tasks by size and priority.

## Screenshots

![Files](./assets/FilesScreenshot.png)
