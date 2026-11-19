# Security policy

This policy covers every orgista repository that does not have its own `SECURITY.md`.

## Reporting a vulnerability

Please **do not open a public issue**. Use **Report a vulnerability** on the affected repository's
Security tab (`https://github.com/orgista/<repo>/security/advisories/new`; private vulnerability reporting
is on for every public repository), or email **support@orgista.com**. See GitHub's guide to
[privately reporting a vulnerability](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability).

Include the app and version, the device and OS, steps to reproduce, and the impact. You should get a
reply within 7 days. Once a fix is released, the advisory is published with credit, unless you prefer
to stay anonymous.

## Supported versions

Only the latest release of each app receives fixes. Security fixes ship within 7 days of a confirmed
report; see [RELEASING.md](RELEASING.md).

## Verifying a download

Release files come with a `SHA256SUMS` list and a GitHub attestation:

```bash
shasum -a 256 -c SHA256SUMS --ignore-missing
gh attestation verify <file> --repo orgista/<repo>
```
