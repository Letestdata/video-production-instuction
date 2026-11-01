---
name: news-video-16x9
description: Standard operating procedure and automated workflow for producing broadcast-quality 16:9 news investigative videos for News Fair. Enforces strict single-use asset discipline (zero image/video repetition), dual-layer full-screen portrait framing, dynamic 3-6s visual sequencing with integrated b-roll video, clean credit-free canvas, authentic Hindi Baloo typography, gapless verbatim Whisper acoustic subtitles, 5-6s kinetic motion graphics, continuous scrolling ticker, and direct master MP4 delivery.
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
| **Canvas Dimensions & Full-Screen Coverage** | `1920 × 1080 px` (16:9 Landscape) @ 30 FPS. **100% Full-Screen Edge-to-Edge Fill**: Zero letterboxing, black side pillars, or blank margins. Every visual fills the 16:9 canvas edge-to-edge. |
| **Universal Portrait Media Protocol** | **Dual-Layer Broadcast Framing**: Portrait/vertical images (9:16, 3:4, 1:1) MUST never have faces/chins cut off or leave empty sides. Layer A fills the full canvas with a blurred atmospheric background (`blur(24px) brightness(0.45)`); Layer B displays the sharp subject anchored to the upper third (`objectPosition: center 18%` to `center 22%`), ensuring complete facial visibility. |
| **Zero Media Repetition (Strict Single-Use Rule)** | **Every Image & Video Clip Used Strictly ONCE**. Zero duplicate assets across the entire video. Never reuse or loop an image or video clip in multiple scenes or within the same scene. Validated by automated pipeline check (`len(sources) == len(set(sources))`). |
| **B-Roll Video Footage Integration** | **Active Incorporation of Broadcast Video Clips**: Integrate high-definition news video footage (`.mp4`) alongside still editorial photography. Each video clip must also follow the strict single-use rule (strictly one-time use, zero looping). |
| **Universal Visual Cut Pacing** | Strictly **3.0 to 6.0 Seconds Per Visual**. **Zero Single-Asset Scenes**: A 45s scene must sequence **8 to 12 distinct, non-repeating images/videos**, each lasting 3–6s, cutting on spoken phrase boundaries. Holding one visual for 10–45s is strictly forbidden. |
| **Compulsory Glassmorphism Architecture** | **MANDATORY ACROSS 100% OF UI CONTAINERS & CARDS**. Every center dossier card, PIP monitor frame, lower-third dock, live news ticker, and subtitle capsule MUST use the **5-Layer Frosted Glass Contract** (`backdropFilter: 'blur(24px) saturate(180%)'`, translucent dark tint `rgba(6,12,20,0.80)`, specular top rim line `rgba(255,255,255,0.40)`, and moving diagonal sheen). Flat opaque plastic boxes (`#000000` / `#FFFFFF`) are strictly prohibited. |
| **Credit Attribution Policy** | **Strictly NO On-Screen Credit Stamps/Badges**: Remove all credit overlays (`● CREDIT: ...`, photo agency tags, watermarks). The broadcast canvas remains clean, uncluttered, and cinematic. |
| **Motion Graphic Card Duration** | Strictly **5.0 to 6.0 Seconds Max** (`150–180 frames @ 30 FPS`). Dossiers, HUDs, charts, and PIP cards must NOT linger for 10–50s. They enter dynamically, hold for 5–6s, and exit to full-screen cinematic imagery/footage for the rest of the scene. |
| **Non-Static Motion Graphics** | **Zero Static Cards Policy**: All graphics must feature active motion: kinetic text entrance, 2.5D inner photo zoom (`1.0 → 1.08`), continuous specular sheen sweeps, pulsing live beacons, and animated counting numbers. |
| **Camera Motion Variety** | Never repeat the same camera move consecutively. Cycle across: `zoom_in_center`, `pan_right_to_left`, `zoom_out_center`, `pan_left_to_right`, `diagonal_drift`, `fast_push`. |
| **Mixed-Media Rule** | **PIP Broadcast Monitor**: Portraits, leader face-offs, quotes.<br>**Full-Screen Edge-to-Edge**: High-energy B-roll, crowd rallies, parliamentary floor, drone establishing shots. |
| **Personal Media Ban** | **Strict Ban on User/Personal Media**. Sourced public broadcast footage (Sansad TV, ANI, PTI, PIB) or press archives only. |
| **Typography** | **Exclusively Hindi Baloo** (`Baloo 2` / `Baloo Bhai 2` Bold & ExtraBold via base64 embedded `fonts.css`). |
| **Captions / Subtitles** | Strictly **3 to 4 Words on Screen**, verbatim match to audio, centered bottom capsule, 1 gold highlight (`#FFD700`). |
| **Voiceover & Audio Mix** | Authoritative investigative delivery (`-1.0 dB` peak). BGM dynamically ducked to **`-18 dB to -22 dB`**. SFX at **`-6 dB to -10 dB`**. |
| **Top Area Cleanliness** | **Strict Ban on Top Sliver Banners & Roof Bars**. Top edge must remain open and breathable with only the top-left News Fair bug. |
| **Master Delivery Policy** | Direct master `.mp4` video export. **Do NOT create Premiere Pro (`.prproj`) or XML files** unless explicitly requested. |

