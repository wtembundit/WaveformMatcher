# WaveformMatcher

macOS app that matches video clips to audio WAV files by comparing waveforms, then exports a ready-to-import FCPXML for Final Cut Pro.

## Features

- **Waveform matching** — compares audio fingerprints between video and WAV files to find sync points automatically
- **Timecode matching** — aligns clips using embedded timecode when available
- **Open Media Files** — sync video and audio files or folders directly without an FCPXML; WAV timecode and iXML metadata are read natively
- **Manual sync mode** — opens clips directly in Manual Sync without running waveform or timecode first
- **Detect Slate** — a built-in clapperboard detector finds the slate in picture, the frame where the sticks close, and the clap in the WAV (also before sync); saves results in `.wmproj` and can apply them with `Use Detect Slate`
- **Manual sync points** — distinct video/audio In-point controls with optional Auto Lock, unlock-to-adjust, and Undo
- **Timeline Detail** — edit a matched pair on one waveform timeline with direct offset dragging, frame nudging, zoom/fit, undo, and per-clip resync
- **Metadata View** — spreadsheet-style metadata editing with rectangular selection, copy/paste, fill, auto-number, Find & Replace, custom columns, undo/redo, and synced preview
- **Smart metadata import** — import CSV, XLSX, and PDF production reports with mapping, row matching, review warnings, and local PDF/OCR processing
- **Metadata export** — export all, filtered, or selected metadata rows to CSV
- **Editorial metadata** — edit Scene, Take, Reel, Camera Name, Angle, Note, Good Take, Speed, Rec FPS, and compatible custom Final Cut Pro metadata
- **Metadata naming** — name exported clips from metadata fields with source-filename fallback
- **Sortable clip table** — sort source filenames, scene, speed, or status in either direction
- **Video Output** — full-screen picture on a second display (Command P)
- **Scene grouping** — export scene keywords and/or one smart collection per scene
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

## 1.5.2 Release Notes

WaveformMatcher 1.5.2 fixes the Final Cut Pro workflow extension, which stayed on "Loading..." on other Macs: macOS refused to load Final Cut Pro's own framework into it. The extension appears in Final Cut Pro (Window → Extensions) once WaveformMatcher is in the Applications folder and has been opened once.

## 1.5.1 Release Notes

WaveformMatcher 1.5.1 makes Detect Slate easier to use: it opens on the frame where the slate is sharpest, its result becomes a yellow Use Detect Slate button, and clips with Final Cut Pro marker pairs get a Use Markers button. Detect Slate no longer seems stuck at 53 % on the first clip. Mute Mix also applies to WAVs whose channels were muted by hand, the Sync View table gets column lines and aligned headers, Space plays after a sync instead of typing into the search field, skimming keeps the playhead in place, and Timeline Detail no longer goes missing after working in Metadata View.

## 1.5.0 Release Notes

WaveformMatcher 1.5.0 adds Video Output on a second display (Command P) with a choice of display, a customizable burn-in overlay of timecode, filenames, metadata and status, and a transport bar in Metadata View. Channels muted on the waveform are now muted in the export too (Option-click hears one channel), with a listening-volume fader per channel. Keyboard shortcuts can be customized, Timeline Detail and the waveform can be skimmed, the export can group clips by Scene with keywords and/or smart collections, and File → Open Recent lists recent projects. Multicam angles that start after the first camera now play in sync in Final Cut Pro's browser and viewer, and two camera angles no longer land a frame apart.

## 1.4.9 Release Notes

WaveformMatcher 1.4.9 turns the Metadata View synced preview into a floating mini player window, like Picture in Picture, so cells can be edited while it plays; it moves and resizes freely and takes Space, J/K/L and frame-step keys, with Esc to close. The mini player opens each clip on its clap or sync point, shows source timecode, plays full screen and zooms. The start screen adds Open Project. It also fixes the Metadata Naming separator and Find & Replace buttons running past their windows' edges.

## 1.4.8 Release Notes

WaveformMatcher 1.4.8 adds Open Media Files to sync video and audio folders without an FCPXML, with native WAV timecode and iXML metadata. Detect Slate is no longer experimental: built-in models find the slate, the frame where the sticks close on digital and handwritten slates, and the WAV clap, even before a clip is synced, including small slates in wide shots. Synced clips open on the slate, and an optional Detect Slate after sync runs in the background. Command +, Command − and Command 0 zoom whatever the pointer is over, including the video viewer for checking a distant slate. It also adds a status bar with keyboard hints, resizable Sync View columns, a redesigned Metadata Naming editor, source timecode in the transport, background PDF import, in-app updates for future releases, and fixes for lag on clip changes, playback after jumps, and timeline zoom.

## 1.4.7 Release Notes

WaveformMatcher 1.4.7 fixes renamed Final Cut Pro audio metadata import and expands clip naming across Sync View, Metadata View, and FCPXML export. It adds Video/Audio Filename choices, editable Clip Name values, reorderable metadata tokens with custom prefixes and separators, Audio Match naming that follows the selected source, Project FPS wording, compact sidebar menus, collapsible waveform settings, and a confirmation before a full sync rerun replaces current work.

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

[Download the latest version](https://wtembundit.github.io/WaveformMatcher/?manual=1)

## Support

Report issues or request features from the [Issues page](https://github.com/wtembundit/WaveformMatcher/issues).

## Dependencies

- `ffprobe` — optional fallback for raw-file timecode reads when FCPXML/native data is insufficient
  The app can now install FFprobe on demand when a timecode workflow truly needs it.

## Acknowledgements

- [FFmpeg / ffprobe](https://ffmpeg.org) — audio and video processing; licensed under LGPL 2.1+
