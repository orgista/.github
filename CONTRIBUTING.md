# Contributing

Thanks for helping. These rules apply to every orgista repository; a repository's own README or
`CONTRIBUTING.md` adds its build and test steps.

## Issues

- Search existing issues first.
- Bug reports need the app version, device and OS, and steps to reproduce.
- Security problems go through private reporting, see [SECURITY.md](SECURITY.md).

## Pull requests

- One fix or feature per pull request, with a short description of how you tested it.
- Add or update tests when behavior changes.
- Keep commit messages short and imperative ("Add PDF bookmarks", not "Added bookmarks").
- Pull requests are squash-merged; the branch is deleted after merge.
- User-visible changes get a line under `## Unreleased` in `CHANGELOG.md`.
- Never commit keys, signing files, tokens, private server URLs or personal data.

## Automation you will see

- **CI** builds and tests every pull request.
- **CodeQL** scans the code and the workflows; **OpenSSF Scorecard** checks the repository setup weekly.
- **Dependabot** opens grouped dependency and GitHub Actions updates every week.
- **Copilot code review** comments on pull requests to the default branch. Treat it as a second reader;
  a maintainer still reviews.
