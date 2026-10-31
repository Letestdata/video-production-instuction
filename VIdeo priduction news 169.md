---
name: news-video-16x9
description: Standard operating procedure and automated workflow for producing broadcast-quality 16:9 news investigative videos for News Fair. Mandatory five foundational engines (Remotion, HyperFrames, FFmpeg, Whisper/whisper.cpp audio master synchronization, yt-dlp). Enforces zero media repetition, authentic Hindi Baloo typography, gapless verbatim Whisper acoustic subtitles, zero user video policy, full-screen broadcast b-roll, structured PIP, continuous scrolling news ticker, lower-third data architecture, official brand logo, zero infographic tropes, 7 core motion graphics standards, and all 32 broadcast production laws.
---

# News Video 16:9 Production Skill

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

## 2. Quick-Reference Cheat Sheet ("Small Information")

| Parameter | Mandatory Rule | Implementation Requirement |
| :--- | :--- | :--- |
| **Video Ratio** | **16:9 Landscape (1920×1080)** | Full HD broadcast canvas at 30 FPS or 60 FPS. |
| **Zero Media & Motion Graphic Repetition Law** | **Every Image, Video & Motion Graphic Shown ONLY ONCE** | **Absolute Zero-Repetition Mandate Across All Visuals**: Every single video clip, every editorial photo, AND every bespoke motion graphic component must appear **strictly once** across the entire video. Zero repeated videos, zero repeated photos, and zero repeated motion graphics. Every visual cut in the timeline must be 100% unique. |
| **Image Cut Pacing** | **Strictly 2.0 to 3.5 Seconds Max** | Still photos must only appear for 2.0 to 3.5 seconds max. Never hold a still image longer than 3.5 seconds. |
| **Video & Motion Graphics Duration** | **As Long as Needed by Script (Strictly Under 10s)** | Video b-roll and motion graphics can be used as long as needed according to the script beat/sentence (typically 3.5s – 6.5s). **STRICT BAN on 10–20 second long video/motion graphic shots** to prevent dragging. |
| **Image Motion Variety** | **Never repeat the same animation** | Cycle across `zoom_in`, `zoom_out`, `pan_left`, `pan_right`, `diagonal_drift`, `fast_push`. |
| **Footage Mix** | **Compulsory Videos + Images** | Mix authentic web videos (b-roll/press clips) with clean editorial photos. |
| **Motion Graphics Style** | **Clean, Simple & Broadcast-Elegant (Zero Sci-Fi Clutter)** | **Strict Ban on Over-Complex Sci-Fi HUDs**: No spinning radar needles, no cybernetic background grids, no military/GPS coordinates, no chaotic dials. Every motion graphic must be **simple, dignified, clean, and immediately understandable in 1 second**: elegant dark obsidian cards (`rgba(18, 2, 4, 0.94)`), sleek gold/red border trims, bold Hindi Baloo typography, and clean horizontal progress bars or two-column comparison cards with smooth spring slide-up. |
| **Motion Graphic Understandability** | **Instant 1-Second Visual Comprehension** | Must be immediately understandable at a glance without reading small text: bold headlines, clear colored bars (e.g. green 19% vs red 81%), and big punchy takeaways in authentic Baloo Bold. |
| **Motion Graphic Design** | **Bespoke per Script** | Never reuse the same generic template. Build unique visuals tailored to the specific story. |
| **Captions Length** | **Strictly 3 to 4 Words on Screen** | Exactly 3–4 words spoken verbatim in sync with audio. Never full lines or summaries. |
| **Verbatim Audio Captions** | **Exact Spoken Words (Zero Misspellings)** | On-screen text must accurately show what the audio says verbatim, aligned to Whisper acoustic timestamps. Never show misheard phonetic approximations or unaligned text. |
| **Captions Style** | **Motion-Director Spring Pop** | Apple-grade spring physics, centered bottom capsule, 1 gold highlighted emphasis word. |
| **Voiceover** | **Abhisar Sharma Clone Voice** | Authoritative, energetic, investigative tone with dramatic inflection. |
| **Typography** | **EXCLUSIVELY Hindi Baloo (Baloo Bhai / Baloo 2)** | **Mandatory Hindi Baloo Font**: Use the authentic Devanagari Hindi Baloo typeface. In Google Fonts, the Devanagari Hindi font is `Baloo 2` (while `Baloo Bhai 2` is Gujarati). In code, `@font-face` must alias `'Baloo Bhai 2'` and `'Baloo Bhai'` to `Baloo2-Bold.ttf` and `Baloo2-ExtraBold.ttf` with base64 embedding (`fonts.css`), ensuring Chromium 100% renders thick, rounded, authentic Hindi Baloo letters. |
| **Channel Logo** | `D:\News\Editing\News fair.png` | Top-left glass pill bug with logo, "News Fair", "सच्ची पत्रकारिता", and pulsating live red dot. |
| **Editorial Photo Credit** | **Strictly 2 to 3 Words** | Top-right badge: `● CREDIT: PTI PHOTO`, `● CREDIT: ANI NEWS`, `● CREDIT: SANSAD TV`. |
| **Channel Graphics Credit** | **ZERO Credit** | Do not put credit badges on News Fair's own custom motion graphics. |
| **AI Images** | **No Credit by Default** | If credit is necessary, strictly label as: `"AI generated image"` (2-3 words). |
| **Images With Text** | **Prohibited except real documents** | Never use photos with baked-in TV news tickers. Only use text images for genuine gazettes, court orders, or posters. |
| **Personal Media Ban** | **Strict Ban on Creator / User Video** | **Absolute Ban on User's Personal Channel Videos**: Never touch or include files from the creator's personal video folders (e.g. `d:/News/videos/`, `BBV news`, personal studio recordings, or private footage). All footage must be authentic public broadcast b-roll (Sansad TV, ANI, PTI) or official press feeds. |
| **Audio Master Sync (Whisper)** | **MANDATORY Whisper Alignment with Full Acoustic Capture** | Word-level speech alignment using Whisper is compulsory. VAD filter must not discard speech chunks. Full acoustic word alignment with greedy decoding captures 100% spoken text across all acts, guaranteeing that captions and visual cuts precisely lock to the audio waveform without any timing drift or missing sections (`clean_cues.json` & `.srt`). |
| **Audio-Driven Visual Matching** | **100% Matched to Voiceover Content** | Audio is the master director. Every single B-roll video clip, editorial photograph, and bespoke motion graphic must be generated, selected, and timed to directly match the spoken words and themes in the audio at that exact second. |
| **Motion Graphic Audio Sync** | **Strictly According to Audio** | Every motion graphic must be created and animated to directly reflect the spoken voiceover at that second. |
| **Approval Gate** | **Storyboard & Studio First** | Always present storyboard stills and live studio previews before rendering final MP4. |

---

## 3. Visual Motion & Footage Rules

### A. Non-Repetitive Image Camera Motions
Static images make viewers lose interest. Every still photo must have active, cinematic camera movement. **Crucially: No two consecutive cuts may use the same camera move.**

The animation cycle must alternate across:
1. `zoom_in_center`: Scale 1.00 → 1.08 over cut duration.
2. `pan_right_to_left`: TranslateX +40px → -40px with subtle scale 1.04.
3. `zoom_out_center`: Scale 1.09 → 1.01 over cut duration.
4. `pan_left_to_right`: TranslateX -40px → +40px with subtle scale 1.04.
5. `diagonal_drift_up`: TranslateX -25px → +25px and TranslateY +20px → -20px.
6. `fast_punch_in`: Snap scale 1.00 → 1.12 with soft damping spring.

