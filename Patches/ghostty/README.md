# ghostty patches

Unified diffs applied to the pinned ghostty checkout by `build.rs` after it
clones `GHOSTTY_COMMIT`, in filename order. Same shape as the series
`termio-sh/libghostty-swift` carries, so a change can move between the two
without being rewritten.

Each patch is rebased onto the pinned commit, so bumping `GHOSTTY_COMMIT`
means re-basing the series. A patch that no longer applies is a hard build
error rather than a silent skip — upstream having fixed it is exactly the
signal to delete the file.

`GHOSTTY_SOURCE_DIR` bypasses this entirely: a local checkout is taken as-is,
patches included or not, because it is the escape hatch for testing a change
before it becomes a patch here.

## Series

- `0001-formatter-reset-style-before-blank-cells.patch` — the `Vt` formatter
  emitted a run of blank cells under whatever style the preceding run left
  active, so re-serialising a screen painted a background the screen never
  held. The blank-*row* path already reset the style for this exact reason;
  blank *cells* did not. Upstream report: https://github.com/ghostty-org/ghostty/issues (pending)
