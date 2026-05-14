# eos

A small CLI for managing ETC Eos Family Software release downloads. Pulls the Mac `.dmg` or the Windows `.exe` (also the installer for ETC consoles, which run Windows) for any release tag from a GitHub releases repo. Built because I switch Eos versions between shows (v3.3.6 on new work, v2.x on legacy shows still locked to it) and wanted a one-liner instead of clicking through release pages.

This is a personal tool, open-sourced in case the pattern is useful. The actual `.dmg` files live in a private repo (`pedropipehitter/eos-software`), so the CLI is only functional for collaborators I've granted access to. Anyone else is welcome to read the source as a reference for similar private-release-management workflows.

## Install

```
brew tap pedropipehitter/eos
brew install eos
```

Requires `gh` authenticated against an account with access to the release repo. Homebrew installs `gh` as a dependency. Run `gh auth login` once if you haven't already.

## Usage

```
eos list                            list remote release tags
eos get [--pc|--mac] <version>      download the installer for that version
eos latest [--pc|--mac] [major]     download newest overall, or newest in a major line
eos installed                       list local downloads with sizes
eos rm <version>                    delete one local version
eos clean                           keep newest local version, delete the rest
```

Platform defaults to `--mac` (`Eos-vX.Y.Z-Mac.dmg`). Use `--pc` for the Windows installer (`Eos-vX.Y.Z-PC.exe`), which is also what ETC consoles run. Mac and PC files for the same version coexist in the same tag folder, so you can grab both without conflict.

Version strings accept either `3.3.6` or `v3.3.6`.

## Examples

```
eos latest                # newest release overall (Mac)
eos latest 2              # newest in the v2.x line, for shows still on v2
eos get 3.2.10            # specific version (Mac)
eos get --pc 3.3.6        # Windows installer, also for ETC consoles
eos latest --pc 2         # newest v2.x PC build
eos clean                 # keep one version folder, drop the rest
```

## Notes

Downloads land in `${EOS_HOME:-$HOME/.eos}/versions/<tag>/`.

The private-repo caveat is the load-bearing one. Without read access to `pedropipehitter/eos-software`, `list`, `get`, and `latest` will fail at the `gh` layer. The local commands (`installed`, `rm`, `clean`) work regardless.

## License

MIT.