---

## 3. Visual Footage, Portrait Framing & Single-Use Standards

### 3.1 Universal 3–6 Second Visual Sequencing Law (Pacing Discipline)
- **Strict Prohibition on Static Visual Monotony**: Never hold a single background image or B-roll shot for an entire 30–60 second scene. Doing so destroys broadcast engagement.
- **Continuous Multi-Visual Progression**: Every narrative scene must sequence a chain of distinct, non-repeating editorial assets cutting every **3.0 to 6.0 seconds** (e.g., a 45-second scene requires **8 to 11 distinct images/clips**, each lasting 3.5 to 5.5 seconds).
- **Thematic Diversity within a Scene**: Even when discussing a single topic (e.g., Dhuri constituency), the visuals must cycle across related contextual evidence:
  1. *0.0s – 5.5s*: Graphic dossier card over dimmed establishing shot.
  2. *5.5s – 10.0s*: Legislative assembly hall or parliament floor (Ken Burns zoom-in).
  3. *10.0s – 15.0s*: Sangrur district geography / rural Malwa landscape (pan left-to-right).
  4. *15.0s – 20.0s*: High-res leader rally or party press conference (zoom-out drift).
  5. *20.0s – 25.0s*: EVM voting machine or election commission gazette document.
  6. *25.0s – 30.0s*: Farmer protest tractor sit-in or rural gathering.
  7. *30.0s – 36.0s*: Punjab Police / border security checkpoint.
  8. *36.0s – 45.0s*: Golden Temple / cultural Punjab landmark.
- **Whisper Phrase Cuts**: Image and video transitions should snap cleanly to spoken phrase or sentence boundaries identified in `clean_cues.json`.

### 3.2 Strict Single-Use Asset Law (Zero Image & Zero Video Repetition)
- **Images Used Strictly Once**: No still photo may appear more than once in the entire video. Once an image has been displayed, it is retired from the timeline. Reusing the same image in different scenes or cycling it repeatedly is strictly prohibited.
- **Videos Used Strictly Once**: No B-roll video clip may be reused or looped. Every video snippet is shown exactly once for its allocated duration (3–6 seconds) and never reintroduced.
- **Inventory Sizing**: The production script must scout and prepare enough distinct assets to satisfy the entire video length:
  $$\text{Required Assets} \approx \frac{\text{Total Video Duration (seconds)}}{4.2\text{ s/cut}}$$
  *(e.g., a 10-minute / 600s video requires 120–150 distinct, unique images and video clips).*
- **Automated Validation**: Before rendering, verify unique source count:
  ```python
  assert len(timeline_assets) == len(set(timeline_assets)), "Duplicate assets detected in timeline!"
  ```

