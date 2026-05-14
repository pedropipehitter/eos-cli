# eos

A small CLI for managing ETC Eos Family Software release downloads on macOS. Pulls the Mac `.dmg` for any release tag from a GitHub releases repo. Built because I switch Eos versions between shows (v3.3.6 on new work, v2.x on legacy shows still locked to it) and wanted a one-liner instead of clicking through release pages.

This is a personal tool, open-sourced in case the pattern is useful. The actual `.dmg` files live in a private repo (`pedropipehitter/eos-software`), so the CLI is only functional for collaborators I've granted access to. Anyone else is welcome to read the source as a reference for similar private-release-management workflows.

## Install

```
brew tap pedropipehitter/eos
brew install eos
```

Requires `gh` authenticated against an account with access to the release repo. Homebrew installs `gh` as a dependency. Run `gh auth login` once if you haven't already.

## Usage

```
eos list                  list remote release tags
eos get <version>         download the Mac .dmg for that version
eos latest [major]        download newest overall, or newest in a major line
eos installed             list local downloads with sizes
eos rm <version>          delete one local version
eos clean                 keep newest local version, delete the rest
```

Version strings accept either `3.3.6` or `v3.3.6`. The asset pattern is `Eos-vX.Y.Z-Mac.dmg`.

## Examples

```
eos latest                # newest release overall
eos latest 2              # newest in the v2.x line, for shows still on v2
eos get 3.2.10            # specific version
eos clean                 # keep one copy, drop the rest
```

## Notes

Downloads land in `${EOS_HOME:-$HOME/.eos}/versions/<tag>/`.

The private-repo caveat is the load-bearing one. Without read access to `pedropipehitter/eos-software`, `list`, `get`, and `latest` will fail at the `gh` layer. The local commands (`installed`, `rm`, `clean`) work regardless.

## License

MIT.
