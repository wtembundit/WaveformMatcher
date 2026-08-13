# WaveformMatcher User Manual

---

## Table of Contents
1. [What is WaveformMatcher](#1-what-is-waveformmatcher)
2. [Why Use WaveformMatcher](#2-why-use-waveformmatcher)
3. [System Requirements](#3-system-requirements)
4. [Installation](#4-installation)
5. [Interface Overview](#5-interface-overview)
6. [Standard Workflow](#6-standard-workflow)
7. [Advanced Features](#7-advanced-features)
8. [Keyboard Shortcuts](#8-keyboard-shortcuts)
9. [Resources & Links](#9-resources--links)

---

## 1. What is WaveformMatcher

**WaveformMatcher** is a macOS application designed to solve the synchronization problem between video clips shot on camera and high-quality audio files (WAV) recorded separately on professional audio recorders.

### Core Functionality
- Analyzes audio waveforms from both video and WAV files
- Automatically finds matching sync points using Audio Fingerprinting technology
- Uses Timecode for matching when valid timecode data is available
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

### ⚠️ Important: App is Not Notarized by Apple

Since WaveformMatcher is an independent app that hasn't been submitted to Apple for notarization, macOS Gatekeeper will block it on first launch.

#### Option 1 — Right-Click to Open (Recommended)

1. In Finder, **right-click** on `WaveformMatcher.app`
2. Select **Open** from the menu
3. In the dialog that appears, click **Open** again
4. If still blocked:
   - Go to **System Settings → Privacy & Security**
   - Click **Open Anyway**

#### Option 2 — Use Terminal

1. Open **Terminal**
2. Run the command (adjust the path to where you placed the app):
   ```bash
   xattr -dr com.apple.quarantine /Applications/WaveformMatcher.app
   ```
3. Open the app normally

---

## 5. Interface Overview

When you first open the app, you'll see the main interface divided into 3 sections:

![Main interface of WaveformMatcher showing the matching table and preview.](wfm_screenshot.png)

### Main Components

#### Left Sidebar
- **FCPXML**: Shows currently loaded file
- **Media Folder**: Folder containing WAV files
- **Matching Settings**: Sync mode configuration
- **Export Settings**: Export configuration

#### Main Area
- **Clip Table**: Lists source video filenames and supports ascending or descending sorting by Filename, Scene, Speed, and Status
- **Waveform Viewer**: Multi-channel WAV waveform display
- **Video Player**: Video playback with Seek Bar

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

Four methods available:

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

**Settings:**
- **Comparison Length**: Length of audio to compare (default 48s)
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

**How it Works:** Skips automatic matching, opens Manual Sync for clip-by-clip manual work

**Best For:**
- Clips where waveform matching failed
- Reviewing and correcting app results
- Work requiring highest precision
- When you want to select WAVs clip by clip

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

**Video Seek Bar Controls (Zoom):**
- **Focus video side**, then press:
  - `-` / `+`: Zoom seek bar in/out
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

### Step 7 — Configure Export

Return to left sidebar, **Export Settings** section:

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

**Timeline FPS:**
- Frame rate of timeline in Final Cut Pro
- Set to match your project (e.g., 24, 25, 30, 50, 60)
- **Important:** If set incorrectly, clips will play at wrong speed

**Resolution:**
- Output resolution
- Choose: 720p, 1080p, 4K or Custom

#### Additional Options

**Metadata From:** Choose metadata source
- **Video Clip**: Use metadata from video file (Scene, Take, Camera Angle, etc.)
- **Audio (WAV)**: Use metadata from WAV file

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
- Calculates speed automatically: `Speed = Record FPS ÷ Timeline FPS`
- Example: Shot 48fps, timeline 24fps = 200% speed

### Step 8 — Export and Import to Final Cut Pro

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

## 7. Advanced Features

### 7.1 Detect Slate (Experimental) ⚠️

**What is a Film Slate?**

A **Film Slate** (also called **Clapperboard** or **Clapboard**) is a device used in film and video production. It consists of a board displaying information about the scene, take, and other details, plus hinged sticks (clapper sticks) that create a sharp "clap!" sound.

**Purpose of Slate:**
1. **Visual Information**: Shows Scene, Take, Camera, Date, etc. in frame
2. **Sync Point**: The visual and audio moment of clapping provides the clearest reference point for synchronization

**What is Detect Slate?**

An experimental feature that attempts to automatically find slate/clap points by:
- **Video side**: Scanning for frames showing the slate board and clapper sticks
- **Audio side**: Finding the sharp peak of the clap sound

⚠️ **Warning:** This feature is still experimental — **always review before using**

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

### 7.2 Auto Speed

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

**1. Shot Notes X:**
- macOS app for recording production metadata
- Records: Scene, Take, Camera, Lens, Frame Rate, etc.
- Writes metadata directly to Final Cut Pro clips
- Download: [Shot Notes X on App Store](https://apps.apple.com/app/shot-notes-x/id853468135)

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
   - System calculates: `Record FPS ÷ Timeline FPS`
   - Speed value entered automatically

3. **Export:**
   - Speed saved in FCPXML
   - When imported to Final Cut Pro, clips play at calculated speed

### 7.3 Project Files (.wmproj)

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
- After app installation, `.wmproj` files are registered with system

**Benefits:**
- Save work → Resume later without redoing
- Keep backup of work
- Share file for others to continue

---

## 8. Keyboard Shortcuts

### General Operations

| Action | Shortcut |
|--------|----------|
| Import FCPXML | `Cmd+I` |
| Export FCPXML | `Cmd+E` |
| Save project | `Cmd+S` |
| Open project | `Cmd+O` |

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
| Zoom waveform (In/Out) | `Option + Scroll` |
| Snap while dragging | Hold `Shift` |
| Audio frame step (Left) | `←` (Left Arrow) |
| Audio frame step (Right) | `→` (Right Arrow) |
| Reset zoom | `Reset` button |

### Video Seek Bar

| Action | Shortcut |
|--------|----------|
| Zoom in | `-` (Minus) |
| Zoom out | `+` (Plus) |
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

The complete searchable list is available from **Help → Keyboard Shortcuts…**.

---

## 9. Resources & Links

### Downloads & Documentation

- **Download WaveformMatcher:**  
  [wtembundit.github.io/WaveformMatcher](https://wtembundit.github.io/WaveformMatcher/)

- **GitHub (Source Code):**  
  [github.com/wtembundit/WaveformMatcher](https://github.com/wtembundit/WaveformMatcher)

- **Changelog:**  
  [CHANGELOG.md](https://github.com/wtembundit/WaveformMatcher/blob/main/CHANGELOG.md)

### Related Tools

**Shot Notes X**  
macOS app for recording production metadata (Scene, Take, Camera, Lens, Frame Rate) and writing to Final Cut Pro clips
- **Download:** [App Store](https://apps.apple.com/app/shot-notes-x/id853468135)
- **Best For:** Users wanting automated workflow between set and edit suite

**FFmpeg / FFprobe**  
Tools for video and audio processing (used for reading timecode from raw files)
- **Website:** [ffmpeg.org](https://ffmpeg.org)
- **License:** LGPL 2.1+
- **Note:** WaveformMatcher can install ffprobe automatically when needed

### Support

**Report Issues / Request Features:**
- Create Issue on GitHub: [github.com/wtembundit/WaveformMatcher/issues](https://github.com/wtembundit/WaveformMatcher/issues)

**Contributing:**
- Fork repo → Create branch → Develop → Pull Request
- Read developer guide in README.md

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
   - Use Shot Notes X to log Scene/Take/Camera
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

**WaveformMatcher v1.4.5**
Built with assistance from Claude Code and Codex
[Report Issues](https://github.com/wtembundit/WaveformMatcher/issues) | [Download](https://wtembundit.github.io/WaveformMatcher/)
