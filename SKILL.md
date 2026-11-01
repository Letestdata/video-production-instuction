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
| **Compulsory Glassmorphism** | **MANDATORY ACROSS ALL CARDS & HUDs**: 100% of dossiers, stat cards, comparison docks, and poll widgets must use the 5-layer frosted glass contract (`backdropFilter: blur(24px) saturate(170%)`, specular rim highlight, sheen sweep). Flat opaque cards are strictly prohibited. | Same |
| **Universal Motion & 3D Animation** | **MANDATORY NON-STATIC & 3D PHYSICS**: Zero static elements allowed. Every image must have continuous Ken Burns scale/pan/drift. Every motion graphic must feature active 3D transforms (`perspective`, `rotateX/Y/Z`), continuous floating sine waves, and moving specular highlights. Above all must NEVER be static. | Same |
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

### Archetype 4: Motion Glassmorphism HUD Docks (Compulsory UI Standard)
- **Compulsory Requirement**: All floating UI elements, stat cards, dual-agency comparison docks (Shin Bet vs Mossad / CBI vs ED), diplomatic profile cards, and interactive poll outros MUST be rendered using the 5-layer frosted glass contract. Flat opaque plastic rectangles are strictly forbidden.
- **5-Layer Glass Contract**:
  1. `backdropFilter: 'blur(24px) saturate(170%)'` (softens B-roll into cinematic optical bokeh).
  2. Translucent dark tint: `rgba(10, 16, 26, 0.72)` to `rgba(6, 12, 20, 0.82)` (preserves contrast while retaining translucency).
  3. Specular rim highlight: `boxShadow: inset 0 1.5px 0 rgba(255, 255, 255, 0.55)` and `border: 1px solid rgba(255, 255, 255, 0.16)`.
  4. Moving light sheen bar sliding across surface at `skewX(-25deg)` every 2.5–3.0s.
  5. Floating sine elevation (`translateY: Math.sin(...) * 8px`) over ambient moving radial color blobs.

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
6. **The Text Legibility & Contrast Law (Zero Obscured / Unreadable Text)**:
   - Spoken words, numbers, and data points must maintain strict contrast against all background motion.
   - High-contrast color pairings are mandatory: pure white (`#FFFFFF`) or amber gold (`#FFD700`) on dark or frosted glass backgrounds; dark obsidian (`#060102`) on light paper dossiers.
   - Multi-layer drop shadows (`textShadow: '0 2px 8px rgba(0,0,0,0.85), 0 0 1px rgba(0,0,0,0.9)'`) or contrast bounding capsules are mandatory to prevent text from washing out when bright dynamic b-roll or color blobs pass underneath.
   - Never allow portraits, HUD borders, or secondary badges to overlap, clip, or occlude primary text.
7. **Color Grading & Visual Cleanliness Standard**:
   - Maintain uniform color temperature, exposure, and saturation across all b-roll plates, cutouts, and synthetic backdrops.
   - Ensure clean color balance without crushed shadows, blown highlights, or muddy compression artifacts.
8. **Noise Management & Stylistic Texture Isolation**:
   - All visual noise, banding, and unintended distortion must be suppressed. Low-resolution or grainy source footage must be de-noised.
   - Stylistic textures (e.g., retro VHS noise, CRT scanlines, halftone dots) must remain strictly confined to background or accent layers—never allow noise overlays to degrade foreground text clarity or data counters.
9. **Universal Non-Static Animation Mandate (Above All Must NOT Be Static)**:
   - **Zero Static Images**: Every single image, leader portrait, paper document, and background plate must have active, continuous motion (continuous Ken Burns push-in/pull-out `scale: 1.05 → 1.18`, subtle positional drift, or parallax shift). A completely frozen still image is strictly prohibited.
   - **Zero Static Motion Graphics**: Every card, HUD dock, data counter, bar chart, split-flap board, and poll widget must maintain living animation throughout its lifespan—continuous floating sine elevation (`translateY: Math.sin(frame / 15) * 8px`), gentle breathing scale, rotating telemetry dials, or sweeping light sheens. Elements must never enter and lock into a frozen state.
