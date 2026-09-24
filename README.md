# Switchyard

Run several Claude Code accounts on one Linux or WSL machine, each with
its own sign-in, settings and sessions, and start the right one by
folder.

## Why

- No more signing out and in again to change accounts.
- Sessions and settings of one account never mix with another's.
- Usage stays with the account it belongs to.
- A web page and a terminal: use whichever you like.

## What it does

- Profiles: one per Claude account, each in its own private folder.
- Folder rules: "everything in ~/company uses Work".
- The shell hook: keep typing `claude`; Switchyard starts it with the
  profile for the folder you are in and shows which one.
- Sign in through the browser, or with a token from `claude setup-token`.
- Bring in your existing `~/.claude` settings and sessions.
- Copy sessions from one profile to another.
- Clean up old sessions, with a backup kept first.
- Health checks (`switchyard doctor`).
- A web page that only your own computer can reach (127.0.0.1).
- Signed updates, checked only if you turn them on.

## Install

One line, in a normal terminal (not as root):

```
curl -fsSL https://github.com/addico786/switchyard-releases/releases/latest/download/install.sh | bash
```

Or read the script before you run it:

```
curl -fsSLO https://github.com/addico786/switchyard-releases/releases/latest/download/install.sh
less install.sh
bash install.sh
```

It installs one file, `~/.local/bin/switchyard`. It never needs root,
never edits your shell startup files, and runs nothing it downloaded
before the checks pass: the sha256 checksum always, and the signature
when `minisign` is installed (`sudo apt install minisign`). To install
one exact version: `VERSION=0.2.0 bash install.sh`.

The minisign public key (the same key is inside `install.sh` and inside
the `switchyard` program):

```
REPLACE_WITH_THE_KEY_FROM_MINISIGN_PUB
```

Then run `switchyard setup` for a short walk-through.

## Update

```
switchyard update              # asks, then installs the newest version
switchyard update --check      # only says whether there is a newer one
switchyard update --rollback   # goes back to the version you had before
```

Every update checks the signature and the checksum first. A daily
check is off unless you turn it on: `switchyard update --setting ask`
(tell me) or `--setting auto` (install for me).

## Uninstall

```
switchyard hook uninstall                                  # removes the one line from ~/.bashrc or ~/.zshrc
rm -f ~/.local/bin/switchyard ~/.local/bin/switchyard.previous
rm -rf ~/.switchyard
```

The last line deletes every profile's sign-in, saved token, sessions,
settings and backups. Skip it to keep them. Your normal `~/.claude` is
never touched.

## Requirements

- Linux x64 or arm64 with glibc. Windows through WSL2 (Ubuntu) is
  tested.
- Claude Code installed (`claude` on your `PATH`), and bash or zsh for
  the hook.
- macOS and Windows without WSL are not supported.

## What this repository is

This repository holds only the releases: the two programs, `install.sh`,
the checksum list `SHASUMS256.txt`, its signature and the release notes.
The source code is kept private. Each program contains Switchyard's
bundled code, as any downloaded program does. The signature and the
checksums protect your download: they prove the file is the one the
owner signed.

## Privacy

Nothing leaves your computer, except the optional daily version check
to github.com, which sends only the version number.

## Security

Please report a security problem privately: on this repository, open
the Security tab and click "Report a vulnerability"
(https://github.com/addico786/switchyard-releases/security). Do not
open a public issue. See [SECURITY.md](SECURITY.md).

## License

MIT License, Copyright (c) 2026 addico786.
