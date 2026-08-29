# Release Notes

GitHub Actions extracts the section matching the APK’s actual `versionName` and writes it into the GitHub Release description. If the version name contains `test`, `alpha`, `beta`, `rc`, or `dev`, it is automatically marked as a pre-release.

## 1.3.9

- Consolidates fixes from the 1.3.8 test line and releases them as a stable version.
- Fix: Restored the Settings home background channel. `com.android.settings.MiuiSettings` is the only lifecycle hook entry used to mount `applyHome`; it was accidentally removed earlier, causing the home background to stop working in both light and dark themes.
- Fix: When typing into Settings search, the whole page briefly turned black. The search loading layer and window-level search overlay are now transparent.
- Improvement: Restored desktop settings background logic to a verified working state, while keeping the old OS3 desktop settings background path.
- New: The About page’s “Current Version Notes” now reads dynamically from the packaged `CHANGELOG.md`, matching the current version. It supports multiple list marker styles, skips code blocks, normalizes version matching, and falls back to the latest notes if no exact match is found.
- Note: The LSPosed module description was expanded into a feature overview for easier understanding in the module list.
- Fix: Some module repository clients could not read the description. `xposeddescription` was changed from a `@string/...` resource reference to a literal manifest string because some clients only read raw manifest values.
- Compatibility: Current HyperOS desktop secondary settings pages are rendered with Flutter/Rust, so View-tree background injection does not work there. This version only ensures older desktop settings background paths are not broken.

## 1.3.8-test6

- New: The About page’s “Current Version Notes” now dynamically reads the matching section from `CHANGELOG.md`; if no exact version is found, it falls back to the latest entry and shows the actual running version.
- Improvement: Removed invalid leftover hooks for desktop settings (`MiuiSettings` lifecycle and precise hooks for native `com.miui.home` Activity), confirmed by decompilation and runtime logs to never be hit.
- Fix: Restored desktop settings background logic to the working state from test5, brought back the `home` branch short-circuit check, and reverted early test6 changes made for Flutter desktop adaptation.
- Compatibility: Current HyperOS desktop secondary settings pages are rendered with Flutter/Rust, so View-tree background injection does not work there; this version only preserves the previously working path on old OS3 desktop settings.
- Compatibility: Only desktop settings were adjusted; existing working logic such as transparent Settings search overlay was not affected.
- Testing focus: About page version notes display, desktop settings page background, page enter/exit behavior, and existing Settings search.

## 1.3.8-test5

- Fixes the issue where typing into Settings search briefly turned the whole page black; the search loading layer and window-level search overlay are now transparent.
- Testing focus: search bar input, search result loading, and background continuity in dark theme.

## 1.3.8-test4

- Removed global background reapplication when the window regains focus to avoid black flicker when the search bar gains focus or the keyboard appears.
- Removed the global layout listener to avoid recursive rescanning and clearing of the whole view tree during search input, result refresh, and keyboard size changes.
- The global background is still mounted as needed during Activity creation, resume, and content replacement, while keeping lifecycle deduplication.
- Testing focus: continuous search input, keyboard pop-up, search result refresh, and secondary menu entry speed.

## 1.3.8-test2

- Fixed host detection for the background on the Phone Services “Mobile Data” secondary page by checking whether the parent of `android.R.id.content` is `ActionBarOverlayLayout`.
- When a MIUIX transition container is detected, the custom background is mounted to the parent to prevent it from sliding with the page and ghosting with the old page.
- If no known hierarchy is detected, it still falls back to the content layer host for compatibility across HyperOS versions.
- Testing focus: enter/exit transition of the Mobile Data page, background continuity, and page rendering after returning.

## 1.3.7-test3

- On MIUIX secondary pages, the global background is elevated to the root layer only when `ActionBarOverlayLayout` is detected; it no longer touches `DecorView`.
- The status bar, navigation/back area, and large-title area are made transparent so the background extends to the top of the screen.
- Directly clears the primary background drawn inside `ActionBarContainer`, fixing cases where normal `View.background` clearing was ineffective.
- Keeps the native semi-transparent styles for top feature cards, privacy page switch bars, and content cards.
- Previously working device interconnect and power-saving management still use content-layer mounting and do not enter top-bar elevation logic.
- The test build returns to the official package name `com.ciallo.hyperbackground`, uses the same private release signature as the stable version, and is marked as pre-release on GitHub so it can be installed over the stable version.
- Scope validation increased from 8 items to 9, adding `com.xiaomi.misettings`.