### 3.3 Universal Portrait Media Protocol & Dual-Layer Framing
Standard 16:9 news broadcasts regularly feature portrait-orientation photographs (e.g., vertical headshots of politicians, 9:16 mobile footage, documents). These MUST be handled with professional broadcast compositing:
1. **Edge-to-Edge Canvas Fill (No Black Bars)**: Never display raw vertical images with black pillarbox borders on the sides.
2. **Dual-Layer Broadcast Compositing**:
   - **Layer 1 (Atmospheric Base Fill)**: The image is scaled to 110% width/height and treated with `filter: blur(24px) brightness(0.45)`, providing an edge-to-edge ambient studio environment that dynamically matches the color palette of the subject.
   - **Layer 2 (Foreground Subject Presentation)**:
     - *Full-Bleed Presentation*: Set `objectFit: "cover"` with vertical anchor `objectPosition: "center 18%"` to `"center 22%"`. This anchors the crop to the subject's forehead and eyes, guaranteeing that heads, facial expressions, and upper torsos are never chopped off.
     - *Or PIP Framed Presentation*: Encase the portrait in a high-tech glass card or studio monitor with subtle border (`1px solid rgba(255,255,255,0.15)`) and deep drop shadow (`0 20px 50px rgba(0,0,0,0.7)`).
3. **Continuous 2.5D Ken Burns Animation**: Every portrait must execute active push or drift (`scale: 1.02 → 1.08`) so it remains dynamic throughout its 3–6s lifespan.

### 3.4 Broadcast Video Clip Integration
- **Mixed Media Discipline**: Incorporate real broadcast B-roll video clips (`.mp4`) alongside high-res photography to maximize editorial energy.
- **Sources & Authenticity**: Sourced via `yt-dlp` from official parliamentary feeds (Sansad TV), official press releases (PIB, ANI), or verified public news archives.
- **Cleanliness & Scrubbing**: Remove any third-party broadcast chyrons, station watermarks, or baked-in logos.
- **Frame-Accurate Synchronization**: Video clips must be trimmed cleanly with FFmpeg to 30 FPS (`-r 30 -c:v libx264 -an`) and integrated into the Remotion composition via `<Video>` or `<OffthreadVideo>`, cutting exactly on Whisper sentence cues.
- **Strict Single-Use**: Each video segment is shown strictly once—zero looping or repeating.

### 3.5 Media Cleanliness & Zero-Credit Canvas Standard
- **Zero On-Screen Credit Stamps**: Remove all credit overlays (`● CREDIT: PTI PHOTO`, `● CREDIT: ANI`, `● CREDIT: SANSAD TV`). Clean, cinematic broadcast presentation requires that the top-right canvas remain unburdened by attribution tags.
- **No Baked-In Newsroom Text**: Never use photos or footage with existing television news lower-thirds, tickers, or station watermarks. (Allowed exception: primary legal evidence like official gazette orders or signed court rulings).

### 3.6 Non-Repetitive Camera Moves
Every still photo must feature active 2.5D camera motion. Never leave an image static:
1. `zoom_in_center`: Scale `1.00 → 1.08`.
2. `pan_right_to_left`: TranslateX `+40px → -40px` with scale `1.04`.
3. `zoom_out_center`: Scale `1.09 → 1.01`.
4. `pan_left_to_right`: TranslateX `-40px → +40px` with scale `1.04`.
5. `diagonal_drift`: TranslateX `-25px → +25px` and TranslateY `+20px → -20px`.
6. `fast_push`: Snap scale `1.00 → 1.12` with soft damping spring.

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

## 6. Broadcast Motion Graphics Architecture (The 5–6s Lifecycle & Full-Screen Transition)

Never leave a graphic card or dossier statically covering the screen for the entire scene duration. Every motion graphic component (dossier, PIP card, infographic, debate box) MUST execute through a strict **5 to 6 second lifecycle** (`150–180 frames @ 30 FPS`), then transition into full-screen imagery/b-roll:

