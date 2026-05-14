# eos

CLI for managing [ETC Eos Family Software](https://github.com/pedropipehitter/eos-software) release downloads on macOS. Pulls the Mac `.dmg` for any version, manages local copies, and keeps the install footprint small between shows.

## Install

```sh
brew tap pedropipehitter/eos
brew install eos
```

Requires `gh` authenticated to a GitHub account with access to the `eos-software` releases repo (brew installs `gh` as a dependency, but you'll still need to run `gh auth login` once).

## Usage

```
eos list                  list remote release tags
eos get <version>         download the Mac .dmg for that version
eos latest [major]        download newest overall, or newest in a major line
eos installed             list local downloads with sizes
eos rm <version>          delete one local version
eos clean                 keep newest local version, delete the rest
```

Versions can be given as `3.3.6` or `v3.3.6`.

Downloads live in `${EOS_HOME:-$HOME/.eos}/versions/<tag>/`.

## Examples

```sh
eos latest          # newest release overall
eos latest 2        # newest v2.x release
eos get 3.2.10      # specific version
eos installed       # what's on disk
eos clean           # keep only the newest local copy
```

## License

MIT
