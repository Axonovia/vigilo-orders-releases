# Vigilo Orders releases

This public repository contains the official Windows distribution artifacts for **Vigilo Orders**.

The application source code and the ACS driver source code are maintained in private Axonovia repositories. Only verified release binaries, checksums, the Tauri update manifest and public release notes are published here.

## Downloads

Use the [latest stable release](../../releases/latest):

- the `setup.exe` is the supported installed version and receives signed in-app updates;
- the portable ZIP is intended for manual installation and recovery, and never auto-updates;
- the ACS bridge shipped in either package must stay with the matching Vigilo Orders version.

Every release includes `SHA256SUMS.txt` and `release-manifest.json`. Tauri update signatures protect the installer used by the application. Windows Authenticode signing is not currently applied, so Windows may still display an unknown-publisher warning.

Do not download or replace the ACS driver independently from Vigilo Orders.
