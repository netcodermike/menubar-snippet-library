# Menubar Snippet Library

Store named local text snippets in a Mac menu and copy them only on explicit selection.

[![Build and verify](https://github.com/netcodermike/menubar-snippet-library/actions/workflows/verify.yml/badge.svg)](https://github.com/netcodermike/menubar-snippet-library/actions/workflows/verify.yml)

**Language:** Swift · **Platform:** macOS desktop · **App type:** Mac local snippet manager

First-release learning implementation, with explicit scope below. This is one independently runnable app, not a placeholder in a combined repository.

## Features

- Menu bar snippet picker
- Add title/text dialog
- Atomic local JSON storage
- No clipboard monitoring

## Requirements

macOS 13+ and Xcode command-line tools supporting Swift 5.9+. No external packages.

## Quick start

```sh
git clone https://github.com/netcodermike/menubar-snippet-library.git
cd menubar-snippet-library
swift build
swift run LocalApp
```

Commands run from the repository root. Lines marked for a particular operating system apply only there. Language tools are prerequisites, not installed by the app. Close desktop windows normally; terminal/server apps stop with Ctrl+C unless their usage notes say otherwise.

## Example workflow

Launch, add a synthetic greeting, select its menu item, paste into a test editor, quit/relaunch, and confirm the snippet remains.

## Architecture, configuration, and data

App.swift validates at most 100 Codable snippets with title length 1–80 and text length ≤20000, loads from ~/Library/Application Support/NetCoderMikeSnippets/snippets.json, and writes updated arrays atomically. Clicking a snippet replaces the system clipboard with its text. Corrupt/invalid stored data disables adding instead of overwriting the file. Tests verify schema and Codable round trips without reading the clipboard.

## Verification

Build with the quick-start command where needed, then run:

```sh
swift run LocalApp --self-test
```

Manual acceptance: Launch, add a synthetic greeting, select its menu item, paste into a test editor, quit/relaunch, and confirm the snippet remains. Also test malformed inputs and an unwritable output destination.

See [validation record](docs/VALIDATION.md) for observed checks and their limits. CI results verify only what the workflow runs; they do not establish native GUI correctness or production readiness.

## Limitations and next steps

No edit/delete UI, expansion shortcuts, launch-at-login, sync, encryption, imports/exports, password storage, or clipboard history. Plaintext snippets can be read by your user account and backups. Selecting a snippet replaces existing clipboard contents. Large menus and title truncation depend on macOS.

## Troubleshooting

Use the exact platform/toolchain above. Preserve originals and use synthetic fixtures first. Errors are displayed in the UI or stderr. A headless machine can run the model tests but cannot verify native GUI/audio behavior. Output paths are chosen explicitly; keep backups of important data.

## Source map

- `Package.swift`
- `Sources/LocalApp/App.swift`

## Development and license

Read [contributing](CONTRIBUTING.md) before changing the app, and [security/privacy](SECURITY.md) before supplying private data. Use synthetic fixtures for tests. No telemetry, paid API key, or account is required by the app itself. Dependencies, when present, are stated in Requirements.

[MIT license](LICENSE), copyright 2026 netcodermike.
