# Changelog

## 1.4.5

### Improved

- Clip table scrolling is significantly smoother by avoiding repeated filter/sort work during redraw and using lighter WAV match menus in rows
- Scene and Take columns now resize dynamically within sensible limits and truncate safely instead of overlapping adjacent columns
- Waveform rendering now preserves the full audio tail when downsampling, preventing length-dependent visual/audio drift in Manual Sync
- Project media relink now handles duplicate filenames more safely by preferring candidates with matching folder suffixes

### Fixed

- Saving a project now immediately updates the clean/dirty baseline so closing or quitting right after Save no longer asks to save again
- Video speed input accepts `0` while editing and rejects non-numeric characters consistently
- Generated FCPXML no longer contains a machine-specific default Final Cut Pro library path

### Testing

- Added the first XCTest target and regression coverage for FCPXML parsing/generation, project round-trip, legacy project defaults, relink edge cases, speed input/presets, and waveform downsampling

## 1.4.4

### Added

- Clip table columns can now be sorted by Filename, Scene, Speed, or Status in ascending or descending order
- Manual Sync now offers an Auto Lock toggle, plus `I` and `O` shortcuts for video and audio sync points

### Changed

- The clip table now displays and sorts by the source video filename by default, independent of renamed Final Cut Pro display names
- Sync points now use distinct In-point symbols and video/audio colors, separate from Slate and Final Cut Pro guide markers
- Auto-matched offsets no longer appear as editable sync points unless the user explicitly creates or applies a point pair
- Auto Lock is visually separated from Clear and other sync actions

### Fixed

- Closing a project window or quitting now consistently offers Save, Don't Save, and Cancel without leaving the app stuck waiting to terminate
- Cancelling or failing a project save now also cancels the pending close or quit operation

## 1.4.3

### Fixed

- Update checking now reads the latest release from the main `wtembundit/WaveformMatcher` repository after the legacy release repository was retired

### Changed

- This is a recommended update so future in-app update notifications continue to work
- Removed the optional third-party quarantine helper recommendation from the README, user manual, and release website

## 1.4.2

### Added

- Added `Use Detect Slate` in Manual Sync so saved slate visual/audio guides can be applied as sync marks before locking sync
- `.wmproj` files are now registered as WaveformMatcher project files and can be opened directly from Finder
- The video seek bar now shows the primary slate visible range and supports focused zoom/pan review
- Detect Slate progress now reports finer-grained scan status so users can see real progress during video/audio analysis

### Improved

- Detect Slate now saves the full guide result in `.wmproj`, including visible ranges, visual/audio guide times, and debug candidates
- Pressing `Detect Slate` again on a clip with an existing saved guide now jumps back to that guide instead of re-analyzing
- Detect Slate audio refinement is anchored to the matched project context and prioritizes useful production channels such as Boom/Mix when available
- Manual Sync restores saved slate ranges when switching between clips in the table
- The app and Workflow Extension now share version `1.4.2`

### Changed

- Detect Slate remains experimental and guide-only; `Use Detect Slate` places marks for review but users still confirm with `Lock Sync`
- Generated slate test reports and media previews are treated as local temp artifacts and are not part of release source

## 1.4.1

### Improved

- Export default naming now uses the imported Event or Timeline name automatically, with the correct `_Sync Clips` or `_Multicam` suffix
- Manual Sync remembers in-progress manual marks more reliably, even before `Lock Sync`, when switching clips or changing the selected WAV
- Manual Sync resizing feels smoother and less jumpy while dragging the divider between the table and viewer
- `Import FCPXML…` is now available from the File menu with `Cmd+I`
- The main app remembers its resized window state more reliably without forcing an oversized first layout

### Fixed

- Fixed a regression where choosing a different WAV in Manual Sync could refresh the video side and clear in-progress marker placement
- Fixed `Send To Final Cut Pro` so it targets Final Cut Pro directly instead of opening with whichever app Finder currently uses for `.fcpxml`
- Fixed English UI sessions that could still show outdated workflow wording in docs and release notes

### Changed

- Workflow Extension documentation now reflects direct Event/Timeline drag and drop from Final Cut Pro, in addition to dropped `.fcpxml` and `.fcpxmld` files

## 1.4

### Added

- Added a Final Cut Pro Workflow Extension shell for file-based handoff into WaveformMatcher
- The extension can hand off dropped `.fcpxml` and `.fcpxmld` files into the main app
- Added `Send To Final Cut Pro` so generated FCPXML can be reopened directly from the app

### Improved

- The main app now restores its last window size more reliably

### Known limitations

- Detect Slate remains experimental and can still miss or misidentify difficult visual frames and some speech-like audio peaks

## 1.3

### Improved

