# Changelog

## 1.5.3

### Added

- Safety Crop export option for cameras shot wide to stabilize or track: the camera clip inside each sync clip and multicam angle is scaled up by the chosen percentage (10 % → 110 %) while the sync or multicam clip stays at 100 %. Saved with the project
- Wrap Clips Without Sync export option: clips with no audio become sync clips, in Multicam export too, taking the project's frame size, Spatial Conform and Safety Crop like synced clips (useful for clips shot in another aspect ratio, and for high-speed clips to retime and stabilize). Saved with the project

### Fixed

- Clips without sync were exported without the Spatial Conform (Fit / Fill) chosen for the synced clips

## 1.5.2

### Fixed

- The Final Cut Pro workflow extension stayed on "Loading..." on other Macs: macOS refused to load Final Cut Pro's own framework into it. It now opens

## 1.5.1

### Changed

- Sync actions are buttons instead of the ◎ menu: once a slate is found, Detect Slate becomes a yellow Use Detect Slate button (↻ scans again; its ▾ lists WAV clap candidates on unsynced clips), then Slate in Use. Clips with Final Cut Pro marker pairs get a MARKER row with a purple Use Markers button (› for the next pair). Rows appear only when there is something to use
- Detect Slate shows the slate where it reads best: the viewer opens on the frame where the board is sharpest, while the yellow guide and Use Detect Slate stay on the clap (often blurred by the moving sticks or a focus pull)

### Fixed

- Mute Mix now also changes WAVs whose channels were muted or unmuted by hand: their Mix channels follow the switch, their other channels keep their state
- Sync View table: column lines run down the rows, text keeps a small gap from them, and headers line up with their cells (they sat a few points to the right). Each column is resized from its left edge, so the divider follows the pointer
- Space in the empty search field plays instead of typing a space (the field could hold focus unnoticed after a sync, and the list then filtered to nothing). Space while skimming plays picture and sound from the skimmed point; while skimming, the playhead stays where it was until a click
- Back in Sync View after working in Metadata View, Timeline Detail could be missing until a clip was clicked: it stayed on the clip selected before. It now follows the selected clip
- Detect Slate could sit at 53 % for about 30 seconds on the first clip: macOS loads its text recognition the first time after a while. It is now loaded in the background at launch, with the slate models. A frame request that stops answering ends after 10 seconds, and a result from Detect Slate after sync also ends the count

## 1.5.0

### Added

- Video Output on a second display: View → Turn Video Output On (Command P) or the display button in the toolbar shows the picture over the whole of another display, menu bar included, while you keep working. Choose the display under View → Output Display (remembered). It turns off if the display is disconnected
- With Video Output on in Metadata View, a transport bar above the status bar plays the active row on the output display (Space, J/K/L, comma and period for frames; the arrows keep moving between cells). The mini player still opens from the bar and takes over the output while it is open
- Output overlay burned into the picture (View → Output Overlay…): source and audio timecode, video and audio filenames, Scene, Take, Reel, Camera Name, Angle, Note, sync status, speed, Rec FPS and custom text, each in one of six places with an optional label, in any order; text size, color, background and margin adjustable with a live preview
- Customizable keyboard shortcuts: Help → Keyboard Shortcuts… lists every command; click its key and press a new one (Esc cancels), with a warning when the key is already used and Reset / Reset All. Commands that had no key (Detect Slate, Use Detect Slate, Lock Sync, Auto Lock, Timeline Detail, Send to Final Cut Pro, output overlay and its settings, Open Mini Player) can now be given one. Built-in keys keep working unless another command takes them
- Skimming in Timeline Detail: while paused, the picture follows the pointer with a pink skimmer line (S) and short sound snippets play as it moves (Shift S); leaving goes back to the playhead. Audio skimming also plays the Sync View waveform under the pointer. View → Skimming and Audio Skimming switch them (S and Shift S show in the menu like other keys; typing in a text field still types the letter)
- Channel mute on the waveform, linked to the export: a speaker beside each WAV channel's name mutes it in the app and turns its role off in Final Cut Pro (sync clip or multicam). Option-click hears only that channel; Option-click it again hears all. Mix channels start muted when the export's Mute Mix is on. Mutes are saved with the project
- Listening volume per WAV channel (−24 to +12 dB): a vertical fader beside each channel's meter, with a reset button (or double-click; Shift-drag for fine steps). Listening only, not exported
- Mute and volume changes can be undone and redone
- Export option Scenes: tag each clip with a keyword for its Scene, add one smart collection per scene (exact Scene match), or both. Scene keyword collections go in a "Scene Keywords" folder and smart collections in a "Scene Smart Collections" folder
- Scenes → Group By: Whole Value, Scene Only, or Scene → Cut (a folder per scene with its cuts), for Scene values that hold scene and cut (S127AC1). Rule and Preview… sets where the cut starts (cut marker, separator or regular expression) and lists the groups the project would make; smart collections match exact values
- Sync clips and multicam clips carry a "Synced" keyword, the counterpart of "Not Synced"; both stay outside the scene folders
- Media opened directly (Open Media Files) gets a keyword with its folder name, the camera or sound roll, as Final Cut Pro adds when it imports media; FCPXML sources keep their own keywords

