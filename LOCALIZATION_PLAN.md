# App English Localization Plan

## Proposed PR title

**Add English app localization resources and remove hardcoded UI text**

## Summary

This follow-up PR should improve English localization for the HyperBackground app UI without changing module behavior.

## Scope

Only localization-related changes:

- string resources
- replacing hardcoded UI text with resource references
- no hook logic changes
- no behavior changes
- no build/signing changes

## Likely files

### Resource files
- `app/src/main/res/values/strings.xml`
- `app/src/main/res/values-zh-rCN/strings.xml`

### UI files
- `app/src/main/java/com/ciallo/hyperbackground/ui/MainActivity.kt`
- `app/src/main/java/com/ciallo/hyperbackground/ui/pages/HomePage.kt`
- `app/src/main/java/com/ciallo/hyperbackground/ui/pages/SettingsPage.kt`
- `app/src/main/java/com/ciallo/hyperbackground/ui/pages/BackgroundDetailPage.kt`
- `app/src/main/java/com/ciallo/hyperbackground/ui/pages/ChangelogPage.kt`
- `app/src/main/java/com/ciallo/hyperbackground/ui/pages/UpdateAvailableDialog.kt`

## Planned changes

1. Compare default and Chinese string files
2. Add missing English entries
3. Improve awkward English wording
4. Find and replace hardcoded Chinese UI text in Kotlin/Compose
5. Verify locale behavior for English and Chinese

## Non-goals

- no hook logic changes
- no scope changes
- no package/signing changes
- no release workflow changes

## Suggested commit structure

1. Add missing English string resources
2. Refine English UI wording
3. Replace hardcoded UI text with string resources

## Acceptance checklist

- [ ] English strings exist for all major UI labels
- [ ] No visible hardcoded Chinese remains in main UI pages
- [ ] Chinese locale still works
- [ ] English fallback works
- [ ] No app behavior changed
