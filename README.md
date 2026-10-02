# Caliber

Caliber is a macOS app that benchmarks AI coding agents against your own
codebase. It reads your local Claude Code sessions (`~/.claude`) and the
repositories they ran in, so you can see what the agent did and what it cost.
Everything stays on your machine.

This repository only holds release builds. The source code is not public.

**[Download the latest build →](https://github.com/k1ausai/caliber-releases/releases/latest)**

## Requirements

- A Mac with Apple silicon (M1 or later). There is no Intel build.
- macOS 13 or later.

You don't need Python, Node, or a GitHub account.

## Install

1. From the [latest release](https://github.com/k1ausai/caliber-releases/releases/latest),
   download `Caliber-<version>-arm64.zip` and unzip it.
2. Move `Caliber.app` to `/Applications`.
3. **macOS will block the app the first time you open it.** These are
   development builds: they are signed ad hoc, not notarized by Apple, so
   Gatekeeper can't check who made them. To unblock it, remove the quarantine
   flag that macOS added during the download:

   ```bash
   xattr -dr com.apple.quarantine /Applications/Caliber.app
   ```

   If you'd rather not use the terminal: open the app, let macOS block it, then
   go to **System Settings → Privacy & Security** and click **Open Anyway** next
   to the message about Caliber. On macOS 15 and later, right-click → Open no
   longer bypasses the block.

4. Open Caliber. The first launch sets up its database before the window
   shows anything, so give it a few seconds.
5. Allow the folder-access prompts. Caliber reads `~/.claude` and the
   repositories your sessions ran in. If you deny them, the app still runs but
   shows nothing. To allow access later, go to
   **System Settings → Privacy & Security → Files and Folders**.

Caliber keeps its data in `~/Library/Application Support/Caliber/`.

## What to expect from development builds

- **macOS asks for folder access again after every update.** Without a
  developer signature, macOS identifies the app by a hash of its binary, so it
  treats each new build as a different app. This goes away once builds are
  signed with a Developer ID.
- **Updates are manual.** Download the new zip and replace the app in
  `/Applications`. Your data in `~/Library/Application Support/Caliber/` is kept.

## Check which version you have

The status badge on the Explore page shows `v<version>`. You can also run:

```bash
/usr/libexec/PlistBuddy -c 'Print CFBundleShortVersionString' \
  /Applications/Caliber.app/Contents/Info.plist
```

## Troubleshooting

**Nothing happens when I open it.** An app opened from Finder has no terminal,
so startup errors aren't shown anywhere. Run the app's binary directly to see the
error:

```bash
/Applications/Caliber.app/Contents/MacOS/Caliber
```

**GitHub details are missing or the menu bar shows `⚡ —`.** Caliber looks for
`gh` and `claude` in `~/.local/bin`, `/opt/homebrew/bin` and `/usr/local/bin`.
If they're installed somewhere else, the app still works but leaves those
details blank.

## License

Copyright © Klaus AI GmbH. All rights reserved.

These builds are provided for evaluation. No license to the software or its
source code is granted, and you may not redistribute it.
