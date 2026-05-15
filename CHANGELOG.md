# Changelog

All notable changes to this project are documented here. Format loosely follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); the project uses [Semantic Versioning](https://semver.org/).

## [2.1.0] - 2026-05-15

### Added

- Per-project config file: `./.pushover-cli` is read from the current working directory between environment variables and the global config. Same `KEY="value"` format and recognized keys (`PUSHOVER_USER_KEY`, `PUSHOVER_APP_TOKEN`) as `global.env`. No walk-up of parent directories. (#6)
- Running `pushover` with no arguments now prints the help text and exits 0, instead of failing with a missing-token error. (#5)

## [2.0.0] - 2026-05-13

This is the first release of the Zottmann fork, based on [aaronfagan/pushover-cli](https://github.com/aaronfagan/pushover-cli). It is not backward-compatible with the original.

### Changed

- **BREAKING:** Reworked the CLI around named flags. Tokens are supplied via `--user` / `--token`, the `PUSHOVER_USER_KEY` / `PUSHOVER_APP_TOKEN` environment variables, or `~/.config/pushover-cli/global.env`. Resolution is flag → env → config file, first match wins per key, no chaining.

### Removed

- **BREAKING:** Removed `install.sh` and the self-update flow. Install via `mise use github:czottmann/pushover-cli` or grab the script from the releases page.

### Added

- GitHub Actions release workflow that builds tarballs and a release on tag push.
