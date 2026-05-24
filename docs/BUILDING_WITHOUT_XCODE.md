# Building Without Xcode

ClickLight is a native macOS app, but it does not use an `.xcodeproj` or `.xcworkspace`.

Instead, it is built with Swift Package Manager from the command line and then wrapped into a standard macOS `.app` bundle.

## The Short Explanation

The project has a `Package.swift` file that defines one executable target:

```swift
.executableTarget(
    name: "ClickLight",
    path: "Sources/ClickLight"
)
```

When you run:

```bash
swift build -c release
```

Swift Package Manager compiles the app binary to:

```text
.build/release/ClickLight
```

macOS apps are bundles, so `build-app.sh` creates this folder structure:

```text
ClickLight.app
└── Contents
    ├── Info.plist
    ├── MacOS
    │   └── ClickLight
    └── Resources
```

Then it copies:

- `Info.plist` into `ClickLight.app/Contents/Info.plist`
- the compiled binary into `ClickLight.app/Contents/MacOS/ClickLight`

That is enough for Finder and `open` to treat it like a normal macOS app.

## The Build Script

The app is built with:

```bash
./build-app.sh
```

The script performs the same steps manually:

```bash
swift build -c release
rm -rf ClickLight.app
mkdir -p ClickLight.app/Contents/MacOS ClickLight.app/Contents/Resources
cp Info.plist ClickLight.app/Contents/Info.plist
cp .build/release/ClickLight ClickLight.app/Contents/MacOS/ClickLight
```

## Why This Works

Xcode is not the compiler. Xcode is an IDE and project system around Apple tooling.

The actual compiler and build tools can also be used directly from the command line through:

- `swift`
- `swiftc`
- Swift Package Manager
- Apple Command Line Tools

ClickLight uses AppKit and CoreGraphics APIs directly from Swift, so it can be compiled as a Swift package without creating an Xcode project.

## What This Does Not Do Yet

This local build flow does not currently handle:

- Developer ID signing
- notarization
- Sparkle or another auto-update mechanism
- installer packaging
- App Store distribution

For local use and open-source iteration, the current `.app` bundle is enough. For broad public distribution, signing and notarization should be added.
