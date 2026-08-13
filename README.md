# Vigilo Orders releases

This public repository is the official Windows binary distribution channel for
**Vigilo Orders**. Application source and ACS driver source remain in private
Axonovia repositories. No signing private key, password, API secret or standalone
ACS driver is stored here.

## Download the latest stable version

Open the [latest stable release](../../releases/latest) and choose one package:

- `Vigilo-Orders_<version>_windows-x86_64-setup.exe` is the supported installed
  edition. It can detect signed stable updates inside Vigilo Orders, asks the
  user before installation, stops the bundled ACS bridge safely, installs the
  matching setup and restarts the application.
- `vigilo-orders_<version>_windows-x86_64-portable.zip` is the portable/recovery
  edition. It never auto-updates; download a newer ZIP and replace the complete
  portable folder manually.

Keep `vigilo_orders.exe` and its sibling `acs-bridge/` directory together. The
bridge is versioned and tested with the application; do not copy a bridge from a
different release or download one independently.

Debug/diagnostic builds are private support artifacts and are never published in
this repository.

The current stable and portable Windows artifacts are built for the dedicated
Vigilo Orders API at:

```text
https://orders-api.162.19.72.42.sslip.io
```

The exact origin embedded in each version is recorded in
`release-manifest.json`. Changing that server requires a newly built release;
downloading a different ACS bridge or editing local files is not supported.

## Update behavior

Only the installed edition contacts this repository's stable update manifest:

```text
https://github.com/Axonovia/vigilo-orders-releases/releases/latest/download/latest.json
```

Checks are non-blocking. A new version displays release notes and requires an
explicit **Install and restart** action. A failed download or invalid signature
leaves the current installation untouched. Portable and debug editions do not
use this endpoint.

## Verify a release

Every stable release contains exactly:

```text
Vigilo-Orders_<version>_windows-x86_64-setup.exe
Vigilo-Orders_<version>_windows-x86_64-setup.exe.sig
vigilo-orders_<version>_windows-x86_64-portable.zip
latest.json
release-manifest.json
SHA256SUMS.txt
```

- `SHA256SUMS.txt` records the SHA-256 digest of every other public asset.
- `release-manifest.json` records the private source commit, pinned ACS driver
  commit, API origin, build flavors, file sizes and artifact hashes.
- `latest.json` is the Tauri stable update contract and includes the setup URL
  plus its signature.
- the `.sig` is a Tauri updater signature over the complete setup. Installed
  clients verify it against the public key compiled into Vigilo Orders before
  launching the installer.

Tauri updater signing and Windows Authenticode are separate. Authenticode is not
currently applied, so Windows SmartScreen can still display an unknown-publisher
warning even though Vigilo Orders verifies updater integrity cryptographically.

Published release tags and assets are treated as immutable. A correction or
rollback is published as a new, higher stable version rather than replacing an
existing file.

## Support

Download only from the Axonovia release page linked above. If a checksum fails,
the updater reports a signature error, or the application/ACS bridge versions do
not match, stop and contact Axonovia support instead of bypassing verification.
