# Security Review

This fork was scanned before republishing under `nishant32f`.

## Verdict

No malicious code was found in the current source tree.

The review found no runtime network client, shell/process execution, AppleScript, dynamic loading, keychain access, pasteboard access, accessibility capture, global event tap, screen capture, hidden LaunchAgent creation, suspicious entitlement, external package dependency, shell-script build phase, or bundled executable payload.

## Reviewed Areas

- Swift runtime code under `Sources/App/`
- Xcode project and shared scheme files
- XcodeGen `project.yml`
- Documentation and install instructions
- Asset catalogs and bundled image files
- Executable-file inventory

## Expected Sensitive Behavior

- The app stores copied JPEGs and `photos.json` under `~/Library/Application Support/PhotoWidget/`.
- The app can register itself as a login item only through the user-visible Launch at Login menu/settings control.
- The app creates borderless desktop-level windows for the selected photos.

## Non-Blocking Hardening Note

`PhotoItem.filename` is loaded from persisted JSON and later used for image load/delete paths. Normal app flow generates UUID `.jpg` filenames, but validating that the stored value is a basename before use would make local same-user tampering more robust.

Full scan artifacts from this run were written to:

`/tmp/codex-security-scans/PhotoWidgetOSX/6647d347f3df_20260614T061156Z/`