1. **Phase 1: Snappy Entrance (`0.0s – 0.6s` / Frames 0–18)**:
   - Header badge drops or snaps in (`translateY: -30px → 0px`).
   - Center dossier / card springs in (`scale: 0.85 → 1.0`, `opacity: 0 → 1`) with physics (`damping: 12, stiffness: 140`).
   - Image inside the card begins active 2.5D push-in zoom (`scale: 1.00 → 1.06`).
   - Background footage/image runs softly dimmed (`opacity: 0.30 - 0.40`, `filter: blur(8px)`).
2. **Phase 2: Active Reading Hold (`0.6s – 5.2s` / Frames 18–156)**:
   - **Zero Freeze Policy**: Micro-push (`scale: 1.00 → 1.03`) keeps the card breathing.
   - Specular light sheen slides across glass surface (`skewX(-25deg)`).
   - High-contrast readability of data points, Hindi headlines, and portrait badges.
3. **Phase 3: Graceful Exit Transition (`5.2s – 6.0s` / Frames 156–180)**:
   - Graphic smoothly animates out (`scale: 1.03 → 0.90`, `opacity: 1.0 → 0.0`, `translateY: 0 → +30px`).
   - Clean, non-distracting exit with soft motion blur.
4. **Phase 4: Full-Screen Footage & Evidence Reveal (`6.0s to End of Scene`)**:
   - The center screen clears completely.
   - Background image / B-roll blooms into full focus (`opacity: 0.95 - 1.0`, `filter: blur(0px)`).
   - Continuous active Ken Burns camera movement (`pan`, `zoom`, `diagonal_drift`) showcases the full-screen visual evidence, legislative hall, or crowd rally without center obstruction.
   - Subtitle capsule and news ticker continue running undisturbed.

### 6.1 Zero-Static Internal Animation Discipline
A motion graphic card must NEVER be a frozen box with static text:
- **Kinetic Text Ingestion**: Headlines and subheadings enter with staggered upward slides (`translateY: 15px → 0px`, `opacity: 0 → 1`) timed 4–8 frames after the card's outer border snaps in.
- **Inner Media Living Zoom**: Any photograph, portrait, or document nested inside the card must continuously animate with subtle 2.5D push-in zoom (`scale: 1.00 → 1.08`).
- **Dynamic Specular Glare**: A diagonal light sheen (`linear-gradient(90deg, transparent, rgba(255,255,255,0.25), transparent)`) sweeps across the frosted glass every 2.5–3.0 seconds.
- **Data Counter Animation**: Any numbers, votes, percentages, or margins (`+58,206`, `92 seats`, `55%`) must physically count up from 0 to their target value over 20–30 frames.
- **Pulsing Living Elements**: Live indicators (`🔴 LIVE`), border glows, or status tags must softly pulse (`opacity: 0.7 ↔ 1.0`) to maintain a high-tech broadcast atmosphere.

### 6.2 Compulsory Glassmorphic Architecture (The 5-Layer Frosted Glass Law)
Glassmorphism is **strictly compulsory** across 100% of UI cards, dossiers, lower-thirds, and data displays:
1. **Layer 1: Optical Bokeh Backdrop**: `backdropFilter: 'blur(24px) saturate(180%)'` (dynamically blurs underlying B-roll and visual footage into rich, cinematic depth).
2. **Layer 2: Translucent Obsidian Tint**: `backgroundColor: 'rgba(6, 12, 20, 0.78)'` to `rgba(12, 18, 28, 0.84)'` (guarantees 100% text contrast without opaque blocking).
3. **Layer 3: Specular Beveled Rim Highlight**: `boxShadow: 'inset 0 1.5px 0 rgba(255, 255, 255, 0.40)'` and `border: '1px solid rgba(255, 255, 255, 0.14)'` (simulates physical light refraction on thick cut glass).
4. **Layer 4: Active Diagonal Light Sheen**: A continuous light sweep (`linear-gradient(90deg, transparent, rgba(255,255,255,0.22), transparent)` at `skewX(-25deg)`) sliding across the card surface every 2.5–3.0s.
5. **Layer 5: Deep Atmospheric Drop Shadow**: `boxShadow: '0 24px 60px rgba(0, 0, 0, 0.85), 0 0 0 1px rgba(255, 255, 255, 0.12)'` (separates the glass element cleanly from the background).
- **Prohibition on Flat Opaque Blocks**: Never use flat, solid-color rectangular cards (`#000000`, `#FFFFFF`, or flat gray). Every UI container must breathe with optical frosted glass depth.

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

