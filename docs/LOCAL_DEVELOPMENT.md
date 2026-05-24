# Local Development

This project is meant to be easy to modify. The app is small, native Swift/AppKit, and built from the command line.

## Prerequisites

Install Apple Command Line Tools if Swift is not already available:

```bash
xcode-select --install
swift --version
```

## Iterate

After changing Swift files:

```bash
./build-app.sh
pkill -x ClickLight
open ClickLight.app
```

If `pkill` does not find a running app, that is fine. It just means ClickLight was not already open.

For a persistent install after your changes, follow [Installation](INSTALLATION.md).

## Useful Files

- `Sources/ClickLight/ClickEventTap.swift`: global mouse capture
- `Sources/ClickLight/OverlayCoordinator.swift`: one overlay per screen
- `Sources/ClickLight/ClickOverlayView.swift`: pulse drawing and animation
- `Sources/ClickLight/StatusController.swift`: menu-bar UI
- `Sources/ClickLight/SettingsStore.swift`: saved preferences
- `Info.plist`: app bundle metadata
- `build-app.sh`: command-line app bundle builder

## Debugging

Run the binary directly if the app does not appear in the menu bar:

```bash
ClickLight.app/Contents/MacOS/ClickLight
```

Other useful checks:

```bash
pgrep -fl ClickLight
defaults read dev.codex.ClickLight
defaults delete dev.codex.ClickLight
```

After deleting preferences, reopen the app.
