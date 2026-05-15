# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-file bash CLI (`pushover`) that posts a message to the Pushover API. No build step, no dependencies beyond `curl`, no test suite. The entire program lives in `./pushover`; everything else is metadata (README, CHANGELOG, LICENSE, release workflow).

## Shell

This script is **bash**, not fish — the global preference for fish does not apply here. Use bash idioms when editing.

## Issue tracking

This project uses **GitHub Issues** (`gh issue ...`), not Beans. Do not invoke `work-on-bean` / `work-on-tree` here. Reference issues as `#N` in commits, e.g. `Closes #6`.

## Verifying changes

There are no tests. After editing the script:

```bash
bash -n pushover     # syntax check
./pushover --help    # eyeball usage output
./pushover --version # confirm VERSION literal
```

For functional checks, you'll need valid Pushover credentials in env, `./.pushover-cli`, or `~/.config/pushover-cli/global.env`.

## Token resolution chain

Implemented in `pushover` as flag → env → project config → global config, first match wins per key, no chaining. The project config (`./.pushover-cli`) is read from CWD only — there is no walk-up of parent directories. Both config files share the `read_config_file` helper and accept only `PUSHOVER_USER_KEY` and `PUSHOVER_APP_TOKEN`.

## Releasing

1. Bump `VERSION="x.y.z"` near the top of `pushover`.
2. Add a `## [x.y.z] - YYYY-MM-DD` section to `CHANGELOG.md`. The release workflow extracts this section as the GitHub release notes and **fails the job if the section is missing**.
3. Commit the CHANGELOG entry first (`docs:`), then the version bump (`chore(release): x.y.z`).
4. Tag annotated (`git tag -a vx.y.z -m vx.y.z`) and push (`git push --follow-tags` only pushes annotated tags; lightweight tags must be pushed explicitly).
5. `.github/workflows/release.yml` builds four target tarballs (linux/darwin × x86_64/arm64) and creates the GitHub release on the tag push.

## Commit conventions

Conventional Commits plus `del:` (removals) and `sec:` (security). Breaking changes use `!` after the type. See `~/.claude/rules/git.md` for the full list.
