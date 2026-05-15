---
summary: 'Release checklist for camsnap (GitHub release + Homebrew tap)'
---

# Releasing camsnap

Follow these steps for each release. Title GitHub releases as `camsnap <version>`.

## Checklist
- Update code version in `cmd/camsnap/main.go`.
- Update `CHANGELOG.md` with the new version section.
- Tag the release: `git tag -a v<version> -m "Release <version>"` and push tags after commits.
- GoReleaser builds release archives and `checksums.txt`; Homebrew uses `camsnap_<version>_darwin_arm64.tar.gz`.
- Confirm `update-homebrew-tap` finished, or dispatch `update-formula.yml` in `steipete/homebrew-tap` with `macos_artifact=camsnap_<version>_darwin_arm64.tar.gz`.
- Update tap README with the new version/date if needed.
- Commit and push changes in camsnap and the tap; push tags: `git push origin main --tags` then `git push` in `../homebrew-tap`.
- Create GitHub release for `v<version>`:
  - Title: `camsnap <version>`
  - Body: bullets from `CHANGELOG.md` for that version
  - Body: bullets from `CHANGELOG.md` for that version plus a note to use `checksums.txt`
- Verify Homebrew install (one-line tap+install): `brew update && brew reinstall steipete/tap/camsnap && camsnap --version`.
- Smoke-test CLI: `camsnap --help`, `camsnap discover --info` (should not crash), and a sample `snap` against a known camera if available.