## 1.3.7-test2

- Reverted the incorrect DecorView bottom-layer mounting from 1.3.7-test; device interconnect returns to the verified `android.R.id.content` implementation from 1.3.6.
- Phone Services, Xiaomi Account, Themes/Wallpapers, Security Center, and other standard Android/Miuix pages now consistently use content-layer backgrounds and keep repeated mounting after async layout.
- Added `com.xiaomi.misettings` scope to cover pages such as Digital Wellbeing that are hosted by a separate app.
- Added an Instrumentation lifecycle fallback to handle pages that do not pass through standard base Activity callbacks.
- Xposed runtime fields for stable and test builds are isolated by package name to avoid session conflicts when both modules are installed.
- Added hook read logging so you can directly confirm whether the target process was injected and read the global background.
- Since the system launcher is a Flutter/Rust shared runtime page, this test build keeps only injection diagnostics and no longer uses a generic Surface overlay that caused regressions elsewhere.
- The test package continues using `com.ciallo.hyperbackground.test` and a debug certificate, so it does not overwrite or alter stable 1.3.6.

## 1.3.7-test

- First round of multi-app background hook compatibility testing (replaced by 1.3.7-test2).

## 1.3.6

- Global background support added for Phone Services, Xiaomi Account, Themes/Wallpapers, system launcher, Security Center, and Power Saver.
- Standard secondary Settings pages continue using the global channel, while the Settings home page and “My Device” remain separate.
- Login, authorization, lockscreen credentials, payments, dialer, emergency calls, and floating windows keep the system default appearance.
- Palette upgraded to 12 preset colors, HSV hue/saturation/value sliders, and editable HEX input.
- HEX input supports `#RRGGBB` and `#AARRGGBB`, and uses an ASCII keyboard for entering A–F.
- Fixed local build artifact filenames not matching the APK’s actual version.
- Release builds now use GitHub Actions Secrets to inject a private PKCS#12 key; the repository no longer stores signing files or passwords.
- Version 1.3.6 is the starting point for private signing migration and is not signature-compatible with 1.3.5 or earlier public-signed builds.

## 1.3.5

- Removed redundant HyperOS / Compose / MIUIX intro cards from the background page.
- Added stable-version verification, latest stable-version status, and current release notes to the About page.
- Fixed a bug where Miuix custom theme colors did not enter the Monet seed color flow, causing the palette to always appear blue.
- Stable version checking now only reads GitHub `releases/latest` and will not mistake test/alpha/beta/rc releases for stable updates.
- Package name and fixed signature remain unchanged, so it can be installed over older versions.

## 1.3.3-test

- Completely removed the broken “theme channel experiment,” including config UI, Provider fields, hook entry points, and implementation classes.
- Global backgrounds continue to be handled through the Activity lifecycle and page root containers, without intercepting system theme attributes.
- README now keeps only current stable-version info; test changes are concentrated in this file and GitHub Releases.
- Build pipeline now automatically generates release notes, build info, and fixed-signature info for both stable and test builds.
- Package name and fixed signature remain unchanged, so it can be installed over older versions.

## 1.3.2-test

- When no custom background is set, the base color follows the MIUIX light or dark theme.
- Added module card opacity, and clarified the old opacity option as background image opacity.
- Added a “Hitokoto” quote area under the HyperBG large title, supporting refresh, custom API, and JSON path fields.
- Keeps three separate background channels: Home, My Device, and Global.

## 1.3.1

- Configuration UI migrated to Kotlin, Jetpack Compose, and Miuix KMP.
- Added light mode, dark mode, follow system, Monet wallpaper color extraction, and custom theme colors.
- Reorganized the three background channels: Home, My Device, and Global.
- Kept media selection, opacity, blur, text color, and Settings appearance options.
- Added links to the author Cangcu, CoolApk, and GitHub.
- Fixed module signing so future versions can be installed over older ones.
