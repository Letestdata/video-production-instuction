---
name: news-video-16x9
description: Standard operating procedure and automated workflow for producing broadcast-quality 16:9 news investigative videos for News Fair. Enforces zero media repetition, authentic Hindi Baloo typography, gapless verbatim Whisper acoustic subtitles, full-screen broadcast b-roll, structured PIP framing, continuous scrolling news ticker, lower-third data architecture, official brand logo, and broadcast motion graphics disciplines.
---

# News Video 16:9 Broadcast Production Skill

This skill governs the production of broadcast-quality 16:9 landscape (`1920×1080`) news investigative videos for **News Fair**, enforcing the technical rigor, visual pacing, audio synchronization, and motion graphics of television broadcast networks (CNN, BBC, NDTV, Aaj Tak).

---

## 1. Core Tool Stack & Command Execution

All 16:9 video productions execute across these foundational engines:

| Tool | System Location | Primary Role & Command |
| :--- | :--- | :--- |
| **Remotion** | `reels-engine/` (`@remotion/cli 4.0.538`) | Programmatic video timeline composition, 30 FPS rendering, audio muxing, and frame-accurate animation orchestration.<br>`npx remotion render src/index.ts <comp-id> out.mp4 --port=3055` |
| **FFmpeg** | System PATH (`ffmpeg 9.0.1`) | Lossless audio extraction, H.264 / AAC 48kHz transcode, stream encoding, and proxy generation. |
| **Whisper (whisper.cpp)** | System PATH (`whisper-cli.exe` v1.9.5) | **Mandatory Audio Master Synchronization Engine**. Word-level speech alignment (`clean_cues.json`, `.srt`) driving exact cut points for footage, graphics, and subtitles. |
| **yt-dlp** | System PATH (`yt-dlp 2026.10.26`) | Sourcing authentic broadcast B-roll footage from public news channels (Sansad TV, PIB, ANI, PTI). |

---

## 2. Quick-Reference Production Matrix

| Parameter | Broadcast Standard Specification |
| :--- | :--- |
| **Canvas Dimensions** | `1920 × 1080 px` (16:9 Landscape) @ 30 FPS |
| **Zero Media Repetition** | **Every Image, Video & Motion Graphic Shown Strictly ONCE**. Zero duplicate assets across the entire video. Validated by automated pipeline check (`len(sources) == len(set(sources))`). |
| **Still Image Duration** | Strictly **2.0 to 3.0 Seconds Max**. Holding a static photo longer than 3 seconds causes viewer drop-off. |
| **Video & Graphic Duration** | **3.5 to 6.5 Seconds** (As needed by script; **Strict Ban on 10–20 second dragged shots**). |
| **Camera Motion Variety** | Never repeat the same camera move consecutively. Cycle across: `zoom_in_center`, `pan_right_to_left`, `zoom_out_center`, `pan_left_to_right`, `diagonal_drift`, `fast_push`. |
| **Mixed-Media Rule** | **PIP Broadcast Monitor**: Portraits, leader face-offs, quotes.<br>**Full-Screen Edge-to-Edge**: High-energy B-roll, crowd rallies, parliamentary floor, drone establishing shots. |
| **Personal Media Ban** | **Strict Ban on User/Personal Media**. Sourced public broadcast footage (Sansad TV, ANI, PTI, PIB) or press archives only. |
| **Typography** | **Exclusively Hindi Baloo** (`Baloo 2` / `Baloo Bhai 2` Bold & ExtraBold via base64 embedded `fonts.css`). |
| **Captions / Subtitles** | Strictly **3 to 4 Words on Screen**, verbatim match to audio, centered bottom capsule, 1 gold highlight (`#FFD700`). |
| **Voiceover & Audio Mix** | Authoritative investigative delivery (`-1.0 dB` peak). BGM dynamically ducked to **`-18 dB to -22 dB`**. SFX at **`-6 dB to -10 dB`**. |
| **Top Area Cleanliness** | **Strict Ban on Top Sliver Banners & Roof Bars**. Top edge must remain open and breathable with only the top-left News Fair bug. |
| **Master Delivery Policy** | Direct master `.mp4` video export. **Do NOT create Premiere Pro (`.prproj`) or XML files** unless explicitly requested. |

