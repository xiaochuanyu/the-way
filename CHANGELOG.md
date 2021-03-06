# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.9.0] - 2020-10-08
### Added
* `the-way cmd` allows adding shell snippets without asking for the language. 
Also, it takes the code as an argument so can be used in a shell function to automatically add the last used command for instance.
* shell snippets can have user-controlled variables inside using `<param>` and `<param=value>`. 
These are queried interactively from the user whenever the snippet is selected (with `search` or `cp`)
* old snippet information is now editable in `the-way edit` (arrow key navigation still doesn't work, waiting on the next dialoguer release)

## [0.8.0] - 2020-10-06
### Added
* Filter using a regex pattern with `-p` or `--pattern` ([PR #68](https://github.com/out-of-cheese-error/the-way/pull/68))
* Can install `the-way` with brew.

### Changed
* Updated dependencies

## [0.7.0] - 2020-09-03
**BREAKING RELEASE - needs a database migration**
* Before upgrade 
```bash
the-way export > snippets.json
the-way clear
```
* After upgrade
```bash
the-way import snippets.json
```
### Changed
* Switched from `reqwest` to `ureq`
* Updated dependencies


## [0.6.1] - 2020-07-23
Sort snippets numerically in `list` and `search`
Fixes [Issue #65](https://github.com/out-of-cheese-error/the-way/issues/65)

## [0.6.0] - 2020-07-15
**BREAKING RELEASE - needs a database migration**
* Before upgrade 
```bash
the-way export > snippets.json
the-way clear
```
* After upgrade
```bash
the-way import snippets.json
```
### Added
`the-way themes language <language.sublime-syntax>` - Add support for syntax highlighting non-default languages ([Issue #63](https://github.com/out-of-cheese-error/the-way/issues/63))
### Changed
* Removed `color_spantrace` dependency
* Bumped `sled` to v0.33.0

## [0.5.0] - 2020-07-14
**BREAKING RELEASE - needs a database migration:**
* Before upgrade 
```bash
the-way export > snippets.json
the-way clear
```
* After upgrade
```bash
the-way import snippets.json
```
### Added
**Sync to Gist functionality!** [Issue #60](https://github.com/out-of-cheese-error/the-way/issues/60)
### Fixed
* `export filename` and `config default filename` work without needing a `>` or an existing file
### Changed
* bumped all dependency versions to latest
* aliased `cp` to `copy`, `del` to `delete` and `config` to `configure`

## [0.4.0] - 2020-07-04
### Fixed
[Issue #58](https://github.com/out-of-cheese-error/the-way/issues/58) - changed search highlight and tag colors
### Changed
Bumped `eyre` and `color_eyre` versions. Holding off on bumping `sled` since it would need a database migration.

## [0.3.2] - 2020-06-03
### Fixed
[Issue #56](https://github.com/out-of-cheese-error/the-way/issues/56)

## [0.3.1] - 2020-05-26
### Changed
* Code highlighter defaults to .txt if syntax not found. This is a workaround b/c `syntect` uses some kind of default syntax set which is a subset of 
the GitHub syntax set. Need to figure this out though, Kotlin isn't highlighted!
* Switched to [`directories-next`](https://github.com/xdg-rs/dirs).

## [0.3.0] - 2020-05-14
I hope I'm following semver correctly, this is a minor version update and not a patch update because the CLI input prompt style changed
Also, no one should be using 0.2.4 b/c of the database bug.

### Added
Documentation for adding syntax highlighting themes to the README (Issue [#47](https://github.com/out-of-cheese-error/the-way/issues/47))

### Changed
Updated [dialoguer](https://github.com/mitsuhiko/dialoguer) to 0.6.2.
This makes `new` and `edit` look much nicer. Destructive commands (`clear` and `del`) now use dialoguer's Confirm prompt.

### Fixed
The code preview for `search` shows the correct number of lines now in the top right corner, previously it showed 3 extra because of newlines.
This fixes Issue [#46](https://github.com/out-of-cheese-error/the-way/issues/46)

## [0.2.5] - 2020-05-13
### Fixed
Fixed a pretty terrible bug - this is why tests matter. Snippet index is incremented after adding a snippet, also this is tested now 
(like it already should've been). Fixes Issue [#43](https://github.com/out-of-cheese-error/the-way/issues/43)

## [0.2.4] - 2020-05-13
### Fixed
"Failed to open configuration file" error when running `the-way config default` - the config command now runs without having a valid 
config file location (i.e. one that has read and write permissions) since you can use the command to make a valid file. 
Any other command that needs a valid config file and can't load it now throws a more helpful error telling you how to fix it.
Fixes Issue [#41](https://github.com/out-of-cheese-error/the-way/issues/41)

## [0.2.3] - 2020-05-08
### Added
Colorful errors with suggestions, courtesy of [color_eyre](https://github.com/yaahc/color-eyre)

### Fixed 
A bug in the change_snippet test that made its own release directory causing clashes between targets in Travis.
This uses the correct release directory now based on the TARGET environment variable.


## [0.2.2] - 2020-05-06
### Removed
- clipboard dependency:
Instead, I'm using xclip and pbcopy respectively on Linux and OSX. This fixes Travis 
compilation issues on Linux and the weird issue that clipboard is cleared 
when the-way exits in Linux, which would've been pretty sad.
clipboard is still a dev-dependency for MacOS, to test that copying works.
The copy test is not run for Linux.
- onig_sys dependency:
This was also causing issues on Linux, so now I'm using the 
[fancy_regex feature flag for syntect](https://github.com/trishume/syntect#pure-rust-fancy-regex-mode-without-onig) instead.

### Added
- Linux binaries
- Tests to Linux compilation with Travis
- A changelog:
I'll make sure to add changes to it from now, the previous two releases weren't perfectly documented.

### Changed
- The CLI:
    - copy -> cp
    - delete -> del
    - show -> view
    - change -> edit
    - themes current -> themes get
    - themes -> themes list

## [0.2.1] - 2020-05-02
### Added
- OSX binary
- Better demo
- Added Travis CI (only for OSX)


## 0.2.0 - 2020-05-02
### Added
- A first working version of the-way
- cargo install option
    
[0.9.0]: https://github.com/out-of-cheese-error/the-way/compare/v0.8.0...v0.9.0
[0.8.0]: https://github.com/out-of-cheese-error/the-way/compare/v0.7.0...v0.8.0
[0.7.0]: https://github.com/out-of-cheese-error/the-way/compare/v0.6.1...v0.7.0
[0.6.1]: https://github.com/out-of-cheese-error/the-way/compare/v0.6.0...v0.6.1
[0.6.0]: https://github.com/out-of-cheese-error/the-way/compare/v0.5.0...v0.6.0
[0.5.0]: https://github.com/out-of-cheese-error/the-way/compare/v0.4.0...v0.5.0
[0.4.0]: https://github.com/out-of-cheese-error/the-way/compare/v0.3.2...v0.4.0
[0.3.2]: https://github.com/out-of-cheese-error/the-way/compare/v0.3.1...v0.3.2
[0.3.1]: https://github.com/out-of-cheese-error/the-way/compare/v0.3.0...v0.3.1
[0.3.0]: https://github.com/out-of-cheese-error/the-way/compare/v0.2.5...v0.3.0
[0.2.5]: https://github.com/out-of-cheese-error/the-way/compare/v0.2.4...v0.2.5
[0.2.4]: https://github.com/out-of-cheese-error/the-way/compare/v0.2.3...v0.2.4
[0.2.3]: https://github.com/out-of-cheese-error/the-way/compare/v0.2.2...v0.2.3
[0.2.2]: https://github.com/out-of-cheese-error/the-way/releases/tag/v0.2.2
[0.2.1]: https://github.com/out-of-cheese-error/the-way/releases/tag/v0.2.1-osx