- File → Open Recent: the last 10 projects opened or saved

### Changed

- WAVs no video was synced with are now exported as audio clips with the "Not Synced" keyword, like unsynced videos, instead of being left out
- File → Print is gone (nothing to print); Command P is Video Output. The toolbar's full-screen button became the Video Output button; full screen on the same display stays on the viewer's button and Shift Command F
- Temporary monitor mixes are also cleared when the app quits
- Multichannel WAVs are ready to hear much sooner: the monitor mix is rendered with vector maths (about 30× faster) and at higher priority
- Scene Grouping's Rule and Preview shows the three choices side by side, with what a scene from the project becomes in each, and the Scene Keywords folder as Final Cut Pro will show it
- Projects that have a file (saved or opened once) save themselves every 20 seconds when something changed (File → Auto Save, on by default); the status bar shows when. Saves are written atomically
- Video Output remembers that it was on and on which display, and comes back at launch when that display is connected
- Metadata Naming fields can be reordered by dragging their handle, as well as with the arrows
- Dragging the audio of a locked pair in Timeline Detail shows "Sync is locked" with an Unlock button, instead of silently only moving the playhead

### Fixed

- Sync View: changing clip while playing could leave Video Output black and stopped until another clip was chosen
- Mute Mix did nothing for WAVs whose mix channel is named in capitals, such as MIX-L (common in recorders' iXML when media is opened directly); Mix channels are now found in any case, in the app and in the export
- A Rec FPS typed in the table (for example 72 for a 300 % clip) was not saved with the project: after reopening it showed the file's own rate (24) while the speed stayed right. It is saved now, and projects saved earlier get it back from their speed when it was set from Rec FPS
- Multicam: a camera that starts after the first one played out of sync in Final Cut Pro's browser and viewer (by the time it starts late), though it looked right in the angle editor. Its lead-in is now written as a gap, as the audio angle's has been since 1.2.3
- Multicam: two camera angles could land a frame apart. Each camera was rounded to the WAV on its own; the difference between cameras is now rounded once, and the audio angle keeps a sample-accurate start
- Media opened directly (Open Media Files): WAV channels were exported as the recorder's input numbers instead of their place in the file, so in Final Cut Pro some roles showed but played no sound (a recorder that skips inputs writes, for example, inputs 3, 4, 5 and 9 as channels 1 to 4). Projects saved earlier are repaired when opened. Audio from an FCPXML source was not affected
- Camera audio was always declared as 2 channels; a camera file with 3 channels lost its third
- Sync clips trimmed to the video started a few seconds late in timecode when the camera timecode was near 00:00:00:00 and the WAV started before it
- High-speed clips (speed above 100 %): Timeline Detail showed only part of the WAV; it now shows the sync clip as Final Cut Pro does, with the video at its retimed length and the full WAV at 100 %
- High-speed clips: the WAV kept playing after the video reached its end
- High-speed clips without sync points played the WAV out of step with the exported sync clip

## 1.4.9

### Added

- The start screen has Open Project… to continue a saved project (.wmproj)

### Changed

- The synced preview in Metadata View is now a floating mini player window, like Picture in Picture: move it anywhere (another screen too), resize it freely, and keep editing table cells while it plays. It stays on top, remembers its place and size, and follows the active row
- While the mini player is open: Space plays or pauses, J/K/L shuttle, Left/Right step a frame, Up/Down change row, Esc closes it (Space opens it, paused). Changing clip keeps playing or stays paused
- The mini player opens each clip on its clap or sync point, as Sync View does, shows the source timecode, plays full screen (button or Shift Command F), and zooms with Command + / Command − / Command 0, Option-scroll or pinch

### Fixed

- The separator buttons in the Metadata Naming window ran past the window's edge
- The start screen's Audio card cut its file types short
- Find & Replace buttons ran past the window's edge and were cut to "Replace…"; the replace buttons now sit on their own row

## 1.4.8

### Added

- Added Open Media Files: sync video and audio files or folders directly, without exporting an FCPXML first
- Video and Audio have separate source buttons, so camera and sound folders can be chosen independently
- WAV timecode is read natively from BWF `bext` and iXML, so Timecode mode no longer needs FFprobe for WAV files that lack an FCPXML start value
- iXML Scene, Take, Tape, Note, Circled and track names now fill Scene, Take, Reel, Note, Good Take and audio roles for directly opened audio
- Added a status bar at the bottom of the window with the current state and keyboard hints for the active view
- Sync View columns can be resized by dragging their headers; widths are remembered
- Check for Updates can now download and install new versions from inside the app (Sparkle), starting with the release after 1.4.8
- Command +, Command − and Command 0 zoom in, zoom out and fit whatever the pointer is over: video viewer, audio waveform, Timeline Detail, the Sync View table or the Metadata table (with the pointer elsewhere: the timeline in Sync View, the table in Metadata View). Plain + / − still zoom the table
- The video viewer zooms in to check small or distant slates: Command + / Command − and Command 0 with the pointer over the viewer, Option-scroll, or pinch; it zooms where the pointer is, scroll or drag moves the picture, and the zoom badge returns to fit. The synced preview in Metadata View zooms the same way
- Pinch zooms the waveforms, the video scrub bar and Timeline Detail; Timeline Detail also zooms with Option-scroll and pans with sideways scroll
- The audio waveform zooms where the pointer is: Command + / Command − and Command 0 with the pointer over it, Option-scroll, or pinch

### Changed

- Fit Timeline moved from Shift Z to Command 0, the same key that fits every other view
- Detect Slate is no longer experimental: a built-in clapperboard detector (Core ML, runs on the Mac) finds the slate in picture in about 2 s per clip. A WAV transient outside the slate is no longer taken as the clap, and still boards that sit in frame for the whole shot are ignored
- Detect Slate finds the clap where the clapper sticks close: digital slates by reading the timecode until it freezes, handwritten slates with a built-in open/closed stick detector; the WAV clap is then taken right at that frame
- Selecting a synced clip opens it on the slate: on the Detect Slate clap, or on a clap guessed from the WAV right after sync (the short, sharp sound of the sticks near the clip's start or end, in the background)
- Added Detect Slate after sync, a checkbox under the Start button (off by default) that runs Detect Slate on every synced clip in the background; the status bar shows background work and its progress, with a ✕ to stop it
- Temporary files (monitor mixes, FCPXML hand-offs) are cleared when a project closes and at launch
- Detect Slate also finds the WAV clap before a clip is synced: from the frozen timecode on digital slates, from the clip's timecode offset when available, otherwise from a built-in clap sound detector, with the top three candidates to choose from in the ◎ menu
- The inspector shows Detect Slate results as FIND and LOCK rows, and is more compact, with short fields side by side
- Detect Slate now sits in front of Auto Lock, with an icon and text
- Choosing the source moved from the sidebar to the start screen in the center of the window; the toolbar shows the loaded source
- The sidebar keeps a fixed width and shows the full naming template
- Redesigned the Metadata Naming editor with a live example name
- Scene, Take, Speed and Rec FPS can be edited directly in the Sync View table (double-click)
- PDF metadata import runs in the background with a progress panel, and each page is read with OCR only once
- The transport and the Timeline Detail ruler show the clip's source timecode, matching the sync clip in Final Cut Pro; time from the clip start stays beside it
- The Offset column shows a full timecode on one line
- Metadata View scrolls and edits faster with large projects

### Fixed

- Changing clips could freeze the app for several seconds
- Playback stopped after jumping to a sync point or scrubbing; it now continues
- Zooming the Timeline Detail drew the audio waveform out of step with the video
- After dragging in Timeline Detail, derived sync points still showed on the timeline
- Timeline Detail showed extra slate ranges before and after the real slate after Detect Slate
- Detect Slate marked a slate range on clips with no clapperboard (car windows, seats, set pieces); only the built-in slate detector is used now, and when it finds no slate in the full frame it looks again zoomed in, to find small slates in wide shots. Detect Slate results saved by earlier versions are cleared when a project opens, so Detect Slate scans again
- A closed project reappeared when opening a new source
- Speed and Rec FPS naming tokens were always empty; they now appear unless Speed is 100% or Rec FPS equals the timeline FPS
- Switching between Sync View and Metadata View now scrolls to the selected clip
- Quick Preview in Metadata View sometimes stayed stopped for clips with multichannel audio
- The Timeline Detail camera waveform loaded slowly for media on external drives
- Fixed QuickTime timecode reads that returned no timecode when the first timecode sample buffer was empty, and that used the timecode track's sample rate instead of the video frame rate

## 1.4.7

### Added

- Added Video Filename and Audio Filename clip-naming options; filename-based names omit the source extension
- Added an editable Clip Name column in Sync View and Metadata View that previews the exported name, follows the active naming option, and supports per-clip manual overrides
- Added metadata naming templates with reorderable tokens, optional text before each token, and underscore, hyphen, slash, hash, space, or no separator
- Added a confirmation before running any full sync mode again, with guidance to use pair-scoped Resync or Manual Sync when only one clip needs adjustment

### Changed

- Audio Match now displays the Final Cut Pro audio clip name by default and follows Audio Filename when that naming option is selected
- Renamed Timeline FPS to Project FPS throughout the current UI
- Updated Output Setup dropdowns to use the compact sidebar menu style
- Waveform matching thresholds now use tested defaults and stay collapsed under Adjust Matching Settings until needed
- Simplified Timecode and Manual mode guidance and standardized current UI wording on Audio

### Fixed

- Fixed Final Cut Pro audio browser clips losing their clip name, metadata, notes, ratings, roles, and markers when the browser name differed from the source filename
- Kept manual Clip Name values out of exported metadata fields while applying them consistently to Sync Clip and Multicam names

## 1.4.6

### Added

- Added Metadata View, an editable spreadsheet-style workspace for reviewing and preparing clip metadata before FCPXML export
- Added editable Scene, Take, Reel, Camera Name, Angle, Note, Good Take, Speed, and Rec FPS fields, plus detected and user-created custom metadata columns
- Added rectangular selection, multi-row copy/paste, fill down, drag fill, auto-number, clear/reset, undo/redo, resizable columns, table zoom, and scoped Find & Replace
- Added metadata source policies for Video, Audio, Video + Audio, and Audio + Video, with per-cell manual overrides preserved in `.wmproj`
- Added metadata-based clip naming with a `Scene_Take_Angle` template and fallback to the source video filename when metadata is incomplete or absent
- Added Metadata Import/Export. CSV supports scoped export and round-trip import; CSV, XLSX, and PDF reports use a shared mapping and review workflow
- Added Smart Import matching by filename, path, filename tokens, Reel + Clip, and report-specific clip ranges while skipping ambiguous rows instead of guessing
- Added PDF table reconstruction and local Apple Vision OCR fallback for difficult reports, including Thai-text review warnings
- Added Reel helpers for embedded reel, source filename, folder name, and a custom value applied to the active selection
- Added an in-app synced metadata preview with aligned production audio, multichannel stereo monitoring, marker/slate guides, and keyboard navigation
- Added Timeline Detail to Sync View with camera/audio waveforms on one time ruler, direct Audio Match dragging, frame nudging, zoom/pan/fit, offset reset, and undo/redo
- Added pair-scoped Resync with Waveform or Timecode for the active Timeline Detail clip without searching unrelated project audio
- Added a distinct orange Manual status for user-adjusted or manually locked sync results

### Changed

- Reorganized the working flow around Sync View, Metadata View, Output Setup, and FCPXML export
- Auto Speed now works with editable Rec FPS, distinguishes automatic and manual values visually, and preserves explicit per-clip speed overrides
- Notes export as Final Cut Pro notes, Good Take exports as a Favorite rating, and metadata edits now flow consistently to sync clips, multicam clips, unsynced clips, and speed duplicates
- The clip table now uses `Audio Match` / `No Audio` terminology consistently
- Auto Lock is enabled by default again and remains available as an explicit per-user toggle
- Removed the ambiguous clear icon beside Lock Sync

### Fixed

- Restored the lightweight update download gateway so existing in-app update prompts resolve the latest notarized DMG instead of opening a removed website
- Improved metadata table focus, rectangular selection, keyboard navigation, Thai-layout shortcuts, column resizing, scroll performance, and minimum-window behavior
- Fixed CSV parsing for CRLF, quoted values, empty trailing fields, duplicate headers, and unknown columns
- Fixed metadata import matching so missing or ambiguous filenames are reported and skipped rather than silently applied to the wrong clip
- Fixed metadata preview playback, seeking, multichannel monitoring, clip navigation, and stale-player crashes/black frames
- Fixed waveform rendering at clip tails and preserved full duration when downsampling
- Fixed speed-duplicate FCPXML element ordering so generated XML passes Final Cut Pro DTD validation
- Fixed project save/open state, metadata persistence, and relink matching across machines with duplicate filenames
- Changing clips while video is playing now recreates the viewer/player state so the newly selected clip does not remain black
- Release builds no longer include the debug-only `get-task-allow` entitlement

### Distribution

- The app and Workflow Extension are signed with Developer ID, use hardened runtime, and are notarized by Apple
- The release script now signs, submits, staples, and validates the DMG with Gatekeeper

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
