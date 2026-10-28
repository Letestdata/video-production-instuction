---
name: news-video-16x9
description: Standard operating procedure and automated workflow for producing broadcast-quality 16:9 news investigative videos for News Fair. Use whenever the user asks to "make news video 16:9", "produce news video", "news video production", "16:9 news", "edit news video", or gives a news script/audio for full video assembly. Enforces zero media repetition, authentic Hindi Baloo typography, gapless verbatim Whisper acoustic subtitles, zero user video policy, and fast editorial pacing.
---

# News Video 16:9 Production Skill

This skill governs the complete end-to-end production of broadcast-standard **16:9 (1920×1080) investigative news videos** for **News Fair**.

---

## The 7 Mandatory Production Laws

1. **Absolute Zero Media & Motion Graphic Repetition**:
   - Every single visual cut in the timeline must be 100% unique.
   - Every editorial photo appears **strictly once** (verified via MD5 duplicate hash check).
   - Every bespoke motion graphic card appears **strictly once**.
   - If public video b-roll is used, every clip appears **strictly once**.

2. **Personal / User Media Prohibition (Zero-Video Rule When Mandated)**:
   - **Strict Ban on Creator's Personal Media**: Never use clips from the creator's personal studio/channel folders (`BBV news`, personal recordings, private footage).
   - **Zero-Video Mandate**: When the user requests "remove all video" or "no video", the timeline must contain **ZERO `.mp4` video files**. The visual layer is carried entirely by high-resolution editorial photos with active Ken Burns moves and bespoke motion graphic cards.

3. **Mandatory Devanagari Hindi Baloo Font**:
   - All text—headlines, statistics, labels, credits, and subtitles—must render in authentic **Devanagari Hindi Baloo** (`Baloo 2`).
   - Aliased in `fonts.css` via `@font-face` with base64 embedding to `'Baloo Bhai 2'`, `'Baloo Bhai'`, and `'Baloo 2'`.
   - Never allow fallback to generic sans-serif or non-Devanagari font families.

4. **Gapless Verbatim Whisper Acoustic Synchronization**:
   - Master audio is transcribed with `faster-whisper` using `vad_filter=False` to prevent Silero VAD from silently dropping speech chunks.
   - Scan for audio gaps > 1.2s across all segments; slice and transcribe any unaligned audio windows to guarantee 100% gapless acoustic coverage.
   - Map ground-truth script words to Whisper acoustic segment timestamps so that every subtitle cue matches spoken speech down to the exact millisecond.
   - **Subtitle format**: Centered bottom glass capsule, strictly 3–4 words per cue, spring pop entrance, with 1 keyword highlighted in radiant gold (`#FFD700`).

5. **Clean & Dignified Motion Graphics (Zero Sci-Fi Clutter)**:
   - **Strictly Prohibited**: Cyberpunk HUDs, spinning radar needles, military grids, and chaotic dials.
   - **Required Style**: Elegant dark obsidian news cards (`rgba(18, 2, 4, 0.94)`), subtle gold/red border trims (`#FFD700`), bold Hindi Baloo headlines, clean two-column comparison cards, and high-contrast horizontal progress bars (e.g. green 19% vs red 81%).
   - Must be immediately understandable at a glance in under 1 second.

6. **Fast Editorial Camera Motion & Pacing**:
   - **Still Photos**: Strictly 2.0s to 3.5s duration. Never hold a still image longer than 3.5s.
   - **Motion Graphics**: 5.0s to 7.5s (up to 9s for grand finale).
   - **Alternating Camera Moves**: No two consecutive photo cuts may share the same animation. Cycle across:
     - `zoom_in` (Scale 1.00 → 1.08)
     - `zoom_out` (Scale 1.08 → 1.00)
     - `pan_left` (TranslateX +30px → -30px)
     - `pan_right` (TranslateX -30px → +30px)
     - `diagonal_up` (TranslateX -20px → +20px, TranslateY +20px → -20px)
     - `fast_push` (Scale 1.00 → 1.12)

