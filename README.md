# DiskCapa

The public home of DiskCapa, a native macOS app for finding reclaimable disk space on developer machines.

- [Website](https://noinnion.com/DiskCapa/)
- [Downloads and release notes](https://github.com/noinnion/DiskCapa/releases)
- [Sparkle update feed](https://noinnion.com/DiskCapa/appcast.xml)

The current release is 1.0.3, signed with a Developer ID and notarized by
Apple. The app requires macOS 14 or later.

## This repository

This repository contains the static website and update feed. App source code
is maintained separately. Download archives belong in GitHub Releases, not in
Git history.

GitHub Pages serves the root of the `main` branch. `.nojekyll` keeps the files
unchanged. The site inherits `noinnion.com` from the organization's Pages site;
it does not need its own CNAME file. The site has no build dependencies,
analytics, or external fonts.

To preview locally, run `python3 -m http.server 8000` in this directory and open
`http://localhost:8000`.

## Publishing an app update

1. Build, Developer ID sign, notarize, and staple the app.
2. Preserve each release archive under a unique, versioned filename.
3. Create a GitHub Release here and upload the archive. Verify its public download URL.
4. Use Sparkle's `generate_appcast` with that release's download URL prefix to
   generate a signed item. Keep existing published items when updating the feed.
5. Commit the generated `appcast.xml` here and push to `main`.
6. Verify the deployed feed and test upgrading from an older configured app.

Increment `CFBundleVersion` for every update: installs are offered an update on
that number, not on the marketing version, so a release that reuses it is
invisible to every copy already out there. Keep the private EdDSA signing key in
the release machine's Keychain; never put it in this repository. Every published
item carries a signature, and an unsigned one is refused by every install.

Copyright © 2026 noinnion. All rights reserved.