### B. Compulsory Real Internet Videos + High-Res Editorial Photos
- Videos cannot consist only of photo slideshows. Interleave **real video b-roll from the internet** (press conferences, parliamentary walkouts, street protests, court steps) with high-resolution editorial photos.
- Use `yt-dlp` to download source footage directly from official feeds (Sansad TV, PIB, ANI, PTI).

### C. Clean Media Only — "No Baked-In Newsroom Text"
- **Strictly Prohibited**: Never use photos/screenshots with existing TV news tickers, lower-third news straps, channel watermarks, or "Breaking News" graphic ribbons.
- **Allowed Exception**: Text-bearing images are permitted **only** when the text itself is primary documentary evidence required by the script:
  - Official Gazette notifications
  - Signed Bar Council of India (BCI) orders
  - Supreme Court / High Court certified orders
  - Parliamentary Privilege Motion notices
  - Student protest placards and handwritten banners
  - Historical archival posters

### D. AI Image Attribution Policy
- AI generated images used as conceptual b-roll do **not** carry credit by default.
- If credit is necessary or legally advised, format it strictly as:
  ```
  ● CREDIT: AI GENERATED IMAGE
  ```
  (2–3 words max, standard top-right pill badge).

### E. Absolute Ban on User's Personal Media ("Do Not Use My Video and Image")
- **Strict Prohibition**: Under no circumstances may video production use the user's or creator's personal videos, private photos, webcam recordings, personal phone clips, or private local media.
- **Compulsory Internet & Broadcast Sourcing**: All video b-roll and still photography must be sourced exclusively from authentic public internet channels:
  1. **Broadcast Video B-Roll**: Downloaded via `yt-dlp` from official public broadcast feeds (Sansad TV, ANI News, PTI, Press Information Bureau (PIB), Press Pool, DD News).
  2. **Editorial Press Photography**: High-resolution documentary photos from credible press agencies (The Hindu, Indian Express, PTI, ANI archives).
  3. **Documentary Primary Evidence**: Certified gazettes, signed Bar Council / Court orders, or genuine student protest placards.
  4. **Script-Specific AI Conceptual Imagery**: Generated clean without text, uncredited or labeled `● CREDIT: AI GENERATED IMAGE`.

### G. Zero Media Repetition Law (Compulsory Unique Media Asset per Cut)
- **Absolute Prohibition on Repetition**: It is strictly forbidden to show the same video clip or the same editorial photograph more than once in any video production. Every cut must introduce a brand new, visually distinct asset.
- **Audience Fatigue Prevention**: Repeating footage makes an investigative report look lazy and repetitive. If a video runs 6 minutes and requires 75 cuts:
  1. Every single video clip must be from a distinct moment or source (press pool, chamber proceedings, rally footage, news desk).
  2. Every single editorial photograph must be unique (distinct camera angles, distinct events, distinct archival records).
  3. Bespoke motion graphics must transition through unique states, tabs, and data displays (never freezing on or looping the exact same graphic).
- **Enforcement in Production Pipelines**: Automated asset validator scripts must verify `len(used_sources) == len(set(used_sources))` for all `image` and `video` cuts in `PARLIAMENT_SHOTS`. Any duplicate `src` filename will immediately fail the production build.

### F. Shot Duration Rules: Images (2–3s) vs. Video & Motion Graphics (Script-Driven, < 10s)
1. **Still Images (Strictly 2.0 to 3.0 Seconds Max)**:
   - Photographs, newspaper scans, and document crops must strictly remain on screen for **2.0 to 3.0 seconds max**.
   - Holding a static still photograph longer than 3 seconds causes viewers to lose visual interest.
   - Every still photo must feature a distinct, non-repeating dynamic camera animation (`zoom_in`, `zoom_out`, `pan_left`, `pan_right`, `diagonal_up`, `fast_push`).

2. **Video B-Roll & Motion Graphics (As Long as Needed According to Script)**:
   - Video clips and bespoke motion graphics carry rich temporal, narrative, and motion information.
   - They must **not** be artificially or arbitrarily cut short at 2.0–2.5 seconds if the visual demonstration, voiceover sentence, or dialogue beat requires more time.
   - Let motion graphics run for their full semantic journey (e.g. 3.5s to 6.5s) to let split-flap departures reveal titles, timeline lasers sweep across historical nodes, or 3D books rotate with lighting sheens.
   - Let authentic video clips run long enough to establish genuine newsroom or parliamentary atmosphere (typically 3.5s to 5.5s).

3. **Strict Ban on 10–20 Second Long Shots (Zero Monotony / No Dragging)**:
   - **Absolute Prohibition**: Never let a single continuous video clip or motion graphic run for **10 to 20 seconds long**.
   - Shots of 10–20 seconds drag down video pacing and make investigative news content feel unedited and lethargic.
   - If an investigative thought or argument spans 10+ seconds in the script, split it into dynamic complementary cuts by alternating between bespoke motion graphics, authentic video b-roll, and snappy 2–3s editorial photographs.

---

### H. Subject Framing, Scale & Y-Positioning Mandate (Zero Head/Chin Cutoff & Adaptive PIP Dimensions)
1. **Adjust Scale and Vertical (Y) Positioning**:
   - Whenever framing a subject or political leader inside a PIP monitor (e.g., Prashant Kishor, Lalu Prasad Yadav), never blindly apply top-aligned `objectFit: "cover"`.
   - **Scale Down / Zoom Out**: Decrease the scale (`imageZoom: 0.88 to 0.94`) until the entire subject (head, hair, face, gesturing hands, chest, and microphone) is completely visible within the PIP frame.
   - **Adjust Y-Position / Object-Position**: Adjust the vertical Y-position (`objectPosition: "center 18%"` to `"center 25%"` or `imageOffsetY`) to center the subject vertically so their forehead is not cropped at the top, and their mouth, chin, beard, and chest are not covered or clipped by the bottom name plate.