10. **3D Motion & Perspective Depth Physics Mandate**:
    - All scenes must enforce authentic 3D spatial staging using CSS 3D transforms (`perspective: 1200px`, `transformStyle: 'preserve-3d'`).
    - Incorporate dynamic 3D multi-axis rotations (`rotateX`, `rotateY`, `rotateZ`, `translateZ`) on entrance, hold, and exit.
    - Multi-plane 3D parallax: background footage, midground frosted glass docks (`translateZ(30px)`), floating data badges (`translateZ(60px)`), and foreground status stamps (`translateZ(90px)`) must move at independent depth speeds to create a tactile 3D physical documentary look.

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

---

## 7. Complete Motion Graphics & 45 Video Effects Inventory

To maximize engagement and velocity, every narrative shift, hook, and evidence reveal must leverage specialized motion graphics and visual effects from the library below, chosen strictly according to script context and audio synchronization.

### 7.1 Motion Graphics Skills Library

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

### 7.2 The 45 Video Effects (`/effects`)
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

### 7.3 Script Scope & Audio Synchronization Integration Law

To ensure 9:16 Shorts & Reels maintain the signature `indiainlast24hr` high-velocity visual impact:

1. **Deploy Strictly According to Script Scope & Context**:
   - Every effect and motion archetype must serve the exact editorial need of the spoken moment:
     * *Financial/Tax Data* $\rightarrow$ `the-bill`, `liquid-glass-graph`, `over-the-shoulder-zoom`.
     * *Elections & Tallies* $\rightarrow$ `motion-split-flap`, `countdown-flip`, `tier-list`.
     * *Sting Tapes & Leaks* $\rightarrow$ `motion-retro-vhs`, `messages` (leaked WhatsApp), `spotlight`.
     * *Court & Rejections* $\rightarrow$ `reject-stamp`, `pause-point`, `motion-blueprint`.
     * *Headlines & Proof* $\rightarrow$ `match-cut`, `headline-wall`, `split-headline`.
     * *Opening Hook / Climax* $\rightarrow$ `motion-kinetic-type`, `lean-in`, `backdrop-word`.
2. **Mandatory Frame-Accurate Audio Synchronization**:
   - Every effect, card entrance, zoom-in, or text reveal MUST trigger on the exact millisecond timecode where the spoken keyword begins in the voiceover (`clean_cues.json` from Whisper).
   - Audio hits (whooshes, stamps, marker squeaks, sub-booms) must sync 1-to-1 with the visual moment of impact.
3. **Pacing & Safe Framing**:
   - Effects run in short, punchy windows (**1.5 to 3.5 seconds** per effect).
   - In 9:16 vertical videos, keep all key visuals and effects inside the **Primary Content Viewport (`Y: 220px – 1480px`)** and clear of the right engagement button column (`X: 950–1080px`). Never cover the speaker's face.

---

## 8. Technical Review, Defect Prevention & Frame Audit SOP

To guarantee that every short meets broadcast visual standards and passes technical quality review, apply the following defect prevention instructions and frame-by-frame audit protocol before final delivery:

### 8.1 Technical Review Target Specifications
- **Video Standard**: `1080 × 1920 px` (9:16 portrait) at `30 FPS`, H.264 master container.
- **Audio Standards**:
  - Peak Voiceover Volume: `-1.0 dB to -2.8 dB` (clean limiter, zero digital clipping).
  - Average Integrated Loudness: `-20 dB to -24 dB` LUFS / RMS.
  - Stereo balance: Clean channel separation, dynamic VO ducking over BGM and tactile SFX.

### 8.2 Defect Prevention Rules (Root Cause & Fix Instructions)

