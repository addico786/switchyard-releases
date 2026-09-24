# Security

## Reporting a problem

Report a security problem privately through this repository's private
vulnerability reporting: open the Security tab and click "Report a
vulnerability"
(https://github.com/addico786/switchyard-releases/security/advisories/new).
Please do not open a public issue.

Say which version you use (`switchyard --version`), what you did and
what happened. Never include a token or a credential file; the output
of `switchyard doctor` is safe to share.

## Supported versions

Only the latest release gets security fixes.

## Checking a download by hand

Each release has `SHASUMS256.txt` and its minisign signature
`SHASUMS256.txt.minisig`. With the public key from the README:

```
minisign -Vm SHASUMS256.txt -P <public key>
sha256sum -c --ignore-missing SHASUMS256.txt
```