2. **Adaptive PIP Framing Strategy (Dynamic Aspect Ratios)**:
   - Do not force a standard 16:9 landscape box (`960×520`) on every image.
   - If scaling the image down leaves empty space or if the source image is square (`1:1`) or portrait (`4:5`, `3:4`), **adjust the dimensions of the PIP box itself to match the source aspect ratio**:
     - For 1:1 square or 0.9–1.1:1 images (e.g., Prashant Kishor, Lalu expressive): Use a tailored monitor (`width: 620px to 720px`, `height: 540px`).
     - This displays the full subject naturally without extreme zoom-in cropping, while leaving the dynamic background (wireframe globe and studio lighting) visible on the flanks, creating a superior broadcast composition.
     - If a standard 16:9 frame must be retained, use a `"contain"` setting with a blurred ambient background, always ensuring the focal point (the subject's face) remains centered.

---

## 4. Script-Tailored Motion Graphics (Simple, Clean & Broadcast-Elegant)

### A. Simplicity Mandate — Ban on Over-Complex Sci-Fi HUDs
- **News Broadcasting Reality**: Viewers are watching an investigative news report, not a science-fiction video game or fighter jet simulation. Complex telemetry grids, 360° rotating radar sweeps, scrolling coordinate matrices (`77.2090° E // 28.6139° N`), and multi-dial gauges distract and confuse viewers.
- **Strictly Prohibited**:
  1. Spinning radar circles, radar sweep cones, and sweeping needles.
  2. Scrolling cybernetic grid meshes and laser scan crosshairs.
  3. Faux-military coordinate readouts, telemetry timestamps, and sci-fi tech borders.
  4. Flashing emergency hazard stripes and rapid blinking alarms.
- **Mandatory News Standard**:
  1. **Clean News Containers**: Sleek dark obsidian glass (`rgba(18, 2, 4, 0.94)`), thin 1.5–2px News Fair Gold (`#FFD700`) or Alert Red border, smooth rounded corners (24–28px), and subtle golden drop shadow.
  2. **Smooth & Simple Spring Animation**: A clean, single spring slide-up (`spring({ frame, fps, config: { damping: 14, stiffness: 140 } })`) with gentle settle.
  3. **High-Contrast Big Typography**: Extra-bold headlines (56px–66px) in authentic Hindi Baloo font.
  4. **Simple Structural Layouts**:
     - **Session Overview**: Category tag, main bold headline, and 3 clean side-by-side metric cards.
     - **Productivity Audit**: 3 clean horizontal progress bars (e.g. Lok Sabha 19% green vs 81% red; Rajya Sabha 39% gold vs 61% red; Question Hour <1% red).
     - **Debate Clash Matrix**: Clean two-column card contrasting Government Claims vs. Opposition Allegations.
     - **Historical Sittings**: 2 clean comparative boxes (1960–70s vs. today).
     - **Constitutional Climax**: 3 clean core questions and the signature *"सत्यमेव जयते • जय हिन्द"* takeaway.

### B. Dynamic Yet Dignified Motion
Every graphic remains active without visual noise:
- Smooth entry with physical spring settling.
- Numbers and progress bars count up cleanly from 0 to their target over 30–50 frames.
- Gentle, subtle breathing on badges or glows (`Math.sin(frame / 6) * 0.15`).
- Zero static PowerPoint-style text: elements feel alive, elegant, and broadcast-ready.

---

## 5. Whisper Audio Synchronization & Audio-Driven Visual Orchestration

### A. Whisper as the Mandatory Master Clock Engine
- **Compulsory Whisper Alignment**: In every video production, the voiceover audio track (`audio.wav`) must first be processed through **Whisper** (`whisper.cpp` / `openai-whisper`) to extract word-level timestamps (`clean_cues.json`, `.srt`).
- **Master Timecode Backbone**: Whisper is not only for subtitles; its millisecond-accurate timecodes dictate:
  1. The total duration of the master video timeline (e.g., 62.38s = 1871 frames at 30 FPS).
  2. The exact start and end boundaries for every visual shot cut.
  3. The trigger points for motion graphic animations (laser sweeps, stamps, node glows).

### B. Audio-Driven B-Roll Footage & Video Synchronization
- **No Random Video Filler**: B-roll video footage downloaded from the internet (via `yt-dlp`) must be selected and timed to match the **exact spoken words** in the audio at that moment:
  - When the voiceover mentions a press conference or statement, cut to authentic press briefing footage (`politics_press_briefing.mp4` / `sonia_aicc_press_clean.mp4`).
  - When the voiceover mentions parliamentary debates, laws, or proceedings, cut to Sansad TV floor footage (`politics_parliament_wide.mp4` / `sonia_parliament_speech_clean.mp4`).
  - When the voiceover speaks of taking oath or ministerial induction, cut to official oath ceremony footage (`sonia_oath_clean.mp4`).
- **Duration**: Video b-roll runs for the natural duration of the spoken statement or action (typically 3.5s to 6.5s, strictly under 10 seconds).

### C. Audio-Driven Editorial Still Photography Matching & Pacing
- **Direct Entity / Context Match**: Every still photo must directly visualize the person, historical event, document, or location spoken in the voiceover at that second:
  - Spoken reference to family/past history -> Archival photo (e.g., Rajiv & Sonia Gandhi 1985 White House photo).
  - Spoken reference to national political reactions -> High-res Lok Sabha benches or Parliament exterior.
  - Spoken reference to newspaper coverage -> High-res newspaper headline archival scan.
- **Pacing**: Still images must **strictly remain for 2.0 to 3.0 seconds max**, paired with non-repeating dynamic camera movements (`zoom_in`, `zoom_out`, `pan_left`, `pan_right`, `fast_push`).

### D. Audio-Driven Bespoke Motion Graphics Generation & Dynamic Timing
- **Direct Semantic Reflection**: Motion graphics must never be generic templates. They must visually represent the exact semantic idea in the voiceover at that second:
  - **Book Title & Launch Announcement**: Mechanical Split-Flap board with live flipping characters, active audio wave visualizer, and bold Hindi headline badge.
  - **Distorted Claims / Classified Truth**: Confidential Dossier Blueprint with dual laser scanners (gold horizontal + red crosshair) and slammed "TOP SECRET // बड़ा खुलासा!" stamp.
  - **Historical Milestones / Political Journey**: 4-Stage Timeline HUD with traveling golden laser beam illuminating each era sequentially.
  - **Polarized Public Reaction / Debate**: Seismic Opinion Radar with live fluctuating percentage indicators (49% vs 51%) and oscillating needle.
  - **Political Climax / Punchline**: High-voltage Tamasha Warning HUD with 360° rotating emergency beacon and impact shockwave.
- **Audio-Beat Micro-Timing**: The internal animations (laser sweep start/end, stamp impact, node illumination, shockwaves) must trigger in synchronization with the cadence and emphasis beats of the speaker's voice.

### E. Audio-Synchronized Kinetic Captions (Strictly 3–4 Words)
- **Pacing & Length Contract**:
  - Captions must display strictly **3 to 4 spoken words** at a time.
  - Words must match the voiceover **verbatim** as spoken by the clone voice.
  - Never display full sentences, paragraphs, or synthesized summaries.
- **Motion-Director Spring Animation**:
  - Centered bottom capsule (`bottom: 60px`, `z-index: 90`), translucent obsidian glass (`rgba(16, 2, 4, 0.94)`), 2px gold border (`rgba(255, 215, 0, 0.5)`).
  - Words enter with Apple-grade spring physics:
    ```ts
    spring({
      frame: frameIntoCue - wordOffset,
      fps: 30,
      config: { damping: 200, mass: 0.6, stiffness: 160 }
    });
    ```
- **Emphasis Word Highlighting**:
  - In every 3–4 word chunk, highlight 1 primary punchy keyword in News Fair Gold (`#FFD700`, `font-weight: 900`, gold drop shadow `0 8px 25px rgba(255, 215, 0, 0.6)`), matching vocal emphasis peaks.



### F. Verbatim Audio Synchronization & Accurate Speech Alignment
- **On-Screen Text Must Accurately Show What Audio Says**: Subtitles and captions must faithfully mirror the exact spoken words in the audio track.
- **Ban on Phonetic Misspellings**: Raw Whisper output often produces phonetic garble or misheard words (e.g. "पत्फर" instead of "पत्थर", "एक रोग बारतियों" instead of "140 करोड़ भारतीयों", "सत्त्मेव जैते" instead of "सत्यमेव जयते"). Raw un-aligned output is strictly forbidden.
- **Compulsory Script-Audio Alignment (`aligned_words.json`)**:
  1. The clean, grammatically verified script text must be acoustically aligned against the audio using Whisper's millisecond word-level timestamps (`align.py`).
  2. Cues must be grouped into strictly **3 to 4 words** per chunk.
  3. Every cue must start and end at the exact millisecond when the speaker utters those 3–4 words, ensuring flawless lip-sync and reading cadence.

---

## 6. Channel Branding & Visual Identity

### A. Official Channel Logo
- **Asset Path**: `D:\News\Editing\News fair.png`
- **Transparent Asset**: `reels-engine/public/brand/news_fair_logo_transparent.png`

### B. Color Palette
- **Brand Crimson**: `#7F0203` (Primary broadcast accent)
- **Deep Burgundy / Obsidian**: `#080102` / `#0D0102` (Main cinematic backdrop)
- **News Fair Gold**: `#FFD700` (Keyword emphasis, border trims, highlights)
- **Text Crisp White**: `#FFFFFF` (Headlines, regular captions)
- **Alert Red**: `#FF0000` (Pulsing live dots, emergency badges)

### C. Floating Broadcast Channel Bug (Top-Left)
Fixed at `top: 40px`, `left: 50px`, `z-index: 80`:
- 44px channel logo with golden drop shadow.
- Channel title: `"News Fair"` (`fontSize: 24`, `fontWeight: 800`, white, Baloo 2).
- Tagline: `"सच्ची पत्रकारिता"` (`fontSize: 13`, `fontWeight: 700`, gold, Baloo 2, uppercase).
- Pulsing red broadcast beacon dot (`12px`, `backgroundColor: #FF0000`, `boxShadow: 0 0 14px #FF0000`, pulsing with `Math.sin(frame / 4)`).

### D. Press Credit Badge (Top-Right)
Fixed at `top: 40px`, `right: 50px`, `z-index: 80` (only visible on external editorial photos):
- Translucent dark pill (`rgba(18, 2, 4, 0.88)`), gold border (`rgba(255, 215, 0, 0.5)`).
- Gold dot indicator + 2–3 words uppercase text:
  ```
  ● CREDIT: PTI PHOTO
  ● CREDIT: ANI NEWS
  ● CREDIT: SANSAD TV
  ● CREDIT: THE HINDU
  ```

---

## 7. Strict Local Typography Specification: Authentic Hindi Baloo Font

### A. Hindi Devanagari Baloo Support Contract
- **The Core Font Engine**: In Google Fonts, the Baloo family separates scripts by regional name: `Baloo 2` covers **Devanagari (Hindi, Marathi)**, while `Baloo Bhai 2` was designed for **Gujarati**.
- **Full Compatibility Alias**: To guarantee that requests for "Baloo Bhai", "Baloo Bhai 2", or "Baloo 2" always render the authentic, iconic chunky rounded Hindi letters:
  1. `@font-face` must map `'Baloo Bhai 2'`, `'Baloo Bhai'`, and `'Baloo 2'` to the Devanagari TTF files (`Baloo2-Bold.ttf`, `Baloo2-ExtraBold.ttf`).
  2. Embed fonts via base64 data URI in `fonts.css` directly imported into `src/index.ts` so Chromium / Puppeteer loads them synchronously into memory without network delay or system fallback.
  3. Every component specifies:
     ```ts
     fontFamily: "'Baloo Bhai 2', 'Baloo Bhai', 'Baloo 2', cursive, sans-serif !important;"
     ```
  4. Ensure all text renders in **Bold** (700, 800, or 900 weight).

---

## 8. Review & Quality Gate (Before Any Video Render)

Before executing any final video render, the following gate must be passed:

1. **Storyboard Inspection**:
   - Generate representative still frames (`npx remotion still ...`) covering every key shot (news hook, motion graphics, b-roll shots, captions).
   - Verify zero text clipping, correct press credits, proper Baloo Bold typography, and correct logo placement.

2. **Live Studio Preview**:
   - **Remotion Studio**: [http://localhost:3000/](http://localhost:3000/)
   - **HyperFrames Studio**: [http://localhost:3002/#project/studio](http://localhost:3002/#project/studio)
   - Play audio to verify that the 3–4 word captions lock on to the voiceover timing with zero drift.

3. **User Approval Sign-off**:
   - The user must review and approve the storyboard stills and studio preview before starting the final MP4 export (`npx remotion render`).

---

## 9. Adobe Premiere Pro Project Export Workflow (`.prproj` / XML)

When an editor needs to bring the generated video into **Adobe Premiere Pro** for manual post-production, Lumetri color grading, custom transitions, or advanced sound mixing, use the **Premiere Pro XML Interchange Standard (FCP 7 XML / XMEML)**:

### A. Why Premiere Pro XML Interchange (Over Raw `.prproj`)
- Native `.prproj` files are gzip-compressed XML databases tied to a proprietary internal build number (`Version="XX"`). Opening a `.prproj` generated for a different build produces the lock error: *"This project was saved in a newer version of Adobe Premiere Pro and cannot be opened."*
- **Premiere Pro XML (`.xml`)** is Adobe's universal project exchange format. It opens with 100% fidelity in **any release** of Adobe Premiere Pro (CS6, CC 2018 through 2025).
- Upon importing the XML, pressing **`Ctrl + S`** immediately saves the project as a native **`.prproj`** file tailored specifically to the user's installed Premiere Pro version.

### B. Project Structure in Premiere Pro
When imported, the XML automatically constructs:
1. **Sequence**: 16:9 Landscape (1920×1080 @ 30 FPS).
2. **Video Track 1 (V1)**: All visual cuts (bespoke motion graphic renders, authentic video b-roll clips, editorial photos) placed back-to-back at exact millisecond timecodes.
3. **Video Track 2 (V2)**: News Fair transparent channel bug overlay.
4. **Audio Track 1 (A1)**: Master voiceover (`audio.wav`) locked to frame 0.
5. **Captions Track**: Synchronized 3–4 word verbatim Hindi subtitles via companion `.srt`.
6. **Automatic Relinking**: All media paths point directly to absolute local hard drive paths (`file://localhost/...`), eliminating "Media Offline" errors.

---

## 10. Advanced Broadcast Motion Graphics Architecture & Engineering

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

6. **Top Area Cleanliness & Channel Bug Primacy (Strict Ban on Top Sliver Banners)**:
   - **Strictly Prohibited**: Never place a full-width sliver bar, top roof banner, or ticking clock band across the top of the canvas.
   - **Open & Breathable**: The top edge must remain completely open and breathable, allowing the background depth to breathe with only the top-left News Fair Channel Bug and `🔴 LIVE` pill anchored cleanly at `top: 26px, left: 40px`.

7. **Augmented Reality (AR) Data Pillars**:
   - For top-tier data visualization (vote shares, seats won, comparison statistics), instead of flat boxes popping up, use **3D bar charts or data pillars** that appear to physically grow out of the floor of the news studio or street-level B-roll footage.
   - **Camera Pan & Orbit**: The camera slightly pans or orbits around them, adding depth, cast shadows, and spatial realism to raw numbers.

---

## 11. The 32 Mandatory Broadcast Production Laws

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

16. **Subject Framing, Scale & Y-Positioning Mandate (Zero Head/Chin Cutoff & Adaptive PIP Dimensions)**:
    - **Adjust Scale and Position**:
      - Whenever framing a political leader or subject (e.g., Prashant Kishor, Lalu Yadav) inside a PIP monitor, **decrease the Scale (zoom out)** (`imageZoom: 0.88 to 0.94`) until the entire subject is completely visible within the frame.
      - **Adjust the Y-Position / Object-Position** (`objectPosition: "center 18%"` to `"center 25%"` or `imageOffsetY`) to center the subject vertically so their head is no longer cut off at the top, and their mouth, chin, microphone, and gesturing hands are not buried or chopped by the bottom Name Plate.
    - **Change Framing Strategy (Adaptive Aspect Ratio Dimensions)**:
      - Never force a generic 16:9 landscape box (`960×520`) on every image.
      - If scaling the image down leaves empty space inside your PIP box, **change the dimensions of the PIP box itself**:
        - Instead of using a standard 16:9 rectangle for all images, **adjust the PIP frame to match the aspect ratio of the source image** (e.g., a tailored `620px to 720px × 540px` monitor for 1:1 square or 4:5 / 3:4 portrait photos like Prashant Kishor or Lalu Prasad Yadav).
        - Alternatively, use a `"contain"` setting with a darkened/blurred ambient backdrop or an authentic "Fill" setting, ensuring the focal point (the subject's face) remains perfectly centered without severe zoom-in cropping.

---

17. **Pacing & Dynamic Transition Architecture (Rapid Laser Wipes, White Flash Bursts & Glitch Slices)**:
    - **Zero Slow Crossfades / Cold Hard Cuts**: Generic presentation dissolves and motionless hard cuts lack the punch of a fast-paced live television news broadcast.
    - **Mandatory 10-Frame Dynamic Transitions**: Deploy broadcast-style energetic transitions on scene entrances AND on every internal cut between assets:
      - **Angled Laser Wipe Beam**: Rapid horizontal beam with an angled skew (`transform: skewX(-18deg)`) sweeping from `-20%` to `120%` across 8–10 frames.
      - **White Light Flash Burst**: A high-energy brief white flash (`#FFFFFF`, `mixBlendMode: screen`, peak opacity `0.85` decaying over 6 frames) simulating a camera flash or satellite feed lock.
      - **Digital Glitch Displacement**: Subtle horizontal signal slice displacement layers to reinforce live satellite uplink texture.

18. **Continuous Ken Burns Internal Motion Mandate (Zero Motionless Stills)**:
    - A completely still photo, even inside an elaborate PIP frame, kills visual broadcast momentum.
    - **Continuous Zoom**: Every image and footage clip MUST feature continuous, active Ken Burns animation (`scale: 1.00` to `1.08` or pan) over its duration.
    - **Per-Clip Scale Reset**: In scenes containing internal cuts between multiple photos/clips, the Ken Burns scale must **reset fresh per clip** (calculated from `frame - cutFrame`) so secondary clips do not linger on an inherited static end-scale.

19. **Landscape & Non-16:9 Image PIP Framing Prompt & Standard Operating Procedure**:
    - **Universal Correction Prompt**:
      > *"Adjust the scale and fit of all landscape and portrait images within the Picture-in-Picture (PIP) frames. Ensure the 'Fit to Frame' or 'Scale to Fit' option is selected so the entire subject is visible without the top or bottom being cropped. If this leaves empty space on the sides, either adjust the PIP frame's aspect ratio to match the image or apply a blurred, zoomed-in version of the same image as a background layer within the PIP frame."*
    - **Standard Code Implementation**:
      - Set `fitMode="contain"` on non-16:9 media (such as 1:1 square, 3:4 portrait, or 9:16 vertical).
      - Automatically render a duplicated ambient underlay layer scaled to cover the box with `filter: blur(28px) brightness(0.28)`, eliminating dead black bars while preserving 100% of the subject's head, gestures, and features uncropped.

---

20. **Strict Prohibition of '● SATELLITE LIVE FEED' Clutter & Fake Signal Straps**:
    - **Never Use '● SATELLITE LIVE FEED'**: Do not add repetitive, artificial tags like `● SATELLITE LIVE FEED`, `● FEED ACTIVE`, or `● SATELLITE LOCATOR` in monitor header bars, video frames, or corner plates.
    - **Clean Authority**: The monitor header bar must feature only the clean, authentic location/topic headline (e.g. `🔴 LUCKNOW // विधान परिषद परिणाम` or `🔴 PATNA // RJD SUPREMO`) without fake satellite telemetry clutter.

21. **Strict Prohibition of Top 'Sliver' Banners & Full-Width Roof Bars (Clean Top Canvas Mandate)**:
    - **Never Render Top Full-Width Banners**: Absolute strict ban on rendering any full-width bar, "sliver banner", or roof bar running across the absolute top edge of the screen (e.g. `🔴 ELECTION 2026: UP MLC ELECTION RESULTS // SPECIAL INVESTIGATIVE REPORT • NEWS FAIR SPECIAL • 15:45:08 IST`).
    - **Visual Claustrophobia**: Such top banners create visual clutter, crowd the canvas, and resemble PowerPoint presentations rather than clean broadcast television.
    - **The Clean Top Rule**: The top of the 16:9 canvas must remain 100% open, clean, and uncluttered. Only the official News Fair Channel Bug and pulsing `🔴 LIVE` badge belong in the top-left corner (`top: 26px`, `left: 40px`). Never span text, borders, or digital clocks across the top margin.

22. **Clean Screen Transitions & Zero Graphic Overlap Mandate**:
    - **The Screen Must Be Kept Clean**: Never layer new PIP videos or secondary graphics on top of old data charts or maps without completely clearing the screen first.
    - **Animate Off or Hard Cut**: Before bringing in the next graphic (e.g. a state locator map) or a new PIP video (e.g. politician quote), the previous graphic (e.g. bar chart) must completely animate off the screen or be swept away via an angled laser wipe or 1-second stinger transition.
    - **Zero Global Background Map Ghosting**: Never place regional outline maps (e.g. up_map.svg, ihar_relief_map.svg) inside persistent global background containers where they linger faintly under subsequent scenes, creating the illusion of messy, leftover graphic clutter. Maps belong strictly in their own dedicated geospatial locator scenes.

23. **Dedicated Full-Screen Graphics (FSG) Standard**:
    - **No Squeezing of Major Data Graphics**: Important data visualizations (e.g., BJP vs SP seat comparison AR pillars, 3D geospatial maps, explosive quote boards) must be dedicated full-screen graphics (1160x540 or full-stage) for their entire duration.
    - **Zero Competing Footage**: Never squeeze complex charts into small PIP boxes while other videos or anchor footage play awkwardly beside them.
    - **Complete Return**: Once the voiceover finishes with the numbers or quotes, the graphic must cleanly sweep away and disappear completely, returning to full-screen B-roll or the next topic.

24. **High-Impact Visible PIP Animation Mandate**:
    - **Ban Microscopic 2-3px Motion**: Tiny 2-3px sine wave wobbles are invisible on 1080p broadcast screens and look static.
    - **Perceptible Dynamic Motion**: Every PIP monitor frame MUST feature:
      1. Visible floating displacement (±10px translateY via Math.sin((frame / fps) * 1.8) * 10).
      2. Subtle live rotational tilt (±0.7deg via Math.sin((frame / fps) * 1.4) * 0.7).
      3. Punchy entrance zoom pop (scale: 0.93 -> 1.00, opacity: 0 -> 1 over the first 8 frames).
      4. Continuous Ken Burns internal push (scale: 1.00 -> 1.08) on the photo/footage inside.
      5. Moving specular glass glare/sheen sweeping across the monitor face every 6 seconds.

25. **The 5-Second Motion Graphic Rule & Strict Audio Synchronization**:
    - **Strict 3 to 5 Second Duration Limit**: Any motion graphic that does not feature a photograph or video (such as text-only Lower Thirds, full-screen data charts, or quote boards) must only remain on screen for a strict duration of **3 to 5 seconds**.
    - **Exact Audio Cue Sync**: Sync the appearance of the graphic with the exact spoken audio cue. Hold it just long enough for the viewer to absorb the data, and immediately animate it off-screen.
    - **Lower Thirds (Name Plates & Headlines)**:
      - `0.0s – 0.5s`: Solid color bar and text quickly slide or wipe in from the left (`translateX: -80px -> 0px`).
      - `0.5s – 4.0s`: Text holds on screen while the voiceover mentions the person or breaking topic.
      - `4.0s – 4.5s`: Bar slides out or collapses downward, allowing full-screen B-roll video to continue playing seamlessly.
    - **Full-Screen Data Charts (Bar Charts & Tallies)**:
      - `0.0s – 1.0s`: Bars rapidly grow and numbers roll up to their totals.
      - `1.0s – 4.5s`: Chart holds on screen with subtle pulsing glow while voiceover reads exact numbers (with audio-synced column highlighting).
      - `4.5s – 5.0s`: Chart collapses downward and completely wipes away directly into real-world stock footage (B-roll) of the political parties.
    - **Crucial Rule on Graphic Exits**: When any 3-5 second motion graphic animates *off* the screen, it must **never leave behind an empty, dark background**. The graphic must always transition out to reveal high-quality, full-screen internet stock footage (B-roll) filling the space.

26. **Professional Data Chart Animation Standard (AR Data Pillars & Tabulation)**:
    - **The Entrance Animation (The Data Build-Up)**:
      - *Frame & Header Wipe*: Outer bounding box and top header bar wipe in quickly from left to right in 0.5s (`clipPath: polygon`).
      - *Growing Bars*: Set the anchor point for bars to the baseline (`transformOrigin: 'bottom center'`). Animate height from 0% to 100% over 1.2s to 1.5s so they grow upwards from the floor.
      - *Rolling Number Counters*: Numbers must not be static text; apply rolling counters rapidly counting up from `0` to their final values as the bars grow.
      - *Logo Elastic Pop*: Party logos (e.g. BJP Lotus, SP Bicycle) pop in with an elastic bounce (`scale: 0% -> 115% -> 100%`) right as the bars hit their peak.
    - **Continuous 'Live' Motion (Idle State)**:
      - *Pulsing Tally Indicator*: Continuous pulsing red recording dot next to 'ELECTION COMMISSION' (fading opacity 100% to 40% every 1 second).
      - *Shimmering Glows*: Outer strokes around data bars slowly pulse in neon brightness (`boxShadow: 0 0 40px`).
      - *Background Drift*: Faint tech grid pattern continuously pans and slowly breathes (`scale: 100% -> 105%`) over the clip duration.
    - **Audio-Synced Highlighting (Guiding Viewer Focus)**:
      - *Focus on Party A*: When audio mentions Party A (e.g., *'Chhah par BJP...'*), scale Party A column to 105% with full brightness while dimming Party B to 70% opacity.
      - *Focus on Party B*: When audio mentions Party B (e.g., *'...aur paanch par Sapa ka kabza'*), scale Party B column to 105% with full brightness while shrinking Party A back to 100% and 70% opacity.
      - *Exit Collapse*: When voiceover finishes discussing data, the entire graphic collapses downward (`scaleY: 1 -> 0`), immediately transitioning into real-world B-roll footage.

27. **Strict Headroom & Zero-Clipping Mandate for Data Charts and PIP Graphic Elements ("Motion Graphic Chart Must Be Fully Seen")**:
    - **User Mandate / Problem Statement**: *"Motion graphic chart is not fully seen in PIP frame. Fix this so next time this mistake never happens."*
    - **Root Cause**: Excessive pillar bar heights (e.g. >250px inside a ~560px container) push top party logos (such as the BJP Lotus circle or SP Bicycle flag) out of the top of the container, where `overflow: hidden` completely cuts them off from the viewer.
    - **Strict Headroom Standard**: Every data chart, comparison pillar, and tally board must provide at least **110px to 130px of safe open headroom** between the top of the highest pillar/logo and the top header strap so that party symbols are 100% visible with zero clipping.
    - **Calibrated Pillar Bar Height Formula**:
      `Max Bar Height <= Container Viewport Height - (Logo Height + Logo Gap + Base Text Height + Top/Bottom Padding) - 110px Safe Headroom`.
      - For a standard ~560px container (viewport height ~472px):
        - Highest Pillar Bar (e.g. BJP 6 seats) must be calibrated to **200px to 215px max**.
        - Secondary Pillar Bar (e.g. SP 5 seats) must be calibrated to **165px to 180px max**.
      - With a 66px circular party logo and 60px label text, total height is ~344px, guaranteeing 128px of open headroom.
    - **Mandatory `flexShrink: 0`**: All party logos, icons, and top chips must specify `flexShrink: 0` so flex layouts never compress or push logos out of the visible screen area under dynamic column scaling (`scale: 1.05`).


---

28. **Strict Single Primary Visual Mandate & Screen Cleanliness (Zero Overlap & Zero Multi-Graphic Stacking)**:
    - **Single Visual Primacy**: Only ONE primary visual element may occupy the screen at any moment:
      1. A single standardized center-stage PIP news monitor (`960x520px`).
      2. A standardized 2-box duel split (`580x400px` each).
      3. A dedicated Full-Screen Graphic (AR Data Pillars, 3D Geospatial Locator Map, or Full-Screen Quote Board).
    - **Constant Lower Third & Ticker Only**: The only concurrent overlay elements permitted alongside the primary visual are the docked Lower Third (L3) strap and the bottom scrolling News Ticker.
    - **Absolute Ban on Graphic Stacking**: Never layer a data chart and a map on screen at the same time. Never display a PIP video on top of or beside an active bar chart or locator map.
    - **Clean Screen Exit Protocol**: Before introducing a new visual, the previous visual must be 100% animated off-screen (e.g. downward collapse, fade, or slide) or cleanly wiped away via an energetic 10-frame transition (laser wipe beam, white flash burst, digital glitch slices).

29. **Mandatory 5-Second Exit for Maps & Data Charts (Cut to High-Quality Full-Screen B-Roll)**:
    - **Strict 3 to 5 Second Duration Limit**: Any graphic that does not feature live action video or editorial photos (such as 3D Geospatial Locator Maps, AR Data Pillars, and text tallies) must only remain on screen for a strict **3 to 5 seconds max** (just long enough for the voiceover to deliver the key tally or constituency names).
    - **Strict Prohibition of Lingering Graphics**: Never leave a locator map or bar chart on screen for 15+ seconds or for the remainder of a scene!
    - **Mandatory Cut to High-Quality B-Roll**: When a 3-5 second motion graphic animates off-screen, it must **NEVER leave behind an empty, dark gradient canvas**. The transition must instantly reveal high-quality, full-screen internet stock footage (B-roll) or standard broadcast monitor video filling the space (e.g., press conferences, counting centers, Vidhan Sabha, street-level party celebrations, constituency landmarks).

30. **Unified Standard PIP News Monitor Architecture (Fixed Dimensions, Border, Nameplate, & Zero White Pillarboxing)**:
    - **Standardized News Monitor Dimensions**:
      - Single Center Stage Monitor: Strictly **960x520px**, centered in the upper 75% of the screen (`paddingBottom: 160px`).
      - Duel Split Screen: Strictly two **580x400px** monitors side-by-side with a 36px central gap.
    - **Mandatory Frame Anatomy**:
      - Sharp corners with `borderRadius: 20px` and `border: 3.5px solid <borderColor>`.
      - Deep ambient shadow (`boxShadow: 0 20px 60px rgba(0,0,0,0.95), 0 0 40px <glowColor>`).
      - Top live feed header strap (`height: 40px`, pulsing red status dot, location headline).
      - Solid high-contrast broadcast Name Plate docked at the bottom (`height: 48px`, `zIndex: 100`, top accent line).
      - CRT TV scanline texture overlay (`repeating-linear-gradient`) and dynamic sweeping specular glass sheen every 6s.
      - Perceptible continuous Ken Burns motion (`scale: 1.00 -> 1.08`).
    - **Zero White/Blank Pillarboxing Mandate**:
      - Media inside monitors must seamlessly integrate with broadcast lighting.
      - Never leave bright white vertical margins or blank pillars on portrait or light-background photos inside the monitor.
      - Use `fitMode="cover"` with calibrated focal centering (`objectPosition: "center 15%"` to `"center 25%"`), or when `fitMode="contain"` is required, render a darkened, blurred ambient underlay layer (`filter: blur(28px) brightness(0.28)`) or replace studio white backgrounds with dark authentic newsroom gradients matching co-panelists.

---

31. **Absolute Zero-Cropping & Complete Subject Visibility Mandate ("Images Are Not Fully Seen / Heads & Chins Chopped Off")**:
    - **User Mandate / Problem Statement**: *"Images are not fully seen in PIP frames (politicians' hair, foreheads, and chins are cut off). Fix this so this mistake never happens."*
    - **Root Cause**: Applying `fitMode="cover"` to portrait or non-16:9 vertical images (1:1 square, 4:5, 3:4, or 9:16) inside 16:9 monitor frames forces Remotion to scale the image horizontally by 180%+, chopping off 50% to 65% of the vertical height (foreheads, hair, skull, eyes, chins, and clothing).
    - **Mandatory Universal Fix**:
      - **Strict Prohibition of `fitMode="cover"` on Portrait / Non-16:9 Media**: Never use `cover` on portrait or vertical leader photographs.
      - **Mandatory `fitMode="contain"` with Safe Zoom**: Strictly set `fitMode="contain"` and `imageZoom: 0.94 to 0.96` with `objectPosition: "center center"`.
      - **Ambient Blurred Extension Layer**: Underneath the contained image, render an edge-to-edge duplicated background layer with `objectFit: "cover"` and `filter: "blur(28px) brightness(0.28)"`. This fills the monitor completely, preserves broadcast dark lighting, and guarantees that **100% of the subject (hair, forehead, eyes, face, chin, neck, gestures) is completely visible without any cropping**.


---


---

32. **The 5-Second Pacing Rule for All Visual Assets (Universal Pacing Standard)**:
    - **User Mandate / Problem Statement**: *"Enforce the 5-Second Pacing Rule for all visual assets: Select every PIP image, video clip, and full-screen graphic on the timeline. Trim the duration of each individual asset to a maximum of 3 to 5 seconds. If a specific topic or voiceover segment lasts longer than 5 seconds, cut to a new, related B-roll video clip or a different camera angle to maintain visual momentum. No single graphic or image should remain on screen longer than 5 seconds before transitioning out."*
    - **Universal 3-to-5-Second Asset Limit**: Every PIP image, video clip, and full-screen graphic on the timeline MUST have its duration trimmed to a maximum of **3 to 5 seconds** (strictly 3.0s to 5.0s max).
    - **Continuous Visual Momentum via Cutaways**: If a specific topic, news segment, or voiceover narration lasts longer than 5 seconds, the timeline MUST cut to a new, related B-roll video clip or a different camera angle to maintain visual momentum.
    - **Zero Visual Stagnation**: No single graphic, map, chart, or image should EVER remain on screen longer than 5 seconds before transitioning out.
    - **Broadcast Wipe & Flash Transitions on Every Cut**: Every cut between assets must be accompanied by an energetic broadcast transition (angled laser wipe beam, subtle flash burst, or glitch displacement) to reset viewer engagement and match high-tempo television news aesthetics.

---

---

33. **The Mixed-Media Framing Rule (Alternating PIP & Full-Screen Edge-to-Edge Visuals)**:
    - **User Mandate / Core Principle**: *"The Mixed-Media Framing Rule: Alternate between PIP frames and full-screen visuals to create a dynamic broadcast pace. Apply the 3-5 second duration rule to all media, regardless of how it is framed. Maintain the Lower Third text bar and scrolling ticker at the bottom of the screen at all times, layered over both PIP and full-screen media."*
    - **How to Choose Between PIP and Full-Screen**:
      - **1. When to Use Picture-in-Picture (PIP Broadcast Monitor)**:
        - **Portraits & Headshots**: When showing a picture of a specific politician (like Yogi Adityanath or Akhilesh Yadav), place them inside a standardized PIP monitor (`fitMode="contain"`, safe headroom, blurred ambient backdrop).
        - **Comparisons**: When comparing two opposing leaders or data points side-by-side, use two PIP boxes next to each other (e.g., 2-box duel split screen).
        - **Quotes**: When displaying a text quote next to a person's face, keep the person framed inside a PIP monitor or dedicated quote plate.
      - **2. When to Use Full-Screen (Edge-to-Edge)**:
        - **Immersive B-Roll Video**: Real-world footage of crowds, rallies, people voting, or EVM machines should take up the entire screen (with the Lower Third text and Ticker visible at the bottom). This pulls the viewer directly into the live scene.
        - **Establishing Shots**: Landscape images, aerial views, or drone videos of critical locations (such as the Vidhan Bhavan/Assembly building in Lucknow or the Varanasi ghats) should be displayed full-screen to establish geographic authority.
        - **High-Impact Action**: Any footage showing movement, protests, or celebrations should break out of the PIP box and expand full-screen for maximum impact.
    - **Persistent Broadcast Layering**: The Lower Third headline bar, live category chip, acoustic Whisper subtitles, and continuous scrolling ticker MUST remain visible at all times, docked at the bottom of the screen layered strictly *over* both PIP and full-screen media.
    - **Pacing Standard**: Apply the strict 3-to-5-second duration rule to all media assets, regardless of whether they are framed as PIP or full-screen edge-to-edge.

---

34. **The Absolute 'Show Only Once' Image Mandate, Compulsory Multi-Video Footage & Multi-Motion Graphics Standard**:
    - **User Mandate / Core Principle**:
      *"Images are repeated, meaning one image is shown for more than one time. One image must show only once across the entire video. Also, use more motion graphics, not only one, and use videos, not only one."*
    - **1. The Strict 'Show Only Once' Asset Law (Absolute Zero Asset Repetition)**:
      - **One Image = Strictly One Appearance**: Every single photograph, editorial portrait, background image, and document on the timeline must appear **strictly once**. Never show the same image file or camera angle twice anywhere in the video.
      - **Zero Duplicate Asset Reuse**: Reusing an image across different scenes or within the same scene is strictly forbidden.
      - **Unique Media Sourcing**: If a political leader (e.g., Amit Shah, Yogi Adityanath, Nitin Nabin, LK Advani) or a location (e.g., Vidhan Bhavan, Gomti River) appears multiple times in the narration, you **MUST source a completely distinct, unique photograph or video angle** for every single appearance.
      - **Automated Validation Requirement**: Build validation into the asset pipeline: `len(used_image_assets) == len(set(used_image_assets))`. If any duplicate image source is detected, the build must halt immediately.
    - **2. Compulsory Multi-Video Standard (Never Only One Video)**:
      - **No Photo Slideshows**: News Fair videos cannot consist solely of still photos with a single solitary video clip. You must actively interleave **multiple authentic video clips (B-roll)** across the timeline (minimum 3 to 6 distinct video clips per video).
      - **Sourcing Broadcast Video**: Download public broadcast footage via `yt-dlp` or use verified newsroom video archives:
        - Real press conference footage of politicians speaking.
        - Floor proceedings from Sansad TV or Vidhan Sabha.
        - Live political rallies, massive crowds, and marching workers.
        - Polling booth lines, EVM handling, and vote counting centers.
      - **Dynamic Video Framing**: Play high-impact crowd/rally/drone videos edge-to-edge full-screen, and frame speaker/press videos inside standardized Broadcast Monitors.
    - **3. Compulsory Multi-Motion Graphic Standard (Never Only One Graphic)**:
      - **Ban on Single-Graphic Videos**: Never produce a video that features only a single bar chart or one data graphic. Every investigative news video must incorporate **multiple distinct, bespoke motion graphics** (minimum 3 to 4 unique graphics per video) tailored to different narrative turns:
        - **Graphic 1: Full-Screen Quote Board (FSG)**: For explosive revelations or dramatic quotes (e.g., Amit Shah's *"जो भी नाराजगी है, गोमती नदी में डाल दीजिए..."*), displaying a deep obsidian background, massive stylized quotes (`“`), clean Baloo Devanagari typography, and speaker badge.
        - **Graphic 2: AR Data Pillars / Comparative Chart**: 3D growing pillar bars comparing governance numbers, seats, or vote shares (e.g., Yogi 200% governance vs past SP/BSP baseline) with 120px safe headroom.
        - **Graphic 3: Confidential Survey / Grievance Matrix**: High-impact dossier card visualizing internal party survey findings, dissatisfaction percentages, and key cadre feedback points.
        - **Graphic 4: Two-Column Dispute / Clash Board**: Clean two-column card contrasting conflicting political stances (e.g., *"बाहरी नेताओं को पद"* vs *"समर्पित कार्यकर्ताओं की उपेक्षा"*).
        - **Graphic 5: Mission 2027 Roadblock / Strategic Takeaway Card**: Final constitutional or strategic roadmap card summarizing the high stakes.
      - **Strict Pacing for All Graphics**: Every motion graphic must follow the 3-to-5-second pacing rule (Law 25 & 32), animating on with smooth spring physics and completely wiping off to reveal full-screen B-roll stock footage.

---

35. **The Continuous Graphic Animation Rule (No Static Graphics / Compulsory 3-Phase Lifespan)**:
    - **User Mandate / Core Principle**:
      > *"Never place a static image of a text board or chart on the timeline. Every motion graphic that does not feature a photo or video must follow a strict 3-to-5-second lifespan consisting of three dynamic phases:*
      > * **Phase 1: The Build-In (0.0s - 1.0s):** The graphic must visually construct itself. Backgrounds wipe in, boxes slide into place, text types out or fades in line-by-line, and chart bars grow from zero.*
      > * **Phase 2: The Active Idle (1.0s - 4.0s):** The graphic must never freeze. While holding on screen for the viewer to read, apply continuous micro-movements: the entire frame must slowly zoom in (100% to 105%), bounding boxes must have a subtle pulsing glow, and background grids must slowly pan.*
      > * **Phase 3: The Rapid Exit (4.0s - 5.0s):** Immediately upon the audio cue finishing, the graphic must collapse, swipe away, or glitch out, transitioning directly into full-screen, real-world stock video (B-roll). It must never fade to black."*
    - **Universal 3-Phase Lifecycle Architecture**:
      1. **Phase 1: The Build-In (`0.0s – 1.0s` / Frames `0 – 30`)**:
         - Background plates wipe or expand into view (`clipPath: polygon` or `scale: 0.95 -> 1.0`).
         - Cards, bounding boxes, and headers slide in energetically from opposite axes with spring physics (e.g. top banner drops down from top edge `translateY: -50px -> 0px`, left card slides in from left `translateX: -80px -> 0px`, right card slides in from right `translateX: 80px -> 0px`).
         - Text fades in or reveals line-by-line (`opacity: 0 -> 1`).
         - Chart bars physically grow upwards or horizontally from `0%` to their final values (`scaleX: 0 -> 1` or `width: 0% -> target%`), while numerical counters simultaneously roll/count up from `0%` to the target percentage.
      2. **Phase 2: The Active Idle (`1.0s – 4.0s` / Frames `30 – 120`)**:
         - **Zero Freeze Policy**: Graphics must NEVER sit static or frozen on screen.
         - **Slow Push-In Ken Burns**: The entire canvas slowly zooms from `100%` to `104%–105%` (`scale: 1.00 -> 1.05`).
         - **Subtle Pulsing Border Glow**: Accent borders pulse in luminance and shadow intensity (`boxShadow: 0 0 15px -> 35px`).
         - **Continuously Panning Background Grid**: Background dot-matrix or blueprint tech grid slowly drifts diagonally (`backgroundPosition: 0px 0px -> 40px 40px`).
         - **Continuous Shimmer/Sheen Loop**: Horizontal sheen highlights continuously sweep across the filled portion of chart bars and monitor frames.
         - **Micro Text Drift**: Body typography scales up imperceptibly (`100% -> 103%`) to maintain visual engagement while the voiceover reads the point.
      3. **Phase 3: The Rapid Exit (`4.0s – 5.0s` / Frames `120 – 150`)**:
         - As soon as the spoken cue concludes, the graphic must aggressively collapse inward (`scale: 1.0 -> 0.8, opacity: 1 -> 0`), retract back (`scaleX: 1 -> 0`), or glitch swipe off-screen.
         - **Never Fade to Black**: The exit MUST cut directly and immediately into high-energy, full-screen real-world stock video (B-roll footage) such as political rallies, press scrums, counting centers, or legislative chambers.
    - **Concrete Implementation Blueprints**:
      - **Split Quote Board (Party Conflict / Dispute Matrix)**:
        - *Build-In*: Top header banner drops down from top edge (`translateY: -60px -> 0px`). Left Leadership box slides in sharply from left (`translateX: -120px -> 0px`). Right Cadre Anger box slides in sharply from right (`translateX: 120px -> 0px`).
        - *Active Idle*: Diagonal background grid drift. Yellow and red borders pulse subtly (`boxShadow`). Box content slowly scales up (`1.00 -> 1.03`).
        - *Exit*: Both boxes rapidly collapse inward toward the center with digital wipe glitch, instantly cutting to full-screen B-roll video.
      - **Horizontal Bar Chart (Internal Confidential Survey HUD)**:
        - *Build-In*: Top red "CONFIDENTIAL" header badge snaps in from the left. Question labels wipe in from left to right. Red (82%), Amber (74%), and Orange (68%) progress bars physically grow horizontally from `0%` to their target widths. The percentage figures on the right simultaneously count up from `0%` to `82%`, `74%`, and `68%`.
        - *Active Idle*: Continuous bright sheen sweep loops across the filled bars. Slow 100% to 105% continuous push-in zoom across the frame. Subtle status pulse on badge.
        - *Exit*: Bars rapidly retract to 0% and cards collapse with digital glitch transition, cutting directly to full-screen B-roll video.


## How to Edit This Skill

This skill is fully editable. You can modify it at any time:
1. **Direct File Edit**: Open and edit `d:\News\Clude news ai\.agents\skills\news-video-16x9\SKILL.md` (or global copy at `C:\Users\ahmad\.gemini\antigravity\skills\news-video-16x9\SKILL.md`).
2. **In Chat**: Ask the assistant: *"Update the news-video-16x9 skill to add rule X"*.
3. Any changes made to the `SKILL.md` file take effect immediately for all subsequent tasks.
