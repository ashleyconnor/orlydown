# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.2.0] - 2026-10-16

### Added

- Requests that fail with a 403, 429 or 5xx error, or because of a network
  problem, are retried up to 4 times with increasing waits, honouring the
  server's `Retry-After` header.
  ([#9](https://github.com/ashleyconnor/orlydown/issues/9))

### Changed

- At most 8 files are downloaded at the same time.
  ([#9](https://github.com/ashleyconnor/orlydown/issues/9))
- `--delay` is documented as the wait between pages of the file list, which
  is what it has always done.
  ([#9](https://github.com/ashleyconnor/orlydown/issues/9))
- Repeated spaces in titles are collapsed when naming the file with
  `--title`, so a re-downloaded book may get a slightly different filename.

### Fixed

- A failed download no longer leaves an incomplete epub under the final
  filename. The book is written to a `.partial` file and only renamed once
  every file has downloaded; on failure the partial file is removed and an
  existing epub of the same name is left alone.
  ([#8](https://github.com/ashleyconnor/orlydown/issues/8))
- `--title` produces filenames that are valid on Windows, macOS and Linux:
  `\` becomes `-`, `"` becomes `'`, `<>|?*` and control characters are
  removed, trailing dots and spaces are trimmed, reserved device names such
  as `CON` get a `_` suffix, and long titles are shortened.
  ([#10](https://github.com/ashleyconnor/orlydown/issues/10))

## [0.1.1] - 2026-10-14

### Fixed

- Images show in books whose chapters use the `.htm` extension (e.g.
  *Elixir in Action, Third Edition*). Chapters are now picked out by the
  media type the API reports instead of their file extension.

### Changed

- The package lists each supported Python version (3.9 to 3.14), so PyPI
  shows them.

## [0.1.0] - 2026-10-11

First release as `orlydown`, a fork of
[xi/oreilly-downloader](https://github.com/xi/oreilly-downloader).

### Added

- Installable from PyPI with pipx or uv, providing an `orlydown` command.
- `--title` names the epub after the book title instead of its ID.
- `--require-auth` exits with an error instead of downloading truncated
  chapters when no JWT is given or it is rejected.
- Help text for the book ID and `--jwt`.

### Changed

- No dependencies: downloads use `urllib` and HTML is parsed with the
  standard library instead of aiohttp and lxml.

### Fixed

- Stylesheets are linked from every chapter, so books keep their formatting
  and fonts.
- Images and links work in books that keep chapters in a subdirectory
  (e.g. `Text/`, `Images/`).
- Books whose package file isn't called `content.opf` (e.g. Springer titles)
  open correctly.
- SVG covers are scaled to fit the page instead of being cropped.

[Unreleased]: https://github.com/ashleyconnor/orlydown/compare/v0.2.0...HEAD
[0.2.0]: https://github.com/ashleyconnor/orlydown/compare/v0.1.1...v0.2.0
[0.1.1]: https://github.com/ashleyconnor/orlydown/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/ashleyconnor/orlydown/releases/tag/v0.1.0
