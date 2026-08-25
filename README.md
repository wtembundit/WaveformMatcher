# WaveformMatcher

macOS app that matches video clips to audio WAV files by comparing waveforms, then exports a ready-to-import FCPXML for Final Cut Pro.

## Features

- **Waveform matching** — compares audio fingerprints between video and WAV files to find sync points automatically
- **Timecode matching** — aligns clips using embedded timecode when available
- **Manual sync mode** — opens clips directly in Manual Sync without running waveform or timecode first
- **Experimental Detect Slate guide** — finds likely slate visible ranges, visual clap guides, and audio clap candidates; saves results in `.wmproj` and can apply them with `Use Detect Slate`
- **Manual sync points** — distinct video/audio In-point controls with optional Auto Lock, unlock-to-adjust, and Undo
- **Timeline Detail** — edit a matched pair on one waveform timeline with direct offset dragging, frame nudging, zoom/fit, undo, and per-clip resync
- **Metadata View** — spreadsheet-style metadata editing with rectangular selection, copy/paste, fill, auto-number, Find & Replace, custom columns, undo/redo, and synced preview
- **Smart metadata import** — import CSV, XLSX, and PDF production reports with mapping, row matching, review warnings, and local PDF/OCR processing
- **Metadata export** — export all, filtered, or selected metadata rows to CSV
- **Editorial metadata** — edit Scene, Take, Reel, Camera Name, Angle, Note, Good Take, Speed, Rec FPS, and compatible custom Final Cut Pro metadata
- **Metadata naming** — name exported clips from metadata fields with source-filename fallback
- **Sortable clip table** — sort source filenames, scene, speed, or status in either direction
- **Keyboard shortcuts window** — searchable command reference from the Help menu
- **Export modes**
  - **Sync Clips** — one `<sync-clip>` per matched pair
  - **Multicam** — one `<multicam>` per WAV file with all matching cameras as angles
- **Timeline-aware parsing** — supports Event XML, split timeline cuts, separate timeline clips, connected audio, and primary storyline audio
- **Metadata round-trip** — preserves imported metadata and applies table overrides to sync clips, multicam clips, original clips, and speed duplicates
- **Auto Speed** — one-click button calculates playback speed from recorded frame rate metadata (recFPS ÷ timelineFPS); supports compatible FCPXML/custom Rec FPS fields, including metadata written by Shot Notes X
- **Export Original Clips** — optionally export original (unsynced) clips in a separate FCP event alongside synced output
- **Export Video Speed Duplicate** — for speed-adjusted clips, exports an additional 1× copy named with the recorded FPS (e.g. "48FPS")
- **Frame-accurate multicam** — mc-angle source clips are snapped to the timeline frame grid, eliminating FCP "not on edit frame boundary" warnings
- **Export controls** — `Trim To Video Area` and `Spatial Conform (Fit / Fill)` for Sync Clip and Multicam workflows
- **Drag-and-drop FCPXML** — drag an FCPXML file directly onto the Import button to load it
- **Final Cut Pro Workflow Extension** — accept direct Event/Timeline drag and drop from Final Cut Pro, plus dropped `.fcpxml` / `.fcpxmld` files, and open them in WaveformMatcher
- **Send To Final Cut Pro** — reopen generated FCPXML results in Final Cut Pro from the app
- **Project files** — save and restore the full project state (clips, settings, match results) in a `.wmproj` file via File > New / Open / Save / Save As
- **Languages** — English and Thai
- **Update notifications** — checks for new versions on launch and alerts the user with a download link

## Requirements

- macOS 14.0+
- Final Cut Pro (to import the exported FCPXML)

## Installation Note

WaveformMatcher 1.4.6 and later is signed with a Developer ID certificate and notarized by Apple. Install it by opening the DMG and dragging the app to Applications.

## Documentation

- [Changelog](CHANGELOG.md)
- [User Manual (English source)](docs/UserManual.en.md)
- [คู่มือการใช้งาน (ภาษาไทย)](docs/UserManual.th.md)
- [User Manual PDF](UserManual.pdf)

## 1.4.6 Release Notes

WaveformMatcher 1.4.6 is a major workflow update that adds metadata preparation and detailed timeline review to the existing synchronization workflow.

- Introduces Metadata View with spreadsheet editing, custom columns, Good Take, Note, Rec FPS, Auto Speed, naming templates, Find & Replace, and synced preview
- Introduces CSV/XLSX/PDF metadata import and CSV export with mapping, matching, review, and local OCR fallback
- Introduces Timeline Detail with aligned waveforms, direct offset editing, frame nudging, zoom/fit, undo, and pair-scoped resync
- Applies current table metadata consistently to Sync Clip, Multicam, original-clip, and speed-duplicate FCPXML output
- Improves player, waveform, project, relink, table, shortcut, and FCPXML stability
- Ships as a Universal app signed with Developer ID and notarized by Apple

## Releases

This public repository hosts WaveformMatcher releases and documentation.

## Support

Report issues or request features from the [Issues page](https://github.com/wtembundit/WaveformMatcher/issues).

## Dependencies

- `ffprobe` — optional fallback for raw-file timecode reads when FCPXML/native data is insufficient
  The app can now install FFprobe on demand when a timecode workflow truly needs it.

## Acknowledgements

- [FFmpeg / ffprobe](https://ffmpeg.org) — audio and video processing; licensed under LGPL 2.1+
