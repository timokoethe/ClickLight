# Manual Install

Use this if you want to build ClickLight from source and install the app yourself instead of using Homebrew.

## Build And Copy

From the project root:

```bash
chmod +x build-app.sh
./build-app.sh
mkdir -p "$HOME/Applications"
cp -R ClickLight.app "$HOME/Applications/ClickLight.app"
open "$HOME/Applications/ClickLight.app"
```

You can also drag `ClickLight.app` into `/Applications` in Finder.

## Accessibility Permission

ClickLight needs Accessibility permission to detect clicks outside its own menu-bar app.

After launching ClickLight, open:

```text
System Settings -> Privacy & Security -> Accessibility
```

Enable `ClickLight`, then quit ClickLight from the menu bar and reopen it.

## Rebuild After Changes

After changing source files:

```bash
./build-app.sh
pkill -x ClickLight
cp -R ClickLight.app "$HOME/Applications/ClickLight.app"
open "$HOME/Applications/ClickLight.app"
```

## Remove Manual Install

```bash
rm -rf "$HOME/Applications/ClickLight.app"
defaults delete dev.codex.ClickLight
```