---

## 3. Visual Footage & PIP Framing Standards

### 3.1 Non-Repetitive Camera Moves
Every still photo must feature active 2.5D camera motion. Never leave an image static:
1. `zoom_in_center`: Scale `1.00 → 1.08`.
2. `pan_right_to_left`: TranslateX `+40px → -40px` with scale `1.04`.
3. `zoom_out_center`: Scale `1.09 → 1.01`.
4. `pan_left_to_right`: TranslateX `-40px → +40px` with scale `1.04`.
5. `diagonal_drift`: TranslateX `-25px → +25px` and TranslateY `+20px → -20px`.
6. `fast_push`: Snap scale `1.00 → 1.12` with soft damping spring.

### 3.2 Subject Framing & Zero Head/Chin Cutoff
When displaying portraits or political figures in Picture-in-Picture (PIP) monitors:
- **Scale & Y-Position**: Never blindly apply `objectFit: cover`. Scale down (`imageZoom: 0.88 to 0.94`) and adjust vertical anchor (`objectPosition: center 18%` to `center 25%`) so hair, forehead, chin, gesturing hands, and microphones are fully visible.
- **Adaptive PIP Dimensions**: Adjust the monitor container to match the photo's natural aspect ratio (`620×540px` for square portraits; `960×520px` for landscape). Never stretch or crop facial features.

### 3.3 Media Cleanliness & Credit Attribution
- **No Baked-In Newsroom Text**: Never use photos with existing TV news tickers, watermarks, or third-party lower thirds. (Allowed exception: primary evidence like official gazette orders or signed court rulings).
- **Credit Badge**: Strictly 2–3 words in top-right corner: `● CREDIT: PTI PHOTO`, `● CREDIT: ANI NEWS`, `● CREDIT: SANSAD TV`. News Fair's own custom motion graphics carry **zero credit**.

---

## 4. Audio Architecture & Whisper Acoustic Synchronization

- **Master Audio Driver**: The voiceover audio track is the master conductor. Every visual cut, B-roll entrance, and motion graphic must synchronize to the exact millisecond timecode where the spoken concept begins.
- **Whisper Alignment**: Word-level acoustic alignment via `whisper-cli` or `process_cues.py` produces `clean_cues.json` and `.srt`. Visual cuts must snap to spoken word boundaries (`start` and `end`).
- **Subtitle Display Standard**:
  - Exactly 3 to 4 words visible at any given moment.
  - Positioned in a centered lower capsule (`Y: 82%`).
  - Active emphasis word highlighted in vibrant Amber Gold (`#FFD700`) with a subtle `scale: 1.05` spring pop.
- **4-Track Audio Stack**:
  1. *Track 1 (VO)*: Peak `-1.0 dB`, aggressively compressed, zero dead air.
  2. *Track 2 (BGM)*: Ducked dynamically to `-18 dB to -22 dB` beneath voiceover; instant silence drop on major revelations.
  3. *Track 3 (Tactile SFX)*: `-6 dB to -10 dB` (whooshes on cuts, paper rustles on documents, typewriter clicks).
  4. *Track 4 (Impact Hits)*: `-4 dB to -8 dB` (sub-bass drops, gavel strikes, metallic thuds). Sourced from `D:\Phone data\Sound Effects`.

---

## 5. Channel Branding & Visual Identity

- **Official Channel Bug**:
  - Located at top-left (`top: 26px, left: 40px`).
  - Features official transparent logo (`D:\News\Editing\News fair.png`), "News Fair", "सच्ची पत्रकारिता" in gold, and a pulsing red live beacon.
  - Continuous subtle shimmer/glare sweep every 10 seconds to maintain broadcast realism.
- **Color Architecture**:
  - Primary Maroon Crimson: `#7F0203`
  - Dark Obsidian Studio Void: `#060102` / `#0A0D14`
  - Accent Gold: Amber Gold `#FFD700`
  - Alert Red: `#FF1E27` / `#DC2626`
  - Cyan Intelligence Accent: `#00E5FF`
- **Top Area Cleanliness**:
  - Strict prohibition on full-width top roof bars, ticker slivers, or fake satellite status bands. The top canvas must remain open and uncluttered.

---

