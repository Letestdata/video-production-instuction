---
name: news-shorts-reel
description: High-velocity faceless investigative news shorts and reels in 9:16 (1080x1920) and 1:1 (1080x1080). Standardizes the signature indiainlast24hr editing style: 1.5–2.8s visual shifts, GeoLayers 3D satellite cartography, 3D paper dossiers with synced marker highlights, motion glassmorphism HUDs, kinetic slam hooks, technical blueprints, split-flap tally boards, retro VHS sting windows, and a 4-track tactile audio stack with dynamic VO ducking.
---

# News Shorts & Reels Production Skill (9:16 & 1:1)

This skill governs the production of high-velocity, faceless investigative news shorts and reels in **9:16 Vertical (`1080×1920`)** and **1:1 Square (`1080×1080`)** formats, enforcing the documentary-grade visual pace, tactile sound design, and motion physics of the **`indiainlast24hr`** editing style.

---

## 1. Technical Production Specifications

| Specification | 9:16 Vertical Short / Reel | 1:1 Square Feed Video |
| :--- | :--- | :--- |
| **Canvas Dimensions** | `1080 × 1920 px` | `1080 × 1080 px` |
| **Frame Rate** | `30 FPS` (Deterministic frame-exact rendering) | `30 FPS` |
| **Duration Target** | **35 – 50 seconds** (Viral sweet spot; max 58s) | `30 – 50 seconds` |
| **Word Count & Pace** | 85 – 125 words at ~2.4 words/second | 75 – 120 words |
| **Visual Shift Rate** | Every **1.8 – 2.8 seconds** (Strictly enforced) | Every 1.8 – 2.8 seconds |
| **Subtitle Policy** | **Zero bottom-screen karaoke word captions**; 2–4 word center phrases only | Same |
| **Typography Pairing** | `Baloo Bhai 2` (Devanagari, 800/900) + `Montserrat` / `Inter` (Latin/Numbers) | Same |
| **Brand Color Palette** | Obsidian (`#060102`), White (`#FFFFFF`), Alert Crimson (`#FF1E27`), Cyan (`#00E5FF`), Gold (`#FFD700`) | Same |
| **Master Delivery** | Direct master `.mp4` (H.264, AAC 48kHz, CRF 18). **No Premiere Pro / XML files**. | Same |

---

## 2. Layout & Safe Margin Contracts

### 9:16 Vertical Canvas (`1080 × 1920 px`):
- **Top Safe Zone (`0 – 180 px`)**: Reserved for broadcast watermark bug (`NEWS FAIR` pill at `top: 36px, left: 40px`). No critical text or face focus.
- **Primary Content Viewport (`Y: 220 px – 1480 px`)**: 100% of dossiers, maps, split-screen docks, and stat cards must sit within this window.
- **Right Engagement Margin (`X: 950 – 1080 px` from `Y: 900 – 1650 px`)**: Keep clear of right-aligned text (Instagram/YouTube Like, Comment, Share buttons overlay here).
- **Bottom Dead Zone (`1640 – 1920 px`)**: Reserved for platform title, handle, audio badge, and timeline scrubber bar.

### 1:1 Square Canvas (`1080 × 1080 px`):
- **Padding**: Uniform `60 px` inner margin on all four boundaries (`center stage: 960 × 960 px`).

---

## 3. Audio Architecture & The 4-Track System

Every cut, card entrance, and document reveal must be driven by an audio trigger. Silent visual shifts are prohibited.

| Track Layer | Target Level | Processing & Role | Audio Asset / File |
| :--- | :--- | :--- | :--- |
| **Track 1: Voiceover (VO)** | `-1.0 dB` peak | Hyper-compressed, dry, zero dead-air pauses. `rate=+14% to +18%`, pitch `+2Hz`. | `hi-IN-MadhurNeural` or Studio WAV |
| **Track 2: Ambient BGM Bed** | `-18 dB to -22 dB` | Dark, driving 120–128 BPM analog synth pulse. Low-pass filter at 3.2 kHz. Cut to instant silence on punchlines. | `bgm_investigation_pulse.wav` |
| **Track 3: Tactile Foley** | `-6 dB to -10 dB` | Realistic physical sounds: paper rustle, felt marker squeak, mechanical flip clacks, camera clicks. | Sourced from `D:\Phone data\Sound Effects` |
| **Track 4: Sub-Bass Hits & Risers** | `-4 dB to -8 dB` | Deep sub-bass booms (`60Hz`), rubber stamp thuds, and whoosh sweeps on cuts. | Sourced from `D:\Phone data\Sound Effects` |

> [!IMPORTANT]
> **Remotion Audio Safety Rule**: Every audio cue must be wrapped in its own `<Sequence from={frame} durationInFrames={dur}>` to prevent premature cutoff after a single frame.

---

## 4. The 7 Visual Motion Archetypes

Rather than relying on flat text slides, every scene in a 9:16 short must be cast into one of these 7 visual archetypes:

### Archetype 1: Kinetic Typo Slam Hook (`0:00 – 0:03`)
- **Use For**: Opening 2.5-second conflict hook.
- **Motion Physics**: Words scale in from `220%` down to `100%` in `0.12s` with elastic squash & stretch (`damping: 10, stiffness: 280`).
- **Color Cycling**: Alternates between Alert Crimson (`#FF1E27`) and Pure White on deep obsidian.
- **Punchline Echo**: Final punch word lands with a 4-layer outlined echo stack cascading downward into depth with a continuous camera push-in.
- **Audio Hit**: Fast air swish (`sfx_fast_swish.wav`) per word + heavy sub boom (`sfx_sub_boom.wav`) on final impact.

