# News Video 16:9 Ratio — Master Production Operating Standard (SOP)

This document establishes the official standard operating procedure, engineering specifications, and artistic rules for producing high-impact, broadcast-quality **16:9 news investigative videos** for **News Fair**.

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
   - **Role**: Millisecond-precision speech recognition, word-level audio alignment, and automatic subtitle cue extraction.

5. **yt-dlp**: [github.com/yt-dlp/yt-dlp](https://github.com/yt-dlp/yt-dlp)
   - **System Location**: System PATH (`yt-dlp 2026.10.26`)
   - **Command**: `yt-dlp -f "bestvideo[height<=1080]+bestaudio/best" <URL>`
   - **Role**: Downloading authentic press conference footage, parliamentary debates, and internet b-roll clips.

---

## 2. Quick-Reference Cheat Sheet ("Small Information")

| Parameter | Mandatory Rule | Implementation Requirement |
| :--- | :--- | :--- |
| **Video Ratio** | **16:9 Landscape (1920×1080)** | Full HD broadcast canvas at 30 FPS or 60 FPS. |
| **Image Cut Pacing** | **Strictly 2.0 to 3.0 Seconds Max** | Still photos must only appear for 2 to 3 seconds max. Never hold a still image longer than 3 seconds. |
| **Video & Motion Graphics Duration** | **As Long as Needed by Script (Strictly Under 10s)** | Video b-roll and motion graphics can be used as long as needed according to the script beat/sentence (typically 3.5s – 6.5s). **STRICT BAN on 10–20 second long video/motion graphic shots** to prevent dragging. |
| **Image Motion Variety** | **Never repeat the same animation** | Cycle across `zoom_in`, `zoom_out`, `pan_left`, `pan_right`, `diagonal_drift`, `fast_push`. |
| **Footage Mix** | **Compulsory Videos + Images** | Mix authentic web videos (b-roll/press clips) with clean editorial photos. |
| **Motion Graphics Animation**| **100% Dynamic & Highly Animated** | Every motion graphic must feature continuous multi-layered motion (sweeping lasers, oscillating needles, particle glows, floating 3D perspective, traveling light beams, expanding shockwaves). Zero static elements. |
| **Motion Graphic Understandability** | **Instant 1-Second Visual Comprehension** | Must be immediately understandable at a glance: crystal-clear visual metaphors (split-flap arrival, classified dossier stamp, timeline progress HUD, 3D rotating book, polarized opinion meter, flashing hazard punchline). Bold high-contrast Baloo typography. |
| **Motion Graphic Design** | **Bespoke per Script** | Never reuse the same generic template. Build unique visuals tailored to the specific story. |
| **Captions Length** | **Strictly 3 to 4 Words on Screen** | Exactly 3–4 words spoken verbatim in sync with audio. Never full lines or summaries. |
| **Captions Style** | **Motion-Director Spring Pop** | Apple-grade spring physics, centered bottom capsule, 1 gold highlighted emphasis word. |
| **Voiceover** | **Abhisar Sharma Clone Voice** | Authoritative, energetic, investigative tone with dramatic inflection. |
| **Typography** | **Exclusively the 9 Baloo Files** | `Baloo 2` & `Baloo Bhai 2` in **BOLD weights (700/800/900)** for both English and Hindi. |
| **Channel Logo** | `D:\News\Editing\News fair.png` | Top-left glass pill bug with logo, "News Fair", "सच्ची पत्रकारिता", and pulsating live red dot. |
| **Editorial Photo Credit** | **Strictly 2 to 3 Words** | Top-right badge: `● CREDIT: PTI PHOTO`, `● CREDIT: ANI NEWS`, `● CREDIT: SANSAD TV`. |
| **Channel Graphics Credit** | **ZERO Credit** | Do not put credit badges on News Fair's own custom motion graphics. |
| **AI Images** | **No Credit by Default** | If credit is necessary, strictly label as: `"AI generated image"` (2-3 words). |
| **Images With Text** | **Prohibited except real documents** | Never use photos with baked-in TV news tickers. Only use text images for genuine gazettes, court orders, or posters. |
| **Personal Media Ban** | **Do NOT use user's video or image** | Never use private, personal, or creator's own videos/photos. Strictly source broadcast media from the internet. |
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

## 4. Script-Tailored Motion Graphics (Always Dynamic, Never Static)

### A. Bespoke Design Strictly Aligned to Audio Script
Do not reuse the identical motion graphic in every video, and **never use generic, decorative motion graphics**. Every motion graphic must be conceived, designed, and animated **strictly according to what the spoken audio is saying at that exact timestamp**:

1. **Audio-Driven Visual Semantic Alignment**:
   - **Parliamentary & Political Standoffs**: When the voiceover speaks of heated Lok Sabha or Rajya Sabha debates, render Split-Flap mechanical departure boards, Lok Sabha / Rajya Sabha seating heatmaps, or Parliament confrontation HUDs displaying the spoken debate topics.
   - **Judicial Orders & Dissent Suppression**: When the voiceover speaks of legal repression, Section 163 bans, or court notices, render high-tech Legal Blueprint schematics with moving laser scanners and slamming administrative rejection stamps (*"सिस्टम से असहमति: धारा 163 का शिकंजा"*).
   - **Nationwide Campus & Student Protests**: When the voiceover speaks of nationwide university outrage (e.g., NALSAR, JNU, LU, MU, JU, NLSIU), render the **National Campus Alert Radar Map** with 360° rotating radar sweep and active pulsing red nodes placed on the specific universities named in the voiceover.
   - **Debates & Confrontation**: When the voiceover contrasts government power against student/opposition dissent, render the **Government vs. Opposition Dual Battle HUD** with rotating VS emblem and spoken quote callouts.
   - **Independent Journalism Defense**: When the voiceover discusses the attack on questioners and the need for courage in reporting, render the **Independent Journalism Shield** with glowing energy aura and News Fair brand core.
   - **Grand Finale & Channel Identity**: In the closing seconds as the voiceover delivers the final takeaway, render the **Truth Prevails Grand Finale** with rotating golden sunburst rays and the signature punchline (*"लेकिन सच्ची ख़बर नहीं! News Fair • जनता की आवाज़ • सच्ची पत्रकारिता"*).

2. **Audio-Beat Micro-Animations**:
   - Transitions, stamp slams, and alert pings must trigger in synchronization with the cadence and emphasis beats of the speaker's voice.

### B. Dynamic Motion Requirement — Zero Static Elements
Every single element on a motion graphic screen must remain active:
- Background grid lines must continuously scroll (`translateY(frame * 0.8)`).
- Cybernetic glow rings must breathe and pulse (`Math.sin(frame / 4)`).
- Card containers must float on micro-sine waves (`Math.sin(frame / 8) * 8`).
- Mechanical split-flap letters must micro-jitter (`Math.sin(frame * 1.5) * 1.8`).
- Radar scan sweeps must rotate 360° continuously.
- Live alert beacons must blink between intense red and dark ruby.

### C. Zero Credit on Channel Motion Graphics
Never add an editorial credit badge (like `● CREDIT: PTI PHOTO`) to News Fair's own custom-designed motion graphics. Credit badges are strictly reserved for external press agency photographs.

### D. Kinetic Dynamism & Multi-Layered Animation Architecture
Motion graphics must never appear as flat, decorative slides. Every graphic must operate like a living, broadcast-grade telemetry HUD with synchronized multi-layered movement:
1. **Primary Layer**: High-impact spring entrance (`spring({ damping: 10, mass: 0.8, stiffness: 200 })`) with physical overshoot and settle.
2. **Secondary Organic Layer**: Continuous non-stop environmental motion:
   - Floating perspective shifts (`transform: perspective(1000px) rotateY(...) translateY(...)`).
   - Oscillating gauges, meters, and needle fluctuations reflecting live measurement.
   - Dual-axis scanning laser sweeps with glowing heads and trailing light fades.
   - Animated progress nodes where light pulses travel down connector lines in real-time.
3. **Tertiary Micro-Detail Layer**:
   - Breathing aura rings (`radial-gradient`), scanning grid meshes, and digital particle drift.
   - Live mechanical flip animations where tiles cycle rapidly through intermediate glyphs before locking into place.
   - Physical impact shockwaves: when stamps or badges land, trigger an expanding radial shockwave ring and a 2-frame subtle micro-shake to convey physical weight.

### E. Instant Understandability & Visual Clarity Standards
A motion graphic fails if the viewer has to pause the video to understand what is being communicated. The core journalistic takeaway must be **immediately obvious within 1 second**:
1. **Clear Visual Metaphors**: Ground every abstract concept in a tangible real-world news construct:
   - **Breaking Book / Memoir Release**: Mechanical Airport Split-Flap board or 3D Floating Hardcover book with glowing release date pill.
   - **Classified Secrets / Unfiltered Truth**: Intelligence Dossier Blueprint with laser scanning bar and slammed bold "TOP SECRET // बड़ा खुलासा!" stamp.
   - **Political Career / Journey**: Sequential Timeline HUD with illuminated nodes, milestone dates, and active node glowing halos.
   - **Clashing Perspectives / Public Debate**: Polarized Seismic Meter with green vs. red cards, active needle fluctuation, and "VS" lightning indicator.
   - **Dramatic Punchline / Climax**: High-voltage Red Alert Warning HUD with flashing warning beacons, bold oversized quotes, and slamming impact stamps.
2. **High-Contrast Bold Hierarchy**:
   - Minimum font size of 24px for auxiliary labels and 48px to 68px for main punchlines.
   - Exclusively use `Baloo 2` and `Baloo Bhai 2` in **ExtraBold (800) and Black (900)** weights.
   - High-contrast color coding: News Fair Gold (`#FFD700`) on deep obsidian ruby (`#120204`), emerald green (`#00FF66`) for favorable shifts, neon alert crimson (`#FF3344`) for critical shifts.
   - Prominent Devanagari Hindi headlines positioned front and center so viewers instantly absorb the narrative beat.

---

## 5. Audio-Synchronized Kinetic Captions

### A. Pacing & Length Contract
- Captions must display strictly **3 to 4 spoken words** at a time.
- Words must match the voiceover **verbatim** as spoken by Abhisar Sharma clone voice.
- Never display full sentences, paragraphs, or synthesized summaries.

### B. Motion-Director Spring Animation
- Capsule positioned centered at bottom (`bottom: 60px`, `z-index: 90`).
- Background: Translucent obsidian glass (`rgba(16, 2, 4, 0.94)`), 2px gold border (`rgba(255, 215, 0, 0.5)`), heavy drop shadow (`0 15px 45px rgba(0, 0, 0, 0.85)`).
- Words enter with Apple-grade spring physics:
  ```ts
  spring({
    frame: frameIntoCue - wordOffset,
    fps: 30,
    config: { damping: 200, mass: 0.6, stiffness: 160 }
  });
  ```

### C. Emphasis Word Highlighting
In every 3–4 word chunk, highlight 1 primary punchy keyword:
- **Regular Words**: Dark glass capsule (`rgba(25, 3, 5, 0.9)`), crisp white text (`#FFFFFF`), `font-weight: 700`.
- **Emphasis Word**: Brilliant News Fair Gold capsule (`#FFD700`), obsidian black text (`#080102`), `font-weight: 900`, gold drop shadow (`0 8px 25px rgba(255, 215, 0, 0.6)`).

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

## 7. Strict Local Typography Specification

### A. Exclusively Allowed Font Files
No external CDN links or Google Fonts imports are permitted during production. Only the 9 local TTF files in `reels-engine/public/fonts/` and `studio/assets/fonts/` must be registered:

1. `Baloo2-Regular.ttf` (Weight 400)
2. `Baloo2-Medium.ttf` (Weight 500)
3. `Baloo2-SemiBold.ttf` (Weight 600)
4. `Baloo2-Bold.ttf` (Weight 700 — **Primary Bold**)
5. `Baloo2-ExtraBold.ttf` (Weight 800 / 900 — **Headline Extra Bold**)
6. `BalooBhai2-Regular.ttf` (Weight 400)
7. `BalooBhai2-Medium.ttf` (Weight 500)
8. `BalooBhai2-Bold.ttf` (Weight 700 — **Primary Bold**)
9. `BalooBhai2-ExtraBold.ttf` (Weight 800 / 900 — **Headline Extra Bold**)

### B. Font Face CSS Declaration Contract
Both Remotion and HyperFrames Studio must register all 9 files:
```css
@font-face {
  font-family: 'Baloo 2';
  src: url('fonts/Baloo2-Bold.ttf') format('truetype');
  font-weight: 700;
  font-style: normal;
}
@font-face {
  font-family: 'Baloo 2';
  src: url('fonts/Baloo2-ExtraBold.ttf') format('truetype');
  font-weight: 800 900;
  font-style: normal;
}
@font-face {
  font-family: 'Baloo Bhai 2';
  src: url('fonts/BalooBhai2-Bold.ttf') format('truetype');
  font-weight: 700;
  font-style: normal;
}
@font-face {
  font-family: 'Baloo Bhai 2';
  src: url('fonts/BalooBhai2-ExtraBold.ttf') format('truetype');
  font-weight: 800 900;
  font-style: normal;
}
* {
  font-family: 'Baloo 2', 'Baloo Bhai 2', sans-serif !important;
}
body, html, div, span, p, h1, h2, h3, h4, h5, h6 {
  font-weight: 700;
}
```

### C. Bilingual Hindi & English Support
- `Baloo 2` provides full Devanagari coverage with authentic conjuncts, matras, and rounded strokes matching the Latin alphabet proportions.
- Every text element must render in **Bold** (`font-weight: 700`, `800`, or `900`).

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
