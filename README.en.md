# HyperBackground

HyperBackground is an LSPosed/Xposed module for customizing backgrounds in HyperOS/MIUI system interfaces, especially parts of the Settings app and related system pages.

## Features

- Custom backgrounds for supported HyperOS/MIUI pages
- Separate background channels for Home, My Device, and Global pages
- Image and video background support
- Opacity and blur controls
- Text color customization
- Theme options including light, dark, follow system, Monet-based colors, and custom theme colors
- Compatibility logic for different HyperOS/MIUI page structures

## Notes

- Some newer HyperOS pages are rendered with Flutter or Rust-based UI layers. Traditional Android View-tree background injection may not work on those pages.
- The module includes compatibility fallbacks for older and supported page structures.
- Installed behavior may vary across HyperOS/MIUI versions and device builds.

## Project Structure

- `app/` — Android app and module source
- `app/src/main/res/values/strings.xml` — default strings
- `app/src/main/res/values-zh-rCN/strings.xml` — Simplified Chinese strings
- `CHANGELOG.md` — release notes

## Localization

This project already includes localized string resources. To improve English support:

- review `app/src/main/res/values/strings.xml`
- compare with `app/src/main/res/values-zh-rCN/strings.xml`
- move any hardcoded UI text in Kotlin/Compose files into string resources

## Module Type

This repository appears to provide:

- an Android configuration app
- an LSPosed/Xposed module hook implementation

Relevant indicators include packaged Xposed metadata and hook entry points.

## Disclaimer

Please use this project in accordance with the original author’s license and your local laws, platform rules, and device security practices.