### Archetype 2: 3D Paper Dossier with Synced Marker
- **Use For**: Leaked intelligence, FIR reports, police tip-offs, official press releases.
- **Physical Realism**: $15^\circ$ Dutch angle tilt, newsprint fold crease, authentic publication masthead, and drop shadow.
- **Synced Highlighter**: Bright yellow (`rgba(255, 235, 59, 0.5)`) felt-tip marker bar wipes left-to-right across the punchline, synchronized with stereo marker squeak SFX (`sfx_marker_squeak.wav`).

### Archetype 3: GeoLayers 3D Satellite Cartography
- **Use For**: Cross-border foreign influence, territorial movements, geopolitical funding.
- **Cartography Contract**: $35^\circ$ tilted NASA Blue Marble terrain; desaturated base.
- **Vector Borders**: Emissive glowing border trace (Crimson for threat, Cyan for diplomacy, Green for foreign territory).
- **Active Telemetry**: Sweeping radar arc, pulsing drop pins, and animated marching-ants dotted trajectory lines (`sfx_laser_trace.wav`).

### Archetype 4: Motion Glassmorphism HUD Docks
- **Use For**: Dual-agency comparison docks (Shin Bet vs Mossad / CBI vs ED), diplomatic profile cards, and interactive poll outros.
- **5-Layer Glass Contract**:
  1. `backdropFilter: 'blur(24px) saturate(170%)'` (softens B-roll into cinematic bokeh).
  2. Translucent dark tint: `rgba(10, 16, 26, 0.72)`.
  3. Specular rim highlight: `boxShadow: inset 0 1.5px 0 rgba(255, 255, 255, 0.55)`.
  4. Moving light sheen bar sliding across surface at `skewX(-25deg)`.
  5. Floating sine elevation (`translateY: Math.sin(...) * 8px`) over ambient moving color blobs.

### Archetype 5: Technical Mechanism Blueprints
- **Use For**: Explaining EVM tampering mechanisms, ballot box logistics, money laundering networks, and cyber interception.
- **Blueprint Aesthetic**: Deep CAD blueprint navy (`#1453A8`), white construction grid, dashed radius circles in light blue (`#9EC5FF`), and yellow (`#FFD84A`) dimension callouts (`Ø`, angles).
- **Mechanical Action**: Interconnected meshed gears rotate in opposing directions at exact mathematical ratios.

### Archetype 6: Mechanical Split-Flap Tally Boards
- **Use For**: Live vote counts, breaking arrest totals, currency amounts, and final verdicts.
- **Flip Motion**: Airport departure board with hairline split flaps (`#1D1D21`) and cream characters (`#F5F1E6`).
- **Wave Transition**: Cells flip through 8–16 characters at `55ms/flip` in a cascading left-to-right, top-to-bottom wave with mechanical clatter SFX, locking into the final status (`ARRESTED`, `DENIED`, `LEAD`).

### Archetype 7: Retro VHS Surveillance Window
- **Use For**: Sting operations, leaked undercover phone recordings, and clandestine archives.
- **Surveillance Filter**: Red/blue chromatic aberration split, CRT scanlines, horizontal tracking band jitter, and monospaced OSD (`PLAY ▶`, flashing `REC ●`, millisecond running timecode).

---

## 5. Editorial Discipline & Quality Laws

1. **The Mandatory Pre-Production Asset Pass**:
   - Extract every named entity (politician, agency, law, currency amount, coordinate) before coding.
   - Hierarchy of Evidence: Scanned document / receipt > Official vector emblem > Verified portrait cutout > Real stock B-roll plate > Zero pictograms or emojis.
2. **Zero Empty Vector Backdrops**:
   - Never float graphics on empty black or red slides. Beneath every card, place desaturated real-world B-roll footage, satellite terrain, or dynamic ambient color blobs.
3. **The 2.0-Second Visual Shift Law**:
   - Every 1.8–2.8 seconds, the frame must change (camera angle shift, document slide, new stat card, or snap zoom).
4. **Continuous Camera Motion**:
   - Every asset must feature continuous slow 2.5D push-in zoom (`100% → 112%`) paired with subtle sine-wave floating. Zero frozen frames.
5. **Direct Master MP4 Output**:
   - Deliver finished master videos (`.mp4`, 1080×1920 @ 30 FPS). Do not generate Premiere Pro (`.prproj`) or XML interchange files unless specifically requested.

---

## 6. Remotion Component Reference

All production components are modular and maintained in `reels-engine/src/`:

| Component | Role | Key Props |
| :--- | :--- | :--- |
| `RedPillCard` | Red capsule stat callouts (1–3 power words) | `text`, `subtext`, `enterFrame`, `color` |
| `KineticSlamHook` | Syllable-by-syllable typographic opening hook | `words[]`, `accentColor`, `enterFrame` |
| `TextHighlighter` | 3D paper dossier with animated marker highlight | `headline`, `highlightText`, `source`, `tiltDeg` |
| `StatusStamp` | Distressed rubber stamp slam with screen shake | `status`, `substatus`, `enterFrame`, `color` |
| `GlassmorphicCard` | Frosted glass container with moving specular sheen | `width`, `height`, `borderColor`, `glowColor` |
| `GlassmorphicBlobsBackdrop` | Ambient moving radial color blobs backdrop | `blobs[]` (coordinates, color, radius) |
| `GlassmorphicPollWidget` | Interactive outro poll with live filling progress bar | `question`, `option`, `targetPercent`, `enterFrame` |
| `GeoLayersMap` | 3D satellite cartography with vector border glow | `center`, `tiltDeg`, `countries[]`, `radar` |
