---
name: news-video-16x9
description: Standard operating procedure and automated workflow for producing broadcast-quality 16:9 news investigative videos for News Fair. Mandatory five foundational engines (Remotion, HyperFrames, FFmpeg, Whisper/whisper.cpp audio master synchronization, yt-dlp). Enforces zero media repetition, authentic Hindi Baloo typography, gapless verbatim Whisper acoustic subtitles, zero user video policy, full-screen broadcast b-roll, structured PIP, continuous scrolling news ticker, lower-third data architecture, official brand logo, zero infographic tropes, and 7 core motion graphics standards (Network Bug & Live Clock, Stingers/Bumpers, Multi-Box Grids, Full-Screen Quote Boards, 3D Geospatial Maps, Top Sliver Banner, and AR Data Pillars).
---

# News Video 16:9 Production Skill

This skill governs the complete end-to-end production of broadcast-standard **16:9 (1920×1080) investigative news videos** for **News Fair**.

---

## 1. Core Tool Stack & Installation Specifications

In all video productions, the following five foundational engines are mandatory:

1. **Remotion**: [github.com/remotion-dev/remotion](https://github.com/remotion-dev/remotion)
   - **System Location**: `reels-engine/` (`@remotion/cli 4.0.538`)
   - **Command**: `npx remotion studio src/index.ts --port=3000` / `npx remotion render src/index.ts <composition-id> out.mp4`
   - **Role**: Programmatic video timeline composition, 60/30 FPS rendering, audio muxing, and frame-accurate animation orchestration.

2. **HyperFrames**: [github.com/heygen-com/hyperframes](https://github.com/heygen-com/hyperframes)
   - **System Location**: `production/democracy-questions/studio/` (`hyperframes@0.8.208`)
   - **Command**: `npx hyperframes preview --port=3002 --no-open`
   - **Role**: Real-time browser-based timeline preview, instant scrubbing, visual layout inspection, and visual QA before rendering.

3. **FFmpeg**: [github.com/FFmpeg/FFmpeg](https://github.com/FFmpeg/FFmpeg)
   - **System Location**: System PATH (`ffmpeg version 9.0.1-full_build-www.gyan.dev`)
   - **Command**: `ffmpeg -i input.mp4 ...`
   - **Role**: Lossless audio extraction, H.264/AAC transcode, video trimming, downsampling, and proxy generation.

4. **Whisper (whisper.cpp)**: [github.com/ggml-org/whisper.cpp](https://github.com/ggml-org/whisper.cpp)
   - **System Location**: System PATH (`whisper-cli.exe` v1.9.5 build 5454 + `openai-whisper` Python 3.11)
   - **Command**: `whisper-cli.exe -m <model.bin> -f audio.wav -oj` or `python process_cues.py`
   - **Role**: **MANDATORY Audio Master Synchronization Engine**. Millisecond-precision speech recognition, word-level audio alignment, automatic subtitle cue extraction (`clean_cues.json`, `.srt`), AND orchestrating the exact timecode cuts for all B-roll footage, videos, images, and bespoke motion graphics to match the audio.

5. **yt-dlp**: [github.com/yt-dlp/yt-dlp](https://github.com/yt-dlp/yt-dlp)
   - **System Location**: System PATH (`yt-dlp 2026.10.26`)
   - **Command**: `yt-dlp -f "bestvideo[height<=1080]+bestaudio/best" <URL>`
   - **Role**: Downloading authentic press conference footage, parliamentary debates, and internet b-roll clips.

---

## 2. The Mandatory Broadcast Production Laws

1. **The Strict "One-Time Use" Rule (Absolute Zero Asset Repetition)**:
   - Every single visual asset in the timeline—whether an editorial photo, b-roll plate, politician portrait, or evidence document—must appear **strictly once**.
   - **Zero Duplicate Hash/File Reuse**: Never reuse the same image file or video clip across different scenes or within the same scene.
   - If a political leader (e.g. Mangani Lal Mandal, Lalu Prasad Yadav) is mentioned at multiple points in the script, you **must source a different unique photograph or video angle** for each distinct appearance.
   - If a mechanism (e.g. EVM, ballot box, counting hall, voting queue) is referenced across multiple scenes, you **must use a distinct unique asset** (e.g. EVM button press vs EVM testing vs EVM distribution vs ballot box stamping vs voters outside gate).

2. **Mandatory Official News Fair Logo Integration**:
   - **Official Logo Assets**: Strictly use the official brand logos located at:
     - `reels-engine/public/brand/news_fair_official_transparent.png` (for top-left broadcast channel bug: white TV antenna frame, News Fair typography, and globe mark with clean alpha).
     - `reels-engine/public/brand/news_fair_official_logo.png` (the full 2000×2000 crimson brand plate from `News fair.png` for master station cards and outros).
   - **Top-Left Channel Bug Standard**:
     - Docked at `top: 26px`, `left: 40px`, `zIndex: 10000`.
     - Solid crimson broadcast plate (`linear-gradient(135deg, rgba(127, 2, 3, 0.96) 0%, rgba(60, 1, 2, 0.98) 100%)`) with `2px solid #FFD700` gold border and sharp rectangular corners (`borderRadius: 6px`).
     - Display the official transparent TV mark at height `52px` (ensuring the internal "News Fair" text and globe are sharp and legible), paired with a pulsing `🔴 LIVE` badge and `सच्ची पत्रकारिता` tagline in gold.
   - Never use placeholder text boxes, generic letters ("NF"), or emoji placeholders for the News Fair logo.

3. **Consistent Broadcast Monitor PIP Framing**:
   - Every inserted photo, evidence plate, and leader portrait must be displayed inside a standardized **Broadcast Monitor Frame**:
     - **Unified Center Stage Monitor** (`960px × 520px`): Centered in the upper 75% of the screen.
     - **Duel Split Screen Monitors** (`580px × 380px` each): Used exclusively when comparing two opposing leaders (e.g. Lalu vs Rahul).
     - **Frame Engineering**: Metallic chamfered borders (`3.5px solid #FFD700` or `#E50914` or `#007BFF`), ambient studio glow, top live feed header strap (`🔴 LOCATION // TOPIC` + `● FEED ACTIVE`), CRT TV scanline texture, and a bottom caption strap.
     - Never mix unbordered raw cutouts with bordered boxes. Stick strictly to this standardized broadcast framing architecture.

4. **Enlarged & Animated Continuous Scrolling News Ticker**:
   - **Prominent Dimensions**: Height must be **58px to 64px** at the bottom edge (`bottom: 0px`).
   - **Continuous Smooth Scroll**: Text must crawl continuously from right to left across all frames without jumping, freezing, or stuttering.
   - **Pulsing Live Badge**: Fixed on the left (`width: ~210px`), featuring a bright pulsing gradient (`#FF1E27` to `#B71C1C`) with yellow accent dot: `⚡ LIVE TICKER` / `ताज़ा अपडेट`.

5. **Docked Lower Third (L3) Architecture (Sharp-Edged, Bottom-Left, Zero Emojis)**:
   - All text, metrics, and seat counts belong strictly in the **Lower Third strap** docked directly above the ticker (`bottom: 62px` to `170px`).
   - **Zero Emojis**: Absolute strict ban on all emojis (`💔`, `🤝`, `🚨`, `📉`, `📊`, `⚠️`, `🔥`, `🗳️`, `❌`, `🎙️`, `⚖️`, `🔒`, `🛡️`, `⏰`, `💥`, `⚡`) in Lower Third headlines, tags, subtext, and ticker. Use clean, authoritative Devanagari/English text only.
   - **Docked at Bottom-Left**: Docked at `left: 54px`, with sharp rectangular edges (`borderRadius: 4px`) and `maxWidth: 1280px` (leaving the right screen area open like CNN/NDTV broadcast standards).
   - **Zero Center Badges**: Never place floating tally cards or central statistic boxes in the middle of the screen.
   - **Category Chip**: Solid red or blue category chip (`BREAKING NEWS`, `बड़ी खबर`, `चुनाव नतीजे`, `विशेष बयान`, `सियासी संग्राम`, `गठबंधन में दरार`) with subtle pulse animation and gold right border.

6. **Acoustic Whisper Subtitle Architecture & Spell-Check Mandate**:
   - Docked cleanly directly above the Lower Third (`bottom: 174px` to `178px`).
   - Verbatim Hindi Devanagari text in authentic **Baloo Bhai 2** font, strictly 3–4 words per cue.
   - **Mandatory Alignment & Spell-Check Against Official Script**: Whisper raw transcription often introduces phonetic misspellings, merged words (e.g. `शामिल्दलोंने`), or truncated phrases (e.g. `बन्धन में`). All subtitle cues MUST be rigorously aligned and sanitized against the authentic script text (`script.txt`) to guarantee 100% accurate Hindi spelling, proper spacing between words, and correct grammar.

7. **Elimination of Infographic & Explainer Tropes (Journalism, Not Cartoons)**:
   - **NO Boomerangs**: Use authentic editorial footage of tense political rallies or press confrontations with sharp L3 headlines.
   - **NO Padlocks**: Use gritty real-world footage of chained and padlocked iron gates at polling booths and voters waiting outside.
   - **NO Scales of Justice or Red ❌ Overlays**: Use real-world election counting centers, EVM testing, and authentic news evidence.

8. **Personal / User Media Prohibition (Zero-Video Rule When Mandated)**:
   - Strictly prohibit personal recordings or private computer files from the creator's computer. Use only verified, internet-sourced public domain and editorial news archives.

9. **The Dynamic Abstract Background Law (Never Static / No Slideshows)**:
   - The background must **never be static or dead**—even when avoiding a busy live newsroom, it must maintain constant, slow cinematic motion:
     - **Continuously Drifting Mesh Gradient**: Radial light orbs slowly undulating across coordinates (`radial-gradient` with sine/cosine coordinates).
     - **Subtle Rotating/Drifting Faint Map**: A huge, very faint (5%–8% opacity) map of Bihar/India or abstract globe rotating slowly and breathing in the background.
     - **Continuous Background Zoom**: Slow camera push on the entire canvas (100% to 106% over the video).
     - **Oblique Moving Tech Grid**: Subtle digital grid scrolling diagonally so the background never feels like a flat slide.

10. **Strict Layering & PIP Framing Architecture**:
    - **Absolute Top-Layer Rule for Lower Third (L3)**: The Lower Third text strap must ALWAYS be the topmost layer (`zIndex: 9999`). It must **never** be obscured, covered, or clipped by images, video clips, or monitor frames.
    - **Structured Framing (No Floating Assets)**: Every photo of a politician (Lalu Yadav, Mangani Lal, etc.) or evidence document must be enclosed inside a structured **Broadcast Monitor Frame** with metallic borders, top live feed header, and bottom caption strap. Never let portraits float loosely in dark space.
    - If full-screen footage is used, it fills the canvas edge-to-edge with the Lower Third cleanly docked on top.

11. **Continuous Ken Burns Motion on Every Single Asset (5% to 10% Scale)**:
    - Every image, video clip, and photo inside monitors or full-screen plates must have an active Ken Burns zoom-in or zoom-out (minimum 5% to 10% scale change, e.g. 1.00 to 1.08) over its display duration.
    - Visual assets must never freeze or appear as completely motionless stills.

12. **Real Footage / B-Roll Exclusively (Zero Explainer Infographics)**:
    - Real news broadcasts use authentic B-roll (real-world footage and photojournalism), **not explainer infographic motion graphics or cartoon icons**:
      - Real EVM machines being handled by officials instead of glowing EVM vector icons.
      - Real counting halls or historical archival documents instead of scales of justice.
      - Real padlocked iron gates and voter queues instead of graphic padlock drops.
      - Real street protests with party flags instead of animated boomerangs.

13. **The Portrait & Transparent Media Rule (Zero-Cropping for 1:1, 9:16, & Cutouts)**:
    - **Never Crop Portrait or Transparent Media**: If an asset is in **portrait orientation** (1:1 square ratio, 4:5, 3:4, or 9:16 vertical ratio), or if it is a **transparent PNG cutout** (politician cutouts, transparent party symbols, badges, or vertical documents):
      - **DO NOT CROP**: Never apply `objectFit: "cover"` or aggressive cropping that cuts off heads, foreheads, chins, shoulders, or graphic borders.
      - **Full Display Mode (`objectFit: "contain"`)**: The image must be displayed **fully and completely** without any clipping.
      - **Studio Framing & Ambient Backdrop**: When a 1:1, 9:16, or transparent portrait is framed inside a 16:9 viewport or broadcast monitor:
        - Set `objectFit: "contain"`, `objectPosition: "center center"`.
        - Render a complementary darkened/blurred ambient layer behind it (`objectFit: "cover"`, `filter: "blur(28px) brightness(0.28)"`) or an authentic dark news gradient, eliminating blank white borders while preserving 100% of the subject.
        - For transparent PNG cutouts: Render centered at natural full height or proper scale, never clipping edges.

14. **Human-in-the-Loop Review Gate ("Show Me First Before Render")**:
    - When requested ("before render show me first"), **render sample still frames first** and present them to the user for visual verification. Only initiate the full video render upon approval.

15. **Politician Name Plate & Layering Mandate (Z-Index Bring-to-Front & Zero Face Covering)**:
    - **Bring to Front (Strict Z-Index Layering)**: Text layers containing politicians' or speakers' names (e.g. Lalu Prasad Yadav, Rahul Gandhi) must ALWAYS be assigned a z-index (e.g. `zIndex: 100`) strictly **above** portrait image tracks and video clips. Names must **never** be placed beneath or obscured by portrait image layers.
    - **Solid High-Contrast Name Plate**: Never use transparent or faint gradients that get washed out or hidden by white clothing, shirts, or backgrounds. Always insert a dedicated, solid dark Name Plate bar (`background: linear-gradient(90deg, #0e0204 0%, #1e0307 60%, #0e0204 100%)`) with a top accent border line (`2px solid <borderColor>`) separating the footage from the typography.
    - **Fix Cropping & Face Clearance**: The portrait image must be positioned and scaled to sit comfortably in the viewport **above** the Name Plate (`flex: 1` viewport + docked name plate tier). The Name Plate must never cover the politician's chin, neck, or face, and the portrait must never obscure the text.

---

## 3. Advanced Broadcast Motion Graphics Architecture & Engineering

To achieve top-tier television network broadcast standards (matching CNN, BBC, Aaj Tak, NDTV), all video productions must incorporate the following seven foundational motion graphics disciplines:

1. **The Bug (Network Logo & Live Clock)**:
   - A persistent, small graphic anchored strictly to the top right or bottom right (or top-left for master channel identifier).
   - **Continuous Motion**: In a true news theme, this is never a static image; it features a slow continuous rotation or a sweeping light-glare sweep effect every 10 seconds.
   - **Live Clock Urgency**: Integrating a ticking digital clock (e.g., `10:42:15 IST` / `LIVE`) right beside it instantly enforces authentic "live broadcast" urgency and breaking news authority.

2. **Stingers and Bumpers**:
   - High-energy, 2-to-3-second full-screen animations featuring 3D channel logos, sweeping anamorphic light flares, and heavy "whoosh" or metallic sound effects.
   - **Segment Segmentation**: Deploy these strictly to break up distinct segments, transition into a major new topic, or introduce a "Breaking News" alert, ensuring a hard, professional cut rather than an amateurish soft crossfade.

3. **Multi-Box / Split-Screen Grids**:
   - When comparing two or three figures or depicting political conflict, **never float their photos in empty space**.
   - **Rigid Sharp-Edged Grids**: Lock them into a rigid, sharp-edged 2-box or 3-box grid.
   - **Metallic Borders & Live Status Badges**: Each box must have a distinct metallic or glowing border (e.g., green for RJD, blue for Congress, saffron for BJP), topped with a small, contrasting badge indicating location or status (e.g., a flashing red `🔴 LIVE: PATNA` or `🔴 LIVE: NEW DELHI` feed tag).

4. **Full-Screen Quote Boards (FSG)**:
   - When highlighting a critical statement, explosive revelation, or controversial quote, cut away from the video entirely to a dedicated **Full-Screen Graphic (FSG)**.
   - **Graphic Composition**: Features a deep, looping dark studio background, a massive stylized quotation mark (`“`), the exact spoken or written statement in a bold, highly readable Devanagari/Latin font, and a high-quality cutout of the speaker anchored securely to the bottom corner.

5. **3D Geospatial Locator Maps**:
   - To establish a location, geographic context, or electoral constituency, replace flat 2D vector maps with 3D satellite imagery or 3D terrain that slowly and continuously zooms into a specific district or polling station.
   - **3D Drop Pin & Animated Tag**: Add a glowing, dropping 3D pin and a sharp, animated text tag (e.g., `📍 PATNA // CONSTITUENCY #4`) to give the segment a high-budget, investigative documentary feel.

6. **The Top "Sliver" Banner**:
   - A very thin, solid-color bar running across the absolute top edge of the screen (`height: 32px to 40px`), serving as an architectural "roof" for your broadcast.
   - **Overarching Framing**: It remains persistently on screen to frame the overarching context of the broadcast (e.g., `🔴 ELECTION 2026: COUNTING DAY` or `MEGA COVERAGE // SPECIAL REPORT`), perfectly balancing the heavy L-bands, Lower Thirds, and running tickers docked at the bottom.

7. **Augmented Reality (AR) Data Pillars**:
   - For top-tier data visualization (vote shares, seats won, comparison statistics), instead of flat boxes popping up, use **3D bar charts or data pillars** that appear to physically grow out of the floor of the news studio or street-level B-roll footage.
   - **Camera Pan & Orbit**: The camera slightly pans or orbits around them, adding depth, cast shadows, and spatial realism to raw numbers.

---

## How to Edit This Skill

This skill is fully editable. You can modify it at any time:
1. **Direct File Edit**: Open and edit `d:\News\Clude news ai\.agents\skills\news-video-16x9\SKILL.md` (or global copy at `C:\Users\ahmad\.gemini\antigravity\skills\news-video-16x9\SKILL.md`).
2. **In Chat**: Ask the assistant: *"Update the news-video-16x9 skill to add rule X"*.
3. Any changes made to the `SKILL.md` file take effect immediately for all subsequent tasks.