## 6. Broadcast Motion Graphics Architecture (The 3-Phase Lifecycle)

Never place a static graphic board or chart on screen. Every motion graphic component must execute through a strict 3-phase lifecycle:

1. **Phase 1: The Build-In (`0.0s – 1.0s` / Frames 0–30)**:
   - Header badge drops or snaps in (`translateY: -40px → 0px`).
   - Cards and containers slide in with spring physics (`damping: 12, stiffness: 140`).
   - Chart bars or meters physically grow from `0%` to their target values while counter tickers animate up simultaneously.
2. **Phase 2: The Active Idle (`1.0s – 4.0s` / Frames 30–120)**:
   - **Zero Freeze Policy**: Graphic must never sit completely still.
   - Continuous slow 2.5D push-in zoom (`100% → 105%`).
   - Continuous moving specular light sheen sliding across glass surfaces (`skewX(-25deg)`).
   - Subtle pulsing glow along card borders.
3. **Phase 3: The Rapid Exit (`4.0s – 5.0s` / Frames 120–150)**:
   - Graphic aggressively collapses inward (`scale: 1.0 → 0.85, opacity: 1 → 0`) or glitch swipes off-screen.
   - **Never Fade to Black**: Cuts immediately and directly into high-energy full-screen B-roll video.

---

## 7. The 7 Core Broadcast Motion Graphic Disciplines

### 7.1 Multi-Box Debate & Conflict Grids (2-Box / 3-Box)
- Encase contrasting political leaders or opposing viewpoints in rigid, sharp-edged frosted glass frames (`backdropFilter: blur(24px) saturate(170%)`).
- Border outlines color-coded to political party / faction (Saffron `#FF9933`, Green `#138808`, Blue `#000088`).
- Flashing live status badge on the top-left of each box (e.g. `🔴 LIVE: PATNA`).

### 7.2 Full-Screen Quote Boards (FSG)
- Used for explosive statements, whistleblower confessions, or court rulings.
- Deep studio void backdrop, large stylized quotation mark (`“`), the spoken statement in bold Baloo typography, and a speaker portrait cutout anchored to the bottom corner.
- Animated yellow felt-tip marker wipes left-to-right across the punchline, synced with marker squeak SFX.

### 7.3 Live Lower-Third Data Ticker & Anchored Docks
- Continuous horizontal news ticker ($1920 \times 84\text{ px}$) rendered in frosted glass with a specular top gold rim line.
- Continuous smooth ticker crawl displaying breaking updates, vote percentages, and verified bullet points.

### 7.4 AR Election Data Pillars & Comparison Charts
- 3D bar pillars or horizontal meters growing physically from `0%` to target percentages.
- Percentage figures count up in real-time (`lerp(0, target, progress)`).

### 7.5 Technical Mechanism Blueprints (`motion-blueprint`)
- Blueprint navy canvas (`#1453A8`) with CAD construction lines, rotating meshed gears, and dimension calipers (`Ø`, angles).
- Deployed when explaining complex mechanisms (EVM verification algorithms, financial laundering trails, legislative quorum procedures).

### 7.6 Mechanical Split-Flap Tally Boards (`motion-split-flap`)
- Airport departure-style split-flap board for constituency results, exit poll tallies, and party seat shifts.
- Character cells flip rapidly (55ms/flip) in a cascading wave accompanied by mechanical clicking Foley, settling on the final verdict (`LEAD`, `WIN`, `MAJORITY`).

### 7.7 Retro Surveillance Window (`motion-retro-vhs`)
- Stylized covert surveillance monitor for investigative sting tapes, leaked audio phone calls, and undercover operations.
- Features CRT scanlines, chromatic aberration color fringing, and monospaced OSD metadata (`REC ●`, `PLAY ▶`, running millisecond timecode).

---

## 8. Review Gate & Direct Master Render Policy

1. **Pre-Render Review Gate**:
   - Always render storyboard stills across key beats and inspect in HyperFrames studio before launching the full MP4 render.
2. **Direct Master MP4 Output**:
   - All projects render directly to finished, broadcast-ready master `.mp4` video files via Remotion and FFmpeg.
   - Do **NOT** generate Adobe Premiere Pro project files (`.prproj`) or XML interchange files (`.xml`) unless specifically requested by the user.
