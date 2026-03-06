# Copilot Instructions

## Repository Purpose

This is a personal [Homebrew Bundle](https://github.com/Homebrew/homebrew-bundle) Brewfile repository, used with [Strap](https://github.com/MikeMcQuaid/strap) to bootstrap a macOS development environment on first run.

## Brewfile Structure

The single `Brewfile` is ordered as follows:
1. **`tap`** – third-party Homebrew tap registrations (27 taps, including private `hashicorp/internal` and `hashicorp/security` taps requiring SSH access)
2. **`brew`** – CLI formulae (~227 entries)
3. **`cask`** – macOS GUI applications (~49 entries, including entries scoped to a tap e.g. `cask "hashicorp/tap/hashicorp-boundary-desktop"`)
4. **`mas`** – Mac App Store apps (~9 entries)

## Key Conventions

- Each `brew` entry is preceded by an inline comment (from `brew bundle dump --describe`) describing the formula — preserve these comments when adding entries.
- Private taps use SSH URLs: `tap "org/name", "git@github.com:org/repo.git"` — do not convert to HTTPS.
- Casks sourced from a specific tap use the namespaced form: `cask "tap/formula"`.
- `brew "python@3.13", link: false` — the `link: false` option is intentional; do not remove it.
- `brew "ed", link: true` — the `link: true` option is intentional.

## Common Operations

```sh
# Install everything from the Brewfile
brew bundle install

# Check what's installed vs. what's in the Brewfile
brew bundle check

# Add currently installed packages back to the Brewfile (with descriptions)
brew bundle dump --describe --force

# Remove packages not listed in the Brewfile
brew bundle cleanup --force
```

## Adding New Entries

- Add `tap` entries at the top, alphabetically within the tap block.
- Add `brew` entries after taps, maintaining the description comment above each entry.
- Add `cask` entries after brews.
- Add `mas` entries last with the numeric App Store ID: `mas "App Name", id: 123456789`.