## 8. Complete Motion Graphics & 45 Video Effects Inventory

To achieve broadcast excellence, every scene, hook, and narrative turn must leverage specialized motion graphics and visual effects from the library below, chosen strictly according to script context and audio synchronization.

### 8.1 Motion Graphics Skills Library

| Skill | Description | Primary Editorial Fit |
| :--- | :--- | :--- |
| **`news-video-16x9`** | SOP for producing broadcast-quality 16:9 news investigative videos. | Full-length news investigations, documentary broadcasts. |
| **`motion-art-deco`** | Art Deco gold reveal: centre line, arches, and sunburst. | Premium milestones, commemorative archives, constitutional celebrations. |
| **`motion-ascii-art`** | 3D spinning ASCII torus on a green-phosphor CRT. | Cybersecurity probes, tech/hacking exposés, dark web investigations. |
| **`motion-bauhaus`** | Geometric Bauhaus grid (circles, triangles, stripes). | Bold brand openers, philosophical debates, structured party divisions. |
| **`motion-blueprint`** | Technical blueprint with dashed construction lines. | Investigative mechanisms, quorum voting rules, EVM architecture. |
| **`motion-clay-3d`** | Soft, bouncing 3D clay toys. | Friendly explainers, civic education, lighter political satire. |
| **`motion-comic-book`** | Halftone comic panel with SFX bursts and speed lines. | Dramatic political rivalries, viral punchlines, confrontation beats. |
| **`motion-glassmorphism`**| Frosted-glass UI widgets floating over motion. | Modern HUD data boards, leader profiles, state comparisons. |
| **`motion-gradient-mesh`**| Flowing, warping mesh gradient backgrounds. | Atmospheric interview backdrops, solemn revelations, transition plates. |
| **`motion-halftone`** | Shapes shaded with dot grids (halftone print style). | Editorial print aesthetic, historical retrospectives, retro newsreels. |
| **`motion-holographic`** | Wobbling, iridescent holographic foil ring. | Future-tech, AI policy, intelligence briefings, surveillance tokens. |
| **`motion-isometric`** | Isometric block city with ripple animations. | Urban planning, economic GDP data, real estate scams, infrastructure. |
| **`motion-kinetic-type`**| Punchy, slam-in kinetic typography. | High-impact hooks, breaking news headlines, climax revelations. |
| **`motion-liquid-morph`**| Liquid-chrome metaball blobs with iridescent sheen. | Fluid transitions, tech innovation, speculative political shifting. |
| **`motion-neo-brutalism`**| Neo-brutalist UI: thick borders, hard offset shadows. | High-contrast callouts, statutory warnings, direct audience CTAs. |
| **`motion-neon-glow`** | Flickering, buzzing neon signs. | Nightlife probes, late-night breaking bulletins, neon alerts. |
| **`motion-particles`** | Particle-swarm graphic that forms words or shapes. | Dramatic logo/word reveals, "magic" consensus moments, transitions. |
| **`motion-pixel-art`** | 8-bit dithered pixel-art scenes. | Retro comparisons, gaming/crypto coverage, youth culture beats. |
| **`motion-retro-vhs`** | 80s synthwave VHS aesthetics (neon grids/sunsets). | Historical archival footage, sting operations, covert leaked recordings. |
| **`motion-split-flap`** | Airport-style split-flap departures board. | Live election seat counts, tallies, poll verdict reveals. |
| **`motion-wireframe-3d`**| 3D wireframe objects that draw themselves on screen. | Structural diagrams, institutional hierarchies, complex machinery. |