- WaveformMatcher now follows an FCPXML-first decision flow more clearly: waveform sync remains native/FCPXML-first, and timecode mode prefers FCPXML timing before native or raw-file fallback paths
- ffprobe is no longer bundled into the app by default and is treated as an optional raw-file timecode fallback
- Timecode mode can install FFprobe on demand when a workflow truly needs raw-file fallback metadata
- Manual Sync snapping is more precise: holding `Shift` while dragging can snap the playhead to nearby marker guides, sync guides, and existing manual marks
- Marker-guided Manual Sync is more streamlined: imported FCP markers appear automatically in the viewer and matching marker pairs can be applied directly without an extra enable toggle
- Sandbox support is enabled again using multiple media access roots and security-scoped bookmarks instead of a single media folder assumption
- Progress estimate text now respects the current UI language correctly

### Fixed

- Fixed English UI sessions that could still show Thai estimate-time strings
- Fixed timeline-aware marker parsing and sync state persistence for Manual Sync marker workflows
- Fixed snap targets in Manual Sync so existing orange/green manual marks are included alongside marker guides

### Changed

- ffprobe is no longer bundled into the app by default
- waveform sync remains native/FCPXML-first and does not depend on ffprobe
- timecode mode now offers one-click FFprobe installation only when raw-file fallback is likely needed

## 1.2.3

### Improved

- Timeline waveform matching now uses each cut's actual in/out range instead of always reading from the source clip start
- Timeline timecode matching now respects trimmed cut ranges for timeline segments
- Manual Sync reads FCP markers automatically and shows purple marker guides for marker-assisted sync review
- Matching marker pairs can now be applied directly from Manual Sync with `Use Marker Pair`
- Saved projects now preserve marker-based sync state and detected marker guide times
- Waveform viewer loading and navigation were refined further for large multi-channel WAV files

### Fixed

- Fixed Sync Clips export so custom output resolution is respected even when it differs from the source clip format
- Fixed Multicam export so retimed angles keep their speed changes inside multicam angles
- Fixed Multicam export so video-only sections are preserved instead of being trimmed away with audio gaps
- Fixed Multicam browser/playback timing so delayed audio does not appear to start from the beginning of the clip
- Fixed timeline marker parsing so later cuts no longer inherit incorrect marker positions

### Changed

- FCP marker guides now appear automatically in Manual Sync when marker data is available; no extra toggle is required
- Detect Slate remains experimental and is still intended as a review guide, not an automatic sync action

### Known limitations

- Detect Slate video guidance is usable but can still lock onto the wrong object in difficult frames
- Detect Slate audio guidance performs best when the clap creates a distinct transient and can still be fooled by short speech-like peaks near the mic
- ffprobe is now treated as a raw-file timecode fallback when FCPXML/native timing is insufficient

## 1.2.2

### Improved

- Manual Sync waveform viewer now shows clearer per-channel labels and starts with a wider default detail view
- Waveform interaction is smoother: click-to-seek, drag scrubbing, follow-playhead behavior, and scroll-based pan/zoom are more predictable
- Audio waveform loading is faster with an earlier preview pass before full detail is refined in the background
- Detect Slate audio guidance is more reliable on clips where the clap peak is clearly visible in the waveform
- Channel labels in the waveform viewer now prefer parsed clip sub-roles before falling back to iXML or generic channel numbering

### Fixed

- Fixed waveform viewer interaction regressions where click or drag could stop moving the playhead
- Fixed waveform follow behavior during playback and pause, especially while zoomed in
- Fixed audio frame-step scrubbing so left/right stepping no longer jumps or requires holding the key
- Fixed scroll gesture direction for waveform pan and zoom controls
- Fixed several Detect Slate regressions introduced during tuning passes and restored a more stable baseline for visual guidance

### Changed

- Detect Slate remains experimental and is still intended as a review guide, not an automatic sync action

### Known limitations

- Detect Slate video guidance is usable but can still lock onto the wrong object in difficult frames
- Detect Slate audio guidance performs best when the clap creates a distinct transient and can still be fooled by short speech-like peaks near the mic
- ffprobe is now treated as a raw-file timecode fallback when FCPXML/native timing is insufficient

## 1.2.1

### Added

- Manual Sync mode as a first-class sync method alongside Waveform and Timecode
- Experimental Detect Slate guide in Manual Sync
- Slate guide times are now saved in `.wmproj`
- `Trim To Video Area` export option
- `Spatial Conform` option with `Fit` / `Fill`
- `File > Export FCPXML…` menu command with `Cmd+E`
- Training and dataset helper scripts for future Slate Detect work

### Improved

- Timeline parser now supports more real-world timeline structures, including split cuts, separate source clips, connected audio, and primary storyline audio
- Manual Sync playback respects timeline cut ranges for video
- Timeline export naming is cleaner for split cuts vs separate source clips
- Sync Clip and Multicam export behavior is more consistent for trimmed and untrimmed timeline cases
- Project save/load now restores more timeline-specific state correctly

### Changed

- App Sandbox flow was removed for the current distribution workflow
- Detect Slate is now explicitly treated as an experimental guide, not an automatic sync action

### Fixed

- Restored correct event-based viewer playback after timeline cut support was added
- Fixed stale slate-guide times when changing or clearing WAV assignment
- Fixed several timeline export edge cases that caused duplicate or malformed unsynced output

### Known limitations

- Detect Slate audio guidance still needs additional tuning
- RT-DETR model inference is optional and only runs when compatible weights are available locally or bundled