7. **Broadcast Canvas & Attribution Standards**:
   - Canvas: Full HD 1920×1080 at 30 FPS.
   - **Top-Left Bug**: Persistent News Fair logo + "News Fair" + "सच्ची पत्रकारिता" + pulsating live red recording dot.
   - **Top-Right Credit**: Strictly 2–3 words for editorial photos (`● CREDIT: PTI PHOTO`, `● CREDIT: SANSAD TV`). Zero credit on News Fair's own custom motion graphics.
   - **Documentary Evidence**: Images with text are only permitted for genuine primary sources (Gazette notifications, signed court/BCI orders, protest placards). Never use images with baked-in commercial TV news tickers.

---

## 6-Step Automated Production Workflow

### Step 1: Script & Audio Ingestion
- Place master audio at `production/<project-id>/audio/audio.wav` (and `demo.mp3`).
- Place the approved Hindi script at `demo scipt.txt`.
- Calculate exact total duration via `ffprobe` (e.g. 365.98s = 10,979 frames at 30 FPS).

### Step 2: Gapless Whisper Acoustic Capture
Run `fast_transcribe.py` using `faster-whisper`:
```python
from faster_whisper import WhisperModel
model = WhisperModel("base", device="cpu", compute_type="int8", cpu_threads=8)
segments, info = model.transcribe("audio.wav", language="hi", beam_size=1, vad_filter=False, word_timestamps=True)
```
- Audit gaps: Scan for any `gap > 1.2s` between consecutive segments.
- If any gap exists, slice the audio chunk with `ffmpeg -ss ... -to ...` and transcribe with `beam_size=5` to achieve 100% gapless acoustic continuity.

### Step 3: Verbatim 3–4 Word Cue Generation
- Split the ground-truth Hindi script into words.
- Anchor script word sequences to Whisper segment acoustic timestamps.
- Chunk words into strictly 3–4 words per cue.
- Highlight key news terms in gold (`#FFD700`).
- Export to `clean_cues.json`.

### Step 4: Shot Architecture & Zero-Repetition Media Curation
- Structure shots across the script's narrative Acts (e.g. Act 1: Hook, Act 2: Investigation & Stats, Act 3: Clash, Act 4: Fact Check & Finale).
- Sizing rule:
  - 20 bespoke motion graphics (~5.5s–7.0s each) = ~120s–130s.
  - ~75 unique editorial photos (~3.0s–3.2s each) = ~235s–245s.
  - Total == exact master audio duration down to 0.01s.
- Run MD5 duplicate audit to verify that every image hash is 100% unique.

### Step 5: Remotion Timeline Assembly
- Define composition in `reels-engine/src/ParliamentMonsoonSession16x9.tsx` (or `<ProjectName>16x9.tsx`).
- Register composition ID in `Root.tsx`.
- Wire `ShotRenderer` with all bespoke motion graphic components from `ParliamentMotionGraphics.tsx` and image Ken Burns handlers.
- Verify TypeScript compilation:
  ```bash
  npm --prefix reels-engine run build
  ```

### Step 6: Multi-Milestone Visual QA
Render sample still frames at diverse narrative milestones via `npx remotion still`:
- Frame 30 (01s): Intro overview card.
- Frame 1775 (~59s): CTA / Engagement card.
- Frame 2500 (~83s): Editorial photo with credit and verbatim caption.
- Frame 4200 (~140s): Data / Productivity progress bar card.
- Frame 5600 (~186s): Debate matrix / Political portrait.
- Frame 7650 (~255s): Fact-check card.
- Frame 10850 (~361s): Grand Finale ("सत्यमेव जयते। जय हिन्द।").

Inspect rendered PNG stills to verify:
1. Zero videos in timeline.
2. Authentic Hindi Baloo font active everywhere.
3. Subtitles verbatim match audio at that exact millisecond.
4. Zero repeated visuals.

---

## How to Edit This Skill

This skill is fully editable. You can modify it at any time:
1. **Direct File Edit**: Open and edit `SKILL.md` (or the global copy at `skills\news-video-16x9\SKILL.md`).
2. **In Chat**: Ask the assistant: *"Update the news-video-16x9 skill to add rule X"* or *"Change the image duration rule in news-video-16x9 to Y seconds"*.
3. Any changes made to the `SKILL.md` file take effect immediately for all subsequent tasks.