---

### 8.2 The 45 Video Effects (`/effects`)
You can apply these directly to talking-head footage or b-roll sequences using the `/effects <name>` command or programmatically in Remotion/HyperFrames:

| # | Effect | What it does | Editorial & Narrative Role |
| :--- | :--- | :--- | :--- |
| 1 | `noise` | Reels pile up behind your head | Rapid evidence stacking, press coverage overload |
| 2 | `lineup` | Numbered tiles fan out above your head | Ordered lists, 3-point strategies, priority items |
| 3 | `locked-on` | Brackets lock onto face, camera follows you | High-intensity focus, target investigation, accusatory beats |
| 4 | `orbit` | Reels circle your head | Surrounding media attention, viral buzz, multi-faceted issues |
| 5 | `lean-in` | Quick punch-in on one word | Accentuate shock phrases, startling figures, critical questions |
| 6 | `backdrop-word` | Giant word drops in behind you | Bold conceptual anchoring (e.g. SCAM, VERDICT, ARREST) |
| 7 | `spotlight` | Kill lights, keep you lit | Serious exposés, confidential leaks, somber confessions |
| 8 | `the-bill` | Print instructions like a receipt | Government expenditure, taxpayer costs, broken promises |
| 9 | `moody` | Moody colour grade | Cinematic, tense, investigative atmosphere |
| 10 | `swipe` | Before and after slider | Policy changes, timeline progression, reality vs promise |
| 11 | `todo` | Checklist beside your head | Election manifestos, promised reforms, compliance audits |
| 12 | `comment-box` | Instagram comment types and posts | Public opinion, social media fallout, audience sentiment |
| 13 | `tap` | Follow button flips to Following | Engagement calls, call-to-action moments |
| 14 | `pause-point` | Freeze frame + hand-drawn arrow | Pointing out hidden details, forensic video analysis |
| 15 | `uninstall` | Glitchy uninstall bar breaks frame | Minister resignations, party expulsions, regime collapse |
| 16 | `reel-frame` | Video shrinks into a reel card | Social media virality, quote cards, sharing context |
| 17 | `shortcut-rain` | Keyboard keys rain behind you | Cyber warfare, digital crime, IT infrastructure scandals |
| 18 | `reject-stamp` | Big red stamp slams down | Plea rejections, bail denials, dismissed allegations |
| 19 | `countdown-flip` | 3, 2, 1 flip clock | Countdown to election day, policy deadline, vote results |
| 20 | `rabbit-hole` | Frame tunnels into itself | Deep-dive transitions, complex conspiracy unpacks |
| 21 | `cover-star` | Become a magazine cover | Politician milestones, personality profiles, media fame |
| 22 | `scribble` | Marker doodles draw around you | Informal explainers, pointing out anomalies, sketch notes |
| 23 | `glass-widgets` | Frosted glass floating artifacts | Modern analytical stats, secondary data points |
| 24 | `red-collage` | B&W you, giant red word, slam-in lines | High-alert warnings, scandal headlines, crisis moments |
| 25 | `split-headline` | Headline slides down, pushes you down | Breaking news chyron, newspaper headline analysis |
| 26 | `pastel-word` | Lavender room, giant word, profile card | Soft profile intros, calm transitions, lifestyle angles |
| 27 | `check-pills` | Grid-paper room, blue pills clicked | Sequential verification, evidence vetting, fact checks |
| 28 | `timeline` | Film look with editing timeline | Chronology of events, minute-by-minute crime reconstruction |
| 29 | `headline-box` | Punch-in with two-line headline | High-priority news bulletin delivery |
| 30 | `profile-wall` | Reels grid fills wall with ticker | Broad public reaction, social media blitz, press flurry |
| 31 | `tier-list` | Tier list drops in | Political rankings, candidate viability, policy comparisons |
| 32 | `broll-split` | B-roll on top, you below | Live commentator analysis with concurrent footage |
| 33 | `phone-fan` | Reels fan out like a hand of phones | Multiple leaked video proofs, citizen journalism captures |
| 34 | `dot-reveal` | Shot builds from glowing dots | Tech surveillance, digital reconstruction, identity reveals |
| 35 | `headline-wall` | Headlines pile up, total pops in front | Massive media consensus, aggregation of journalistic proof |
| 36 | `checklist` | Claude task list under your chin | Structured legal arguments, procedural steps, milestones |
| 37 | `liquid-glass-graph` | Liquid glass graph climbs | Inflation rates, unemployment trends, election seat projections |
| 38 | `carousel-spin` | Reels spin in 3D carousel | Surveying multiple news reports or conflicting statements |
| 39 | `match-cut` | News pages cut on one word | Proving unified media narratives across national dailies |
| 40 | `apple-toggles` | iPhone switches flip on | Feature checklist, governance levers, policy implementations |
| 41 | `led-sign` | Glowing LED sign types itself out | Official slogans, bold investigative mottos, night bulletins |
| 42 | `slow-push` | Cinematic push-in, room blur | Dramatic emphasis, emotional gravity, serious moral questions |
| 43 | `over-the-shoulder-zoom` | Corner zoom + liquid glass graph | Side-by-side financial metric or polling margin analysis |
| 44 | `messages` | iMessage notifications pop in | Leaked WhatsApp chats, whistleblower texts, insider memos |
| 45 | `place-in-grid` | Shrink into center of 3x3 grid | Broad contextual landscape, placing the story among peers |

