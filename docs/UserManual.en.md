# WaveformMatcher User Manual

---

## Table of Contents
1. [What is WaveformMatcher](#1-what-is-waveformmatcher)
2. [Why Use WaveformMatcher](#2-why-use-waveformmatcher)
3. [System Requirements](#3-system-requirements)
4. [Installation](#4-installation)
5. [Interface Overview](#5-interface-overview)
6. [Standard Workflow](#6-standard-workflow)
7. [Metadata View](#7-metadata-view)
8. [Timeline Detail](#8-timeline-detail)
9. [Advanced Features](#9-advanced-features)
10. [Keyboard Shortcuts](#10-keyboard-shortcuts)
11. [Resources & Links](#11-resources--links)

---

## 1. What is WaveformMatcher

**WaveformMatcher** is a macOS application designed to solve the synchronization problem between video clips shot on camera and high-quality audio files (WAV) recorded separately on professional audio recorders.

### Core Functionality
- Analyzes audio waveforms from both video and WAV files
- Automatically finds matching sync points using Audio Fingerprinting technology
- Uses Timecode for matching when valid timecode data is available
- Reviews and edits production metadata in a spreadsheet-style table
- Imports metadata reports from CSV, XLSX, and PDF, with local PDF/OCR processing
- Refines individual sync offsets in Timeline Detail with aligned waveforms
- Exports FCPXML files ready for immediate import into Final Cut Pro

---

## 2. Why Use WaveformMatcher

### The Problem in Video Post-Production

In professional film and video production:
- **Cameras** record reference audio (scratch audio) of lower quality
- **Sound Department** records actual production audio on high-quality devices (Sound Devices, Zoom, etc.) as WAV files

**The Challenge:** When you have dozens or hundreds of clips, you must:
1. Match each video clip with its corresponding WAV file
2. Synchronize them frame-accurately
3. Do this manually in Final Cut Pro — which is extremely time-consuming

### WaveformMatcher Solution

✅ **100% Automated** — Analyzes and matches automatically  
✅ **Accurate** — Uses Audio Fingerprinting and Timecode  
✅ **Time-Saving** — Reduces hours of work to minutes  
✅ **Ready to Use** — Exports FCPXML that imports directly into Final Cut Pro

---

## 3. System Requirements

### Operating System
- **macOS 14.0+** (Sonoma or later)

### Required Software
- **Final Cut Pro** (for importing results)

### Required Files
- **FCPXML** from Final Cut Pro (`.fcpxml` file or `.fcpxmld` package)
- **WAV Files** from Sound Department (high-quality production audio)

---

## 4. Installation

WaveformMatcher 1.4.6 and later is signed with a Developer ID certificate and notarized by Apple.

1. Open the downloaded DMG.
2. Drag `WaveformMatcher.app` to **Applications**.
3. Open WaveformMatcher normally from Applications.

---

## 5. Interface Overview

When you first open the app, you'll see the main interface divided into 3 sections:

![Main interface of WaveformMatcher showing the matching table and preview.](wfm_screenshot.png)

### Main Components

#### Left Sidebar
- **FCPXML**: Shows currently loaded file
- **Media Folder**: Folder containing WAV files
- **Matching Settings**: Sync mode configuration
- **Metadata**: Opens Metadata View and selects the source policy used for preview/export
- **Output Setup**: export type, naming, format and export options. Export with the button at the bottom of the sidebar, the toolbar, or `Cmd+E`
- **Start screen**: before a source is loaded, the center of the window offers an FCPXML from your editor or Video + Audio files, and **Open Project…** to continue a saved `.wmproj`. Once loaded, the toolbar shows the source; to use different media, start a New Project

#### Main Area
- **Sync View**: Dual video/audio viewer, metadata inspector, Timeline Detail, and match table
- **Metadata View**: Editable metadata spreadsheet and Import/Export tools
- **View Switch**: Use `Cmd+1` for Sync View and `Cmd+2` for Metadata View
- **Table Scale**: Changes the table size in both views (`+` / `-`, or `Cmd++` / `Cmd+-` / `Cmd+0` with the pointer over the table)
- **Zoom keys**: `Cmd++`, `Cmd+-` and `Cmd+0` (fit) zoom whatever the pointer is over: video viewer, audio waveform, Timeline Detail or table. With the pointer elsewhere they zoom the timeline in Sync View and the table in Metadata View
- **Column widths**: Drag a Sync View column header edge to resize it; widths are remembered
- **Status bar**: The bar at the bottom of the window shows the current state (clips, matches, background work) and keyboard hints for the view you are in

---

## 6. Standard Workflow

### Step 1 — Export FCPXML from Final Cut Pro

Before using WaveformMatcher, you must export data from Final Cut Pro.

#### Event Export (Recommended)
1. Open Final Cut Pro
2. Go to Library → Right-click on desired **Event**
3. Select **Export FCPXML**
4. Save as `.fcpxml` or `.fcpxmld` file

#### Timeline (Project) Export
1. Open desired Timeline/Project
2. Menu **File → Export XML**
3. Select format as **FCPXML**
4. Save the file

### Step 2 — Import FCPXML into WaveformMatcher

Five methods available:

#### Method A — Drag & Drop
- Drag `.fcpxml` or `.fcpxmld` file onto the **Import** button in the app

#### Method B — File Menu
- Go to **File → Import FCPXML…**
- Or press `Cmd+I`

#### Method C — Workflow Extension (if installed)
1. In Final Cut Pro, open WaveformMatcher **Workflow Extension**
2. Drag **Event** or **Timeline** from Final Cut Pro into the panel
3. Main app opens automatically with data loaded

#### Method D — Open .wmproj File
- Double-click `.wmproj` file in Finder (for previously saved projects)

#### Method E — Open Media Files (no FCPXML)
- On the start screen (center of the window), click **Video** and **Audio** (or drop files/folders onto them). Each side keeps only its own file type, so camera and sound folders can be chosen separately; choosing again replaces only that side
- **File → Open Media Files…** (`Shift+Cmd+I`) accepts both at once and sorts files by extension
- Folders are searched recursively for MOV, MP4, M4V, MXF video and WAV, AIFF, MP3, M4A, CAF audio
- Video timecode is read from the QuickTime timecode track. WAV timecode is read from the BWF `bext` time reference (or the iXML timestamp) without FFprobe
- iXML fills Scene, Take, Reel (Tape), Note, Good Take (Circled) and channel names (as `dialogue.<track name>` roles)
- Files this Mac cannot read (for example BRAW or R3D) are listed after import. Bring those in through an FCPXML from your editor instead

### Step 3 — Set Media Folder

The app needs to know where your WAV files are located:

1. Look at left sidebar, **Media Folder** section
2. Click **Click to change folder**
3. Select the folder containing all your WAV files
4. App will automatically scan for WAV files in that folder and subfolders

### Step 4 — Choose Sync Mode

The app has 3 modes in **Matching Settings**:

#### 🟢 Waveform (Recommended to Try First)

**How it Works:** Analyzes audio waveforms from both video and WAV, then automatically finds matching points

**Best For:**
- Clips with clear audio recording
- Situations without timecode
- General production work

**Settings:** The tested defaults are used automatically. Click **Adjust Matching Settings** only when a job needs tuning.
- **Comparison Length**: Length of audio to compare (default 40s)
  - Shorter = Faster but potentially less accurate
  - Longer = Slower but more accurate
- **Matched ≥**: Minimum match score threshold for "matched" status (default 25%)
- **Low Conf. ≥**: Threshold for "low confidence/uncertain" matches (default 25%)

**How to Use:** Click **Start Waveform Matching** button

#### 🔵 Timecode

**How it Works:** Uses embedded timecode recorded in video and WAV files for direct matching

**Best For:**
- Cameras and audio recorders synced with timecode on set
- Using devices like Tentacle Sync, Ambient Master Clock, Timecode Systems
- Most accurate when valid timecode is available

**Caution:**
- If timecode doesn't match, results will be incorrect
- Verify both camera and audio recorded the same timecode

#### 🟡 Manual

**How it Works:** Opens clips in Sync View so you can choose Audio, set sync points, and lock each result.

**Best For:**
- Clips where waveform matching failed
- Reviewing and correcting app results
- Work requiring highest precision
- When you want to select Audio clip by clip

After a full sync has already run, starting Waveform, Timecode, or Manual Sync again asks for confirmation because the current results and edits will be replaced. To update one clip, use **Resync** in Timeline Detail or adjust it with Manual Sync.

### Step 5 — Review Match Results

After matching completes, clips are organized into 4 tabs:

| Tab | Meaning | Action |
|-----|---------|--------|
| **All** | Shows all clips | Overall view |
| **Matched** | Successfully matched clips (green ✓) | Review offset for reasonableness |
| **Review** | Matched but low score | Should check with Manual Sync |
| **Unmatched** | Failed to match | Requires Manual Sync |

**In each table row, you'll see:**
- **Filename**: The source video filename, independent of a renamed Final Cut Pro display name
- **Score**: Confidence score (0-100%) — higher is better
- **Offset**: Time shift required (in seconds)
  - Positive (+) = Video leads WAV
  - Negative (-) = Video lags WAV
- **Status**: 
  - ✓ Matched (green)
  - ⚠ Low Conf. (yellow)
  - ✗ No Match (red)
  - ✗ No Audio (gray)

Click the **Filename**, **Scene**, **Speed**, or **Status** column header to sort the table. Click the active header again to switch between ascending and descending order.

### Step 6 — Manual Sync (Adjust Unmatched Clips)

For clips in **Review** or **Unmatched**:
1. Double-click clip to open **Manual Sync** view

#### Manual Sync Interface
#### Navigation Controls

**Video Controls:**
- **▶ / ❚❚**: Play/Pause
- **J K L**: Rewind / Stop / Play (like Final Cut Pro)
  - J = Rewind (press repeatedly for faster speed)
  - K = Stop
  - L = Play (press repeatedly for faster speed)
- **◀ ▶**: Step frame by frame
- **Space**: Play/Pause (alternative)

**Waveform Controls (Audio):**
- **Click** on waveform: Move audio playhead to that position
- **Drag** on waveform: Precise audio scrubbing
- **Shift + mouse wheel**: Pan waveform left/right
- **Option + mouse wheel**: Zoom waveform in/out
- **Arrow keys**: Step by audio frame
- **Reset**: Return to default view

**Video Viewer Zoom:**
- Point at the part of the picture you want to see (for example a small slate in a wide shot), then:
  - `Cmd++` / `Cmd+-`: Zoom in/out where the pointer is
  - `Option + Scroll` or pinch on the trackpad: Zoom in/out where the pointer is
  - Scroll or drag: Move the zoomed picture
  - `Cmd+0` or click the zoom badge (e.g. `300%`): Fit the whole picture again
- Zoom resets when you move to another clip
- The synced preview in Metadata View zooms the same way
- The audio waveform works the same way: with the pointer over it, `Cmd++` / `Cmd+-`, `Option + Scroll` or pinch zoom where the pointer is, and `Cmd+0` resets it

**Channel mute and listening volume:** Each WAV channel on the audio waveform has a speaker beside its name. Click it to mute the channel; the mute is saved with the project and exported, turning that channel's role off in Final Cut Pro (in the sync clip or multicam), so what you hear is what the edit gets. Option-click a speaker to hear only that channel; Option-click it again to hear all channels, as in Final Cut Pro. When the export's **Mute Mix** is on, Mix channels start muted. Mute and volume changes can be undone with Command-Z. The vertical fader beside each channel's meter sets its listening volume (−24 to +12 dB) for channels that are too quiet or too loud; drag it (Shift-drag for fine steps) and use the reset button beside the value, or double-click, to return to 0 dB. Volume changes only what you hear in WaveformMatcher and is not exported; while any channel's volume is changed, the waveform shows **Volume: listening only** with a Reset Volume button.

**Video Seek Bar Controls (Zoom):**
- **Focus video side**, then press:
  - `Cmd++` / `Cmd+-`: Zoom seek bar in/out (when Timeline Detail is closed and the pointer is not over the picture)
  - `[` / `]`: Pan visible range
  - `0`: Reset to show full clip

**Snap Helper:**
- Hold **Shift** while dragging on waveform
- Playhead will snap to:
  - Marker guides (purple lines)
  - Slate guides (yellow lines)
  - Existing marks

#### Setting Sync Points and Locking Sync

1. **Find Sync Point:**
   - Play video and find desired sync point
   - Good points: Clap sound, clear speech, or prominent transient

2. **Set Video Sync Point:**
   - Stop video at that point
   - Click **Set Sync Point** on the VIDEO side
   - Or press `I` (`M` sets a point on whichever player is focused)

3. **Set Audio Sync Point:**
   - Play WAV and find same audio point
   - Look at waveform for matching peak
   - Click **Set Sync Point** on the AUDIO side
   - Or press `O` (`M` sets a point on whichever player is focused)

4. **Lock Sync:**
   - **Auto Lock** is enabled by default and locks as soon as both sync points are set
   - Turn Auto Lock off when you want to place and review both points before locking manually
   - Click **Locked** to unlock and adjust the points
   - Offset is saved automatically

**Visual language:** Editable sync points use large In-point heads (orange for video, green for audio). Slate guides are yellow and Final Cut Pro markers are purple. **Clear Sync Points** removes only the editable video/audio pair.

#### FCP Marker Guides (Marker Assistance)

If clips in FCPXML have markers set in Final Cut Pro:
- **Purple guide lines** appear automatically at marker positions
- If video and WAV have markers with matching names:
  - **Use Marker Pair** button appears
  - Click to create sync points from the marker pair
  - If multiple pairs exist, click **Next Pair** to cycle through
- Review the generated sync points; Auto Lock confirms them when enabled

**Note:** Marker guides remain non-editable assistants until you choose **Use Marker Pair**.

### Step 7 — Review and Edit Metadata

1. Open **Metadata View** from the sidebar, toolbar, or press `Cmd+2`.
2. Choose **Source Metadata**. Video is the safest starting point; combined modes fill missing fields from the matched audio.
3. Review Scene, Take, Reel, Camera Name, Angle, Note, Good Take, Speed, and Rec FPS.
4. Edit individual cells or use the spreadsheet tools for multiple clips.
5. If production reports are available, use **Import/Export → Import Metadata…** and review the mapping before applying.
6. Return to Sync View with `Cmd+1` whenever a sync result needs correction.

Metadata edits become the values used by FCPXML export. Hidden columns are not deleted; compatible imported custom metadata continues to round-trip unless the user overrides it.

### Step 8 — Configure Export

Return to the left sidebar, **Output Setup** section:

#### Main Settings

**Export As:** Choose output format
- **Sync Clips** (Recommended for general work):
  - Exports as `<sync-clip>` pairs
  - Each clip has video and WAV synced together
  - Best for: General editing, Single camera
  
- **Multicam**:
  - Exports as `<multicam>`
  - Organizes each camera as an angle in one file
  - Best for: Multi-camera shoots

**Event Name:** 
- Name of Event to create in Final Cut Pro
- Default: Name of imported FCPXML file
- Recommended: Use descriptive project name

**Project FPS:**
- Frame rate of timeline in Final Cut Pro
- Set to match your project (e.g., 24, 25, 30, 50, 60)
- **Important:** If set incorrectly, clips will play at wrong speed

**Resolution:**
- Output resolution
- Choose: 720p, 1080p, 4K or Custom

#### Additional Options

**Clip Name:** Choose the naming source
- **Video**: Final Cut Pro browser name of the video clip
- **Video Filename**: Source video filename without its extension
- **Audio**: Final Cut Pro browser name of the matched production-audio clip
- **Audio Filename**: Source audio filename without its extension
- **Metadata**: Builds a name from the active metadata naming template and falls back to the video clip name when no usable metadata exists

**Metadata Template:** The default is `Scene_Take_Angle`. Empty fields are skipped cleanly. User-created custom metadata can also be added to a naming template.

**MC Angle Name:** For Multicam output, choose Filename, Camera Angle, or Camera Name.

**Spatial Conform:** (When clip resolution doesn't match output)
- **Fit**: Scale clip to fit frame showing entire image (may have black bars)
- **Fill**: Scale to fill frame (may crop image)

**Trim To Video Area:**
- **On (Recommended)**: Trim output to video-only range
- **Off**: Keep full range (audio-only sections marked as Rejected)

**Mute Mix Track:**
- **On (Recommended)**: Mute video scratch audio in output
- **Off**: Keep video audio (may cause double audio)

**Auto Speed:**
- Appears when clip has Record Frame Rate metadata
- Calculates speed automatically: `Speed = Record FPS ÷ Project FPS`
- Example: Shot 48fps, timeline 24fps = 200% speed

**Scenes:** Group clips by Scene in the exported event
- **None**: No scene grouping
- **Keywords**: Each clip gets a keyword with its Scene, so Final Cut Pro lists a keyword collection per scene
- **Smart Collections**: One smart collection per scene, matching the Scene field exactly (scene 10 does not also collect 10A)
- **Keywords + Smart Collections**: Both
- **Group By** (when Scene holds scene and cut, e.g. S127AC1 = scene 127A, cut 1): **Whole Value** (each value its own group), **Scene Only** (S127AC1 and S127AC2 both go to S127A), or **Scene → Cut** (a folder per scene with its cuts inside). **Rule and Preview…** sets where the cut starts: a cut marker (C: S127AC1 → S127A + C1, S127CV3 → S127 + CV3), a separator (_: E03_09_2 → E03_09 + 2) or a regular expression. It shows the three choices side by side with what a scene from this project becomes in each, and the Scene Keywords folder as Final Cut Pro will show it. Smart collections still match exact Scene values, so scene 127 never collects 127A.

**Synced / Not Synced:** Sync clips and multicam clips carry the keyword **Synced**. Videos without a match and WAVs no video was synced with are still exported, with the keyword **Not Synced**, so nothing from the source is lost. Scene keyword collections go in a **Scene Keywords** folder and smart collections in a **Scene Smart Collections** folder; Synced and Not Synced stay outside them.

**Folder keywords:** Media opened directly gets a keyword with its folder name (camera or sound roll), as Final Cut Pro adds when importing; clips from an FCPXML keep their own keywords.

### Step 9 — Export and Import to Final Cut Pro

1. **Click Export Button:**
   - Click **Export FCPXML Event** (bottom left sidebar)
   - Or press `Cmd+E`

2. **Choose Save Location:**
   - Select destination folder
   - Name file (default: `[Event Name]_Sync Clips.fcpxml`)
   - Click **Save**

3. **Import to Final Cut Pro:**
   
   **Method A — Use Send To Final Cut Pro:**
   - In WaveformMatcher, click **Send To Final Cut Pro** button
   - File opens in Final Cut Pro automatically
   
   **Method B — Manual Import:**
   - Open Final Cut Pro
   - Menu **File → Import → XML…**
   - Select exported `.fcpxml` file
   - Click **Import**

4. **Verify Results:**
   - Open imported Event
   - Verify clips are synced correctly
   - Check clip speed (if using Auto Speed)

---

## 7. Metadata View

Metadata View is the preparation stage between synchronization and FCPXML export. It presents one row per video result and keeps an authoritative set of resolved metadata values for export.

### 7.1 Source Metadata

The **Source Metadata** menu controls the starting values shown in the table:

- **Video**: Use video metadata only.
- **Audio**: Use metadata from the matched audio when available.
- **Video + Audio**: Start with video and fill empty fields from audio.
- **Audio + Video**: Start with audio and fill empty fields from video.

Changing the source policy does not erase manual edits. A manually edited cell remains an override until it is reset.

### 7.2 Built-in and Custom Columns

Built-in editable fields include Clip Name, Scene, Take, Reel, Camera Name, Angle, Note, Good Take, Speed, and Rec FPS.

- **Clip Name** previews the name that will be exported. It follows the Clip Name option automatically; editing it creates an orange manual override, and Reset returns it to the automatic value. Filename-based values omit the source extension.
- **Note** exports as a Final Cut Pro note.
- **Good Take** exports as a Final Cut Pro Favorite rating. For Multicam, a favorite on any contributing clip is retained on the exported multicam result.
- **Rec FPS** uses explicit Record/Sensor FPS when available and otherwise begins with the clip frame rate.
- **Speed** can remain automatic or be overridden manually per clip.
- **+ Column** shows compatible custom metadata found in the imported FCPXML, hides/shows columns, and creates or deletes WFM custom columns.

Hidden columns remain in the project and continue to round-trip. Deleting a WFM-created custom column removes that table field after confirmation.

### 7.3 Spreadsheet Editing

- Single-click a cell to select it; double-click or press `Return` to edit text.
- Drag across cells or Shift-click to create a rectangular selection.
- Copy and paste tab-separated rectangles between WaveformMatcher and spreadsheet apps. Select only the top-left destination cell to paste a copied block.
- **Fill** copies the source value down the selected range; use the fill handle for drag-fill.
- **Number** creates a numeric sequence across selected rows.
- **Clear** removes selected overrides; **Reset Selected** restores resolved source values.
- **Find** supports Selection, Active Column, or Visible Columns, with Match Case and Whole Cell options.
- Cell edits and table-structure actions participate in Undo/Redo.
- Resize columns by dragging header dividers. Use horizontal scrolling when the visible columns exceed the window width.

### 7.4 Auto Speed and Rec FPS

Auto Speed calculates `Rec FPS ÷ Project FPS × 100`.

- Blue Speed values are automatic, including normal `100%`.
- Orange Speed or Rec FPS values are manual overrides.
- Editing Rec FPS recalculates Speed only while that row remains in Auto mode.
- Editing Speed manually unlocks that clip from later automatic recalculation; other clips remain automatic.
- Click **Auto Speed** to reapply automatic calculation to selected rows, or to current visible rows when nothing is selected.

### 7.5 Synced Preview

- Press `Space` to open the synced preview for the active row, paused on the clip's clap; press `Space` again to play. It opens as a floating mini player window that stays on top: move it anywhere (another screen too) and resize it from any edge, and keep editing table cells while it plays. It remembers its place and size.
- While it is open: `Space` plays or pauses, `J` / `K` / `L` shuttle (press again to go faster), `←` / `→` step one frame, `↑` / `↓` change row, and `Esc` closes it. Changing clip keeps playing, or stays paused when you had paused. While you type in a cell, the keys go to the cell.
- The mini player opens each clip on its sync point or slate clap, as Sync View does, and shows the clip's source timecode. The full-screen button (or `Shift+Cmd+F`) plays it full screen. `Cmd++` / `Cmd+-` / `Cmd+0`, `Option + Scroll` and pinch zoom its picture.
- The preview uses the stored WFM offset and a stereo monitor mix for multichannel WAV playback; export still retains the original multichannel audio.
- The preview follows the active row: click a row or use `↑` / `↓`.
- The scrub bar shows FCP markers, manual sync points, slate guides, and slate visible ranges when available.
- Press `Option+Space` only when a raw Finder Quick Look reference is needed.

### 7.6 Import Metadata

Choose **Import/Export → Import Metadata…** or press `Option+Cmd+I`.

Supported input:
- **CSV**: Reliable interchange and round-trip editing.
- **XLSX**: Select the worksheet and header row when the workbook contains multiple tables or title rows.
- **PDF**: Reconstructs table structure locally and uses Apple Vision OCR when the PDF text layer is missing or unreliable.

Import workflow:
1. Select the source file.
2. For XLSX/PDF, choose the correct table or header row if requested.
3. Choose the matching rule. Prefer exact Filename/Path; structured reports may offer Reel + Clip or token-based matching.
4. Map each source column to an existing metadata field, Ignore it, or create a custom field.
5. Check the matched, needs-review, and skipped counts before applying.
6. Leave **Overwrite manual edits** off unless the imported report should replace existing manual work.
7. Apply the import. Missing or ambiguous rows are skipped rather than guessed.

PDF processing is entirely local. OCR results, especially Thai text and reports with merged cells, should be reviewed before export. Review warnings are guidance; they do not modify a clip until **Apply Import** is pressed.

### 7.7 Export Metadata

Choose **Import/Export → Export Metadata…** or press `Option+Cmd+E`.

- Row scope: All Project Rows, Current Filter/Search, or Selected Rows.
- Column scope: All Metadata Columns or Visible Columns.
- Output is CSV for interchange with spreadsheet and production-report workflows.

### 7.8 Reel Helper and Metadata Naming

The **Reel** menu can populate visible rows from Embedded Reel, Source Filename, or Folder Name. **Custom Value…** applies to the current selection/active row.

When **Clip Name → Metadata** is selected, the naming builder uses metadata fields in the chosen order and removes empty separators. Each token can have optional text before it, and the separator can be underscore, hyphen, slash, hash, space, or none. The default template is `Scene_Take_Angle`; if no field produces a usable name, WFM uses the video clip name. Speed duplicates use the same base name before appending the FPS suffix. In Multicam mode, all rows sharing the same production-audio clip show and edit one group-level Clip Name.

---

## 8. Timeline Detail

Timeline Detail is the clip-by-clip sync editor inside Sync View. It opens by default for the active clip and can also be reopened by double-clicking a filename.

### 8.1 Reading the Timeline

- The blue **Video** lane shows mixed camera scratch audio.
- The green **Audio Match** lane shows the matched production audio at the stored offset.
- Both lanes share one ruler and playhead, so clap transients can be compared visually.
- FCP markers, manual sync points, slate ranges, and slate guides remain visible as review references.
- Clicking the Video lane focuses video playback; clicking the Audio Match lane focuses audio. The active lane is outlined.

- Skimming, as in Final Cut Pro: while paused, move the pointer over Timeline Detail to see the frame under it (pink skimmer line, `S` or the hand button) and, with audio skimming on (`Shift+S` or the speaker button), hear short snippets. Moving the pointer away goes back to the playhead; clicking moves the playhead. With audio skimming on, the audio waveform in Sync View plays the sound under the pointer too, and while you drag on it. Both switches are also in the View menu (Skimming, Audio Skimming).

### 8.2 Adjusting Sync

- Drag the Audio Match lane horizontally to change the offset.
- Press `,` or `.` to nudge by one timeline frame; hold Shift for ten frames.
- Use `Cmd++` / `Cmd+-` to zoom and `Cmd+0` to fit the complete extent.
- Use the reset-offset control to return Audio Match to zero offset.
- One drag becomes one Undo step. The project is marked changed only when the committed value differs.
- A committed drag/nudge or manually locked marker/slate pair receives the orange **Manual** status while remaining valid for Matched filtering and export.

### 8.3 Pair-scoped Resync

Use the Resync menu in the Timeline header to run **Waveform** or **Timecode** again for only the displayed Video and Audio Match. It does not search other Audio files in the project. The replacement result is undoable.

Auto Lock is enabled by default. Turn it off when you want to place and inspect both sync points before committing with **Lock Sync**.

---

## 9. Advanced Features

### 9.1 Detect Slate

**What is a Film Slate?**

A **Film Slate** (also called **Clapperboard** or **Clapboard**) is a device used in film and video production. It consists of a board displaying information about the scene, take, and other details, plus hinged sticks (clapper sticks) that create a sharp "clap!" sound.

**Purpose of Slate:**
1. **Visual Information**: Shows Scene, Take, Camera, Date, etc. in frame
2. **Sync Point**: The visual and audio moment of clapping provides the clearest reference point for synchronization

**What is Detect Slate?**

Finds the slate and clap automatically, in about 2 seconds per clip. All models are built into the app and run on the Mac:
- **Slate in picture**: A trained clapperboard detector marks the frames where the slate is visible. A board that stays in frame for the whole shot is ignored
- **Picture clap**: The frame where the sticks close
  - **Digital (timecode) slates**: the app reads the timecode display until it freezes
  - **Handwritten slates**: an open/closed stick detector finds the first frame the sticks are shut
- **Audio clap**: The clap in the WAV, taken right at the picture clap

Detect Slate is a guide: review the result before you lock sync. When a take has no audible clap, only the slate in picture is marked.

**Clips that are not synced yet**

Detect Slate also works on clips that Waveform or Timecode could not sync:
- **Digital slate**: The frozen slate timecode is the WAV timecode of the clap, so the app finds the clap in the WAV from it
- **Timecode offset**: If the video and WAV both have timecode, the app uses that offset to look for the clap
- **Otherwise**: A built-in clap sound detector ranks claps in the WAV. The best one is used, and the top three are listed under **WAV clap candidates** in the ◎ menu so you can try another

In the inspector, the **FIND** row holds Detect Slate and the ◎ menu (Use Detect Slate, marker pairs, WAV clap candidates); the **LOCK** row holds Auto Lock and Lock Sync.

**After sync**

- When Waveform or Timecode sync finishes, the app looks for the clap in each synced clip's WAV in the background (about 0.2 s a clip). Selecting a synced clip then opens it on the slate, so you can check the sync straight away. This guess comes from the sound alone: it looks for the short, sharp sound of the sticks within the first and last 8 seconds of the clip, and lands on another sound about one time in five; it only places the playhead and never changes the sync.
- Tick **Detect Slate after sync** under the Start button to also run Detect Slate on every synced clip in the background (about 3 s a clip). Selecting a clip then opens on the clap found in picture. Leave it off when you do not need it.
- The status bar shows the background work and its progress; click its ✕ to stop it (results so far are kept). Results are saved with the project.

#### How to Use Detect Slate

1. **Open Manual Sync** for desired clip

2. **Click Detect Slate Button:**
   - App scans beginning/end of clip
   - Searches for likely slate-visible ranges (Head/Tail windows)
   - Searches for clap sound in WAV

3. **Review Results:**
   - **Yellow bar** on video seek bar = Likely slate-visible range
   - **Guide line** = Probable visual clap point
   - **Audio guide line** = Detected audio clap peak

4. **Use Guide:**
   - If guide looks correct → Click **Use Detect Slate**
   - System places video/audio marks automatically
   - **Review again** → Click **Lock Sync**

5. **If Guide is Wrong:**
   - Don't use Use Detect Slate
   - Set marks manually using Manual Sync instead

#### What Detect Slate Saves

When you click Detect Slate, the system saves:
- **Visible Ranges**: Time ranges where slate is likely visible
- **Visual Guide Time**: Time point of visual clap
- **Audio Guide Time**: Time point of audio clap
- **Debug Candidates**: Other detected candidates

**Benefits:**
- Click Detect Slate again on same clip → Returns to saved guide instead of re-scanning
- Saved in `.wmproj` file → Guides persist when reopening project
- Useful starting point for Manual Sync

#### Detect Slate Limitations

⚠️ **Video Detection:**
- May miss slate if:
  - Image too dark
  - Slate unclear
  - Other objects resemble slate
- May lock onto wrong object if similar items present

⚠️ **Audio Detection:**
- Works best when:
  - Clap sound is clear with distinct transient
  - Minimal background noise
- May fail when:
  - Short speech sounds resemble clap
  - Other transients louder than clap
  - Clap sound unclear

**Recommendation:** Use Detect Slate as a **starting point** only — always verify and adjust with Manual Sync

### 9.2 Auto Speed

**What is Auto Speed?**

Feature for automatic clip speed adjustment when shooting frame rate differs from timeline rate.

**Usage Examples:**

1. **High Frame Rate (HFR):**
   - Shot 48fps, timeline 24fps
   - Speed = 48 ÷ 24 = **200%** (50% slow motion)
   
2. **Variable Frame Rate:**
   - Shot 60fps, timeline 30fps
   - Speed = 60 ÷ 30 = **200%** (50% slow motion)

3. **Normal Speed:**
   - Shot 24fps, timeline 24fps
   - Speed = 24 ÷ 24 = **100%** (Normal speed)

#### Supported Metadata

Auto Speed works when clips have **Record Frame Rate** metadata from:

**1. Compatible Final Cut Pro metadata:**
- Works with Record/Sensor FPS fields already present in the FCPXML
- Can read compatible metadata written by production logging tools, including Shot Notes X
- The app treats these fields as imported metadata, not as a required dependency

**2. Camera Meta**
- Metadata embedded in camera files
- Supported field names:
  - Sensor FPS
  - Record Frame Rate
  - Recording Frame Rate

#### How to Use Auto Speed

1. **Check if Button Appears:**
   - In clip table, see **Video Speed** column
   - **Auto Speed** button appears if metadata exists

2. **Click Auto Speed Button:**
   - System calculates: `Record FPS ÷ Project FPS`
   - Speed value entered automatically

3. **Export:**
   - Speed saved in FCPXML
   - When imported to Final Cut Pro, clips play at calculated speed

### 9.3 Project Files (.wmproj)

**What is .wmproj?**

WaveformMatcher project file used to save work-in-progress for later continuation.

**What's Saved:**
- ✅ All clip-to-WAV pairings
- ✅ Sync offsets
- ✅ Manual marks
- ✅ Sync method used (manual / marker pair / Detect Slate)
- ✅ Auto speed values
- ✅ Slate guide data (visible ranges, visual/audio guide times)
- ✅ Detect Slate debug candidates
- ✅ Export settings

#### How to Use

**Save Project:**
- **File → Save** or press `Cmd+S`
- **File → Save As…** to save with new name
- Recommended: Save before closing app

**Open Project:**
- **File → Open…** or press `Cmd+O`
- Or **double-click** `.wmproj` file in Finder
- **File → Open Recent** lists the last 10 projects opened or saved; **Clear Menu** empties it
- After app installation, `.wmproj` files are registered with system

**Benefits:**
- Save work → Resume later without redoing
- Keep backup of work
- Share file for others to continue

---

### 9.4 Video Output on a Second Display

Show the picture full screen on another display, like Final Cut Pro's A/V Output, while you keep working on the main screen.

- **Turn on/off:** **View → Turn Video Output On** (`Cmd+P`), or the display button at the right of the toolbar. The output covers the whole screen, menu bar included.
- **Choose the display:** **View → Output Display** lists the connected screens. By default the output uses the first screen that is not showing the main window; your choice is remembered and used again when that screen is connected.
- **What it shows:** the clip in the viewer you are using. In Sync View, the viewer's clip. In Metadata View, a transport bar appears above the status bar and plays the active row on the output: `Space` plays or pauses, `J` / `K` / `L` shuttle and `,` / `.` step a frame, while the arrow keys keep moving between cells. **Open Mini Player** on the bar opens the mini player, which drives the output while it is open. Play, J/K/L, frame steps and clip changes are all controlled from the main window. Sound stays on the Mac's output.
- **Overlay (burn-in):** **View → Show Overlay on Output** turns it on; **View → Output Overlay…** chooses what it shows, like DaVinci Resolve's Data Burn-In. Pick any of Source Timecode, Audio Timecode, Video and Audio Filename, Scene, Take, Reel, Camera Name, Angle, Note, Sync Status, Speed, Rec FPS and your own text; put each in one of six places (top or bottom; left, center or right), with or without a short label (SRC, SC, TK…), and drag to set their order. Text size, color (white or yellow), background and margin are adjustable, with a live preview. The settings are remembered.
- With one display only, the command is unavailable ("Connect a second display"). If the output display is disconnected, Video Output turns off.

## 10. Keyboard Shortcuts

**Customize:** **Help → Keyboard Shortcuts…** lists every command. Click a command's key and press the new one (Esc cancels); the window warns when the key is already used by another command, which then gives it up. Reset puts one command back, Reset All all of them. Commands without a built-in key — Detect Slate, Use Detect Slate, Lock Sync, Auto Lock, Timeline Detail, Send to Final Cut Pro, the output overlay and its settings, Open Mini Player — can be given one. The tables below list the built-in keys.

### General Operations

| Action | Shortcut |
|--------|----------|
| Import FCPXML | `Cmd+I` |
| Export FCPXML | `Cmd+E` |
| Save project | `Cmd+S` |
| Open project | `Cmd+O` |
| Video Output on second display | `Cmd+P` |
| Open Media Files | `Shift+Cmd+I` |
| Viewer fullscreen | `Shift+Cmd+F` |
| User Manual | `Shift+Cmd+/` |
| Sync View / Metadata View | `Cmd+1` / `Cmd+2` |
| Show/Hide Sidebar | `Cmd+3` |
| Focus Search | `Option+F` |
| Import / Export Metadata | `Option+Cmd+I` / `Option+Cmd+E` |

### Video Playback

| Action | Shortcut |
|--------|----------|
| Play / Pause | `K` or `Space` |
| Rewind | `J` (repeat for faster) |
| Fast Forward | `L` (repeat for faster) |
| Step Frame (Left) | `◀` (Left Arrow) |
| Step Frame (Right) | `▶` (Right Arrow) |

### Waveform Navigation

| Action | Shortcut |
|--------|----------|
| Pan waveform (Left/Right) | `Shift + Scroll` |
| Zoom waveform (In/Out) | `Option + Scroll`, pinch, or `Cmd++` / `Cmd+-` with the pointer over it |
| Snap while dragging | Hold `Shift` |
| Audio frame step (Left) | `←` (Left Arrow) |
| Audio frame step (Right) | `→` (Right Arrow) |
| Reset zoom | `Reset` button |

### Video Viewer

| Action | Shortcut |
|--------|----------|
| Zoom in / out (pointer over the viewer) | `Cmd++` / `Cmd+-` |
| Zoom where the pointer is | `Option + Scroll` or pinch |
| Move the zoomed picture | Scroll or drag |
| Fit picture | `Cmd+0` |

### Video Seek Bar

| Action | Shortcut |
|--------|----------|
| Zoom in | `Cmd++` |
| Zoom out | `Cmd+-` |
| Pan left | `[` (Left Bracket) |
| Pan right | `]` (Right Bracket) |
| Reset view | `0` (Zero) |

### Manual Sync

| Action | Shortcut |
|--------|----------|
| Set sync point on focused player | `M` |
| Set Video Sync Point | `I` |
| Set Audio Sync Point | `O` |
| Next Clip | `↓` (Down Arrow) |
| Previous Clip | `↑` (Up Arrow) |

### Sync and Filters

| Action | Shortcut |
|--------|----------|
| Waveform / Timecode / Manual mode | `Option+1` / `Option+2` / `Option+3` |
| Start selected sync mode | `Option+S` |
| All / Matched / Review / Unmatched | `Option+4` / `Option+5` / `Option+6` / `Option+7` |

### Metadata Table

| Action | Shortcut |
|--------|----------|
| Copy / Paste selected cells | `Option+Cmd+C` / `Option+Cmd+V` |
| Fill down / Auto-number | `Option+D` / `Option+N` |
| Clear / Reset selected | `Cmd+Delete` / `Cmd+R` |
| Find & Replace | `Cmd+F` |
| Open synced preview (mini player) | `Space` |
| Mini player: play/pause · shuttle · frame step · close | `Space` · `J` `K` `L` · `←` `→` · `Esc` |
| Raw media Quick Look | `Option+Space` |
| Table zoom in / out / reset | `+` / `-`, or `Cmd++` / `Cmd+-` / `Cmd+0` with the pointer over the table |

### Timeline Detail

| Action | Shortcut |
|--------|----------|
| Nudge Audio Match one frame | `,` / `.` |
| Nudge Audio Match ten frames | `Shift+,` / `Shift+.` |
| Timeline zoom in / out | `Cmd++` / `Cmd+-` |
| Fit timeline | `Cmd+0` |
| Video skimming / audio skimming | `S` / `Shift+S` |
| Zoom / pan | `Option + Scroll` or pinch / sideways scroll |
| Close Timeline Detail | `Esc` |

The complete searchable list is available from **Help → Keyboard Shortcuts…**.

---

## 11. Resources & Links

### Downloads & Documentation

- **Download WaveformMatcher / Releases & Docs:**
  [github.com/wtembundit/WaveformMatcher](https://github.com/wtembundit/WaveformMatcher)

- **Changelog:**  
  [CHANGELOG.md](https://github.com/wtembundit/WaveformMatcher/blob/main/CHANGELOG.md)

### Related Tools

**Shot Notes X compatibility**  
WaveformMatcher can read compatible Scene, Take, Camera, Lens, and Record FPS metadata when it is already present in the imported FCPXML.

**FFmpeg / FFprobe**  
Tools for video and audio processing (used for reading timecode from raw files)
- **Website:** [ffmpeg.org](https://ffmpeg.org)
- **License:** LGPL 2.1+
- **Note:** WaveformMatcher can install ffprobe automatically when needed

### Support

**Report Issues / Request Features:**
- Create Issue on GitHub: [github.com/wtembundit/WaveformMatcher/issues](https://github.com/wtembundit/WaveformMatcher/issues)

**Release repository:**
- This public repository hosts releases and documentation.

---

## Appendices

### A. Understanding Timecode

**What is Timecode?**

Timecode is a system for assigning "time addresses" (Hours:Minutes:Seconds:Frames) to every frame of video and audio, enabling frame-accurate referencing between different files.

**Format:** `HH:MM:SS:FF`
- Example: `01:23:45:12` = 1 hour 23 minutes 45 seconds frame 12

**Timecode Types:**
1. **LTC (Linear Timecode):** Embedded in audio signal
2. **VITC (Vertical Interval Timecode):** Embedded in video signal
3. **Embedded Timecode:** Stored in file metadata

**Syncing Timecode on Set:**
- Use devices like Tentacle Sync, Ambient Master Clock
- Send same timecode to both camera and audio recorder
- Ensures all files have matching timecode

### B. Camera Settings for Optimal Workflow

**For Best Results:**

1. **Record Scratch Audio:**
   - Always enable camera microphone
   - Set appropriate audio levels (not too low/high)
   - This audio is used for Waveform Matching

2. **Slate Every Take:**
   - Clap sticks clearly
   - Hold slate steady long enough to read info
   - Wait 1-2 seconds after clap before action

3. **Record Metadata:**
   - Log Scene/Take/Camera in the production tool of your choice
   - Note Frame Rate used for shooting
   - Sync timecode if possible

### C. Glossary

| Term | Definition |
|------|------------|
| **FCPXML** | Final Cut Pro XML — XML file containing Final Cut Pro project data |
| **Scratch Audio** | Reference audio recorded by camera (lower quality) |
| **WAV** | High-quality audio file from professional audio recorder |
| **Waveform** | Graph showing audio level over time |
| **Timecode** | Time code assigned to each frame |
| **Slate / Clapperboard** | Film slate used on set for identification and sync |
| **Sync** | Aligning video and audio in time |
| **Offset** | Time difference between video and audio |
| **Multicam** | Multi-camera shooting |
| **Frame Rate (FPS)** | Number of frames per second |

---

**WaveformMatcher v1.5.0**
Built with assistance from Claude Code and Codex
[Report Issues and Downloads](https://github.com/wtembundit/WaveformMatcher)
