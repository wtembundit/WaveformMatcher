# WaveformMatcher

macOS app that matches video clips to audio WAV files by comparing waveforms, then exports a ready-to-import FCPXML for Final Cut Pro.

## Features

- **Waveform matching** — compares audio fingerprints between video and WAV files to find sync points automatically
- **Timecode matching** — aligns clips using embedded timecode when available
- **Manual sync mode** — opens clips directly in Manual Sync without running waveform or timecode first
- **Experimental Detect Slate guide** — finds likely slate visible ranges, visual clap guides, and audio clap candidates; saves results in `.wmproj` and can apply them with `Use Detect Slate`
- **Manual sync points** — distinct video/audio In-point controls with optional Auto Lock, unlock-to-adjust, and Undo
- **Sortable clip table** — sort source filenames, scene, speed, or status in either direction
- **Keyboard shortcuts window** — searchable command reference from the Help menu
- **Export modes**
  - **Sync Clips** — one `<sync-clip>` per matched pair
  - **Multicam** — one `<multicam>` per WAV file with all matching cameras as angles
- **Timeline-aware parsing** — supports Event XML, split timeline cuts, separate timeline clips, connected audio, and primary storyline audio
- **Metadata** — round-trips FCP studio tags (reel, scene, shot, camera angle, keywords) from source FCPXML
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

This app is not notarized with Apple. On first launch, macOS Gatekeeper may block it.

**Option 1 — Right-click to open:**
Right-click `WaveformMatcher.app` → **Open** → click **Open** in the dialog.

If macOS still blocks the app, go to **System Settings** → **Privacy & Security** and click **Open Anyway**.

**Option 2 — Remove quarantine flag via Terminal:**
```bash
xattr -dr com.apple.quarantine /Applications/WaveformMatcher.app
```

## Documentation

- [Changelog](CHANGELOG.md)
- [User Manual (English source)](docs/UserManual.en.md)
- [คู่มือการใช้งาน (ภาษาไทย)](docs/UserManual.th.md)
- [Release Website](https://wtembundit.github.io/WaveformMatcher/)
- [User Manual PDF](UserManual.pdf)

## 1.4.5 Release Notes

WaveformMatcher 1.4.5 is a bug-fix and stability release focused on smoother review and safer project handoff.

- Smoother clip-table scrolling and lighter WAV match controls
- Dynamic Scene/Take column sizing to avoid overlapping text
- More accurate Manual Sync waveform drawing for long or trimmed audio
- Safer relink behavior when duplicate filenames exist in copied media folders
- Save state updates immediately after saving, so closing right away does not ask again
- Initial XCTest regression coverage for parser, generator, project files, relink, speed input, and waveform downsampling

## Releases

Source code is maintained in this repository.

Release artifacts and the public download page live in this repository.

The GitHub Pages release website is published from [`docs/`](docs/).

### Releasing a new version

1. Bump `CURRENT_PROJECT_VERSION` and `MARKETING_VERSION` in Xcode build settings
2. Commit, tag, and push:
   ```bash
   git tag vX.X && git push origin main && git push origin vX.X
   ```
3. Build a signed Release app and DMG with the release script:
   ```bash
   ./scripts/build_release_dmg.sh
   ```
   This script builds from the Xcode Release configuration with code signing enabled so the exported app keeps its sandbox entitlements.
4. Refresh the public docs and user manual PDF:
   ```bash
   python3 scripts/generate_user_manual_pdf.py
   ```
5. Create the GitHub release in this repository and upload the generated DMG:
   ```bash
   gh release create vX.X WaveformMatcher-X.X.dmg \
     --title "Version X.X"
   ```

## Contributing

Contributions are welcome.

Recommended workflow:

1. Fork the repo and create a focused branch
2. Build locally with Xcode or:
   ```bash
   xcodebuild -project WaveformMatcher.xcodeproj -scheme WaveformMatcher -sdk macosx build CODE_SIGNING_ALLOWED=NO
   ```
3. Keep large local assets out of git:
   - `ffprobe`
   - `rtdetr-*.pt`
   - local datasets and generated release artifacts
4. If you touch user-facing behavior, update:
   - localization strings
   - user manual source in `docs/`
   - website assets in `docs/` when relevant
   - `CHANGELOG.md`
5. Open a pull request with a short testing note

## Dependencies

- `ffprobe` — optional fallback for raw-file timecode reads when FCPXML/native data is insufficient
  The app can now install FFprobe on demand when a timecode workflow truly needs it.

## Acknowledgements

- [FFmpeg / ffprobe](https://ffmpeg.org) — audio and video processing; licensed under LGPL 2.1+

---
*Built with the assistance of [Claude Code](https://claude.ai/code) and Codex*