---

### 8.3 Script Scope & Audio Synchronization Integration Law

To ensure video editing achieves television broadcast standards:

1. **Deploy Strictly According to Script Scope & Context**:
   - Never apply random or novelty effects. Every effect and motion graphic must be deliberately chosen to serve the script's editorial message:
     * *Financial/Tax Data* $\rightarrow$ `the-bill`, `liquid-glass-graph`, `over-the-shoulder-zoom`.
     * *Elections & Tallies* $\rightarrow$ `motion-split-flap`, `countdown-flip`, `tier-list`.
     * *Sting Tapes & Leaks* $\rightarrow$ `motion-retro-vhs`, `messages` (leaked chat), `spotlight`.
     * *Court & Rejections* $\rightarrow$ `reject-stamp`, `pause-point`, `motion-blueprint`.
     * *Headlines & Proof* $\rightarrow$ `match-cut`, `headline-wall`, `split-headline`.
     * *Opening Hook / Climax* $\rightarrow$ `motion-kinetic-type`, `lean-in`, `backdrop-word`.
2. **Mandatory Frame-Accurate Audio Synchronization**:
   - Every effect, card entrance, zoom-in, or text reveal MUST trigger on the exact millisecond timecode where the spoken keyword begins in the voiceover (`clean_cues.json` from Whisper).
   - Audio hits (whooshes, stamps, marker squeaks, sub-booms) must sync 1-to-1 with the visual moment of impact.
3. **Pacing & Safe Framing**:
   - Effects run in short, punchy windows (**1.5 to 5.0 seconds** per effect).
   - Keep speaker faces clear and unobstructed (effects sit behind the head or avoid the center safe zone).

---

## 9. Review Gate & Direct Master Render Policy

1. **Pre-Render Review Gate**:
   - Always render storyboard stills across key beats and inspect in HyperFrames studio before launching the full MP4 render.
2. **Direct Master MP4 Output**:
   - All projects render directly to finished, broadcast-ready master `.mp4` video files via Remotion and FFmpeg.
   - Do **NOT** generate Adobe Premiere Pro project files (`.prproj`) or XML interchange files (`.xml`) unless specifically requested by the user.
