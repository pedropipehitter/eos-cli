# eos

A small CLI for managing ETC Eos Family Software release downloads. Pulls the Mac `.dmg` or the Windows `.exe` (also what ETC consoles run) for any release tag, in one command.

I built this because I switch Eos versions between shows. One house runs v3.3.6 on a current console. The next is on v2.x because the booth Ion has not been touched since Windows XP. Clicking through release pages every time I set up a show laptop got old.

This is a personal tool, open-sourced in case the pattern is useful. The installer files live in a private repo (`pedropipehitter/eos-software`). Remote commands work for collaborators with read access to that repo. Without that access, the remote commands fail at the `gh` layer; the source is still useful as a reference for managing private release downloads.

## Install

```bash
brew tap pedropipehitter/eos
brew install eos
```

Requires `gh` authenticated against an account with read access to the release repo. Homebrew installs `gh` as a dependency. Run `gh auth login` once if you have not done so already.

## Usage

```
eos list                            list remote release tags
eos get [--pc|--mac] <version>      download the installer for that version
eos latest [--pc|--mac] [major]     download newest overall, or newest in a major line
eos installed                       list local downloads with sizes
eos rm <version>                    delete one local version
eos clean                           keep newest local version, delete the rest
```

Platform defaults to `--mac` (`Eos-vX.Y.Z-Mac.dmg`). Use `--pc` for the Windows installer (`Eos-vX.Y.Z-PC.exe`), which is also what ETC consoles run. Mac and PC files for the same version live in the same tag folder, so grabbing both is safe.

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

The private-repo caveat is load-bearing. Without read access to `pedropipehitter/eos-software`, `list`, `get`, and `latest` will fail. The local commands (`installed`, `rm`, `clean`) work regardless.

## License

MIT.