| Defect / Quality Issue | Root Cause | Mandatory Instruction & Fix |
| :--- | :--- | :--- |
| **Blocked / Obscured Text** | Foreground card, portrait cutout, or badge encroaching on text bounding box. | • Reposition elements or increase vertical padding.<br>• Enforce strict z-index hierarchy (`z-index: 50+` for primary typography).<br>• Lock text strictly within the Primary Viewport (`Y: 220px – 1480px`). |
| **Unreadable Text / Low Contrast** | Text color blending into bright or busy background; insufficient text shadow. | • Apply high-contrast text styling (White `#FFFFFF` or Amber Gold `#FFD700` on dark backgrounds).<br>• Add multi-layer text shadows: `textShadow: '0 3px 12px rgba(0,0,0,0.9), 0 1px 2px rgba(0,0,0,0.95)'`.<br>• Back text with a frosted glass capsule (`backdropFilter: 'blur(20px)'`). |
| **Visual Noise & Distortion** | Low-bitrate source footage, aggressive scaling, or unconstrained stylistic noise filters. | • Apply de-noising to grainy source assets before import.<br>• Confine noise/scanline filters strictly behind text layers.<br>• Maintain clean, anti-aliased vector rendering and smooth gradient dithering. |
| **Color Imbalance / Inconsistent Grading** | Disparate source footage clashing in saturation, contrast, or tint. | • Normalize color balance and exposure across all footage.<br>• Apply a unified LUT / tone grade (cinematic high-contrast dark palette with controlled saturation). |

### 8.3 Frame-by-Frame Quality Audit Protocol (By Narrative Acts)

Every render must undergo a systematic 4-phase frame audit:

1. **Act 1: Hook & Opening Punch (Frames 0 – 600 / 0:00 – 0:20)**:
   - ✅ Verify kinetic typography slam hook impact, rapid word zoom physics, and sub-boom synchronization.
   - ✅ Confirm opening dossier reveal and highlighter wipe alignment with voiceover.
2. **Act 2: Mid-Section Data, Seats & Tallies (Frames 600 – 1050 / 0:20 – 0:35)**:
   - ⚠️ **Critical Audit Zone**: Inspect frames at ~0:25 and ~0:30 for text clarity and data readability.
   - ✅ Check split-flap tally boards and liquid graphs: numbers, party labels, and status badges must be 100% sharp and readable.
   - ✅ Ensure no overlapping card borders or badges block or shadow the text.
3. **Act 3: Comparison Grids, Evidence & Transitions (Frames 1050 – 1400 / 0:35 – 0:45)**:
   - ⚠️ **Critical Audit Zone**: Inspect comparison cards, stamps, and B-roll plates for visual noise and distortion.
   - ✅ Confirm seamless color grading consistency across all party comparison bars and photographic assets.
   - ✅ Verify that red status stamps ("LANDSLIDE VICTORY!", "REJECTED") slam cleanly without clipping boundary borders.
4. **Act 4: Institutional Blueprint, Climax & Community Poll Outro (Frames 1400 – 1744 / 0:45 – 0:58)**:
   - ✅ Verify CAD blueprint gear rotation and demographic node clarity.
   - ✅ Confirm interactive poll widget options and percentage bars render inside safe zone (`Y: 220px – 1480px`).
   - ✅ Verify complete clearance from platform right-hand engagement controls (`X: 950–1080px`) and bottom scrubber.

### 8.4 Post-Render Verification & Re-Extraction Protocol
1. **Automated Still Extraction**:
   - Extract verification frame stills across all four acts (e.g., Frames 100, 250, 650, 950, 1250, 1680).
2. **Visual Inspection**:
   - Visually inspect mid-section stills (specifically checking Frames 25, 30, and 35–45 equivalents) for zero text blockage, razor-sharp contrast, and noise-free image quality.
3. **Master Sign-Off**:
   - Only declare the Master MP4 approved when all text is 100% legible, audio peaks comply with broadcast limits (`-1.0 dB to -2.8 dB`), and visual pacing adheres strictly to the 1.8–2.8s shift rule.
