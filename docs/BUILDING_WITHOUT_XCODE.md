# Building Without Xcode

ClickLight is a native macOS app, but it does not use an `.xcodeproj` or `.xcworkspace`.

It is a Swift Package Manager executable wrapped into a standard macOS `.app` bundle.

## Build Flow

`Package.swift` defines one executable target:

```swift
.executableTarget(
    name: "ClickLight",
    path: "Sources/ClickLight"
)
```

`swift build -c release` compiles the binary to:

```text
.build/release/ClickLight
```

`build-app.sh` then creates:

```text
ClickLight.app
└── Contents
    ├── Info.plist
    ├── MacOS
    │   └── ClickLight
    └── Resources
```

and copies the compiled binary and `Info.plist` into that bundle.

That is enough for Finder and `open` to treat it like a normal local macOS app.

## Why This Works

Xcode is not the compiler. Xcode is an IDE and project system around Apple tooling.

ClickLight uses AppKit and CoreGraphics APIs directly from Swift, so it can be compiled from the command line with Apple Command Line Tools and Swift Package Manager.

## Not Included Yet

This local build flow does not currently handle:

- Developer ID signing
- notarization
- auto-updates
- installer packaging
- App Store distribution
