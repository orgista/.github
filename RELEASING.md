# Release process

How orgista apps are versioned, built and published, and what users can expect.

## Expectations

| | |
|---|---|
| Versions | [Semantic Versioning](https://semver.org/), tagged `vMAJOR.MINOR.PATCH`. `-beta.N` / `-rc.N` suffixes are pre-releases. |
| Cadence | Ship when a change is ready, and at least one maintenance release a month while a project is in active development. |
| Security fixes | Released within 7 days of a confirmed report. |
| Support | Only the latest release gets fixes. |
| Notes | Every release has a `CHANGELOG.md` section; the GitHub release notes are taken from it. |
| Integrity | Every release has a `SHA256SUMS` file and a GitHub attestation for each file. |
| Store builds | App Store, TestFlight, Mac App Store and Meta Horizon Store builds use the same version numbers as the GitHub release. |

## Where builds come from

Release builds are made and signed on our build Mac, never on a hosted CI runner, so signing keys
never leave it. GitHub Actions only checks pull requests (CI, CodeQL, Scorecard) and, once a release is
published, checks its files against `SHA256SUMS` and attests them (`release-attest.yml`). The
attestation proves a file is the one published in that repository's release; it does not describe the
build machine.

## Steps

1. Move the `## Unreleased` items in `CHANGELOG.md` under `## X.Y.Z - YYYY-MM-DD`; bump the app's version.
2. Merge to `main` through a pull request (squash).
3. Build and sign the release on the build Mac with the project's own build script.
4. Publish:

   ```bash
   scripts/release-github X.Y.Z path/to/artifact [more artifacts]
   # OpenPanel publishes its builds to the public releases repo:
   scripts/release-github --repo orgista/openpanel-releases X.Y.Z openpanel-X.Y.Z.apk
   ```

   The script tags `vX.Y.Z`, takes the notes from `CHANGELOG.md`, uploads the files plus `SHA256SUMS`,
   marks `-suffix` versions as pre-releases, refuses signing and secret files, and can be re-run (it
   replaces assets with the same name).
5. Check the release page: the notes, `SHA256SUMS`, and the `vX.Y.Z.intoto.jsonl` attestation bundle
   that `release-attest.yml` adds a minute later.
6. Submit the same build number to the stores.

## Repository setup

Each public repository has the same baseline, modelled on
[cyberbanksy/.eml](https://github.com/cyberbanksy/.eml):

- `Protect main` ruleset: no force pushes, no deleting `main`, Copilot code review on pull requests.
- Squash merge only; branches are deleted after merge.
- Dependabot alerts and security updates, weekly grouped version updates, secret scanning with push
  protection, private vulnerability reporting.
- Workflows: `ci.yml` (where the project builds on a hosted runner), `codeql.yml`, `scorecard.yml`,
  `release-attest.yml`. Actions are pinned to commit SHAs and run with read-only tokens by default.
- Community files come from this repository unless a project has its own.
