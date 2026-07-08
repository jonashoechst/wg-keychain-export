# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Calendar Versioning](https://calver.org/) (`YYYY.MM.MICRO`).

## [Unreleased]

## [2026.07.1] - 2026-07-08

### Added

- `wg-keychain-export` script to list and export WireGuard tunnel configs from the macOS Keychain to wg-quick compatible `.conf` files
- Support for `--keychain`, `--output`, `--tunnel`, and `--list` options
- README with installation, usage, and limitations
- `.gitignore` for exported configs (`wg-quick/`) and `.DS_Store`
- MIT `LICENSE` file
- GitHub Actions workflow for ShellCheck and shfmt (`.github/workflows/shell-check.yml`)
- README badges for CI status, license, version, platform, and shell
- Calendar versioning (`2026.07.1`) with `VERSION` file and `-V` / `--version` flag
