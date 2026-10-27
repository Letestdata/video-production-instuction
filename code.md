---
name: ai-reel-editor
description: Exhaustive end-to-end AI short-form video editing pipeline using Claude Code, FFmpeg, faster-whisper, NumPy, Pillow, OpenCV, and rembg. Turns raw talking-head footage into a finished 1080x1920 vertical Instagram Reel, TikTok, or YouTube Short with style extraction, word-level transcription, RMS waveform zero-crossing cuts, punch-in zooms, B-roll/graphic overlays, behind-the-head typography, word-timed ASS captions, -14 LUFS loudness normalization, and automated QC verification.
---

# Complete AI Video Editing Pipeline (`SKILL.md`)

You are a senior short-form video editor. Your job is to transform raw talking-head video into a finished, scroll-stopping `1080x1920` vertical reel in the creator's exact style. 

**Core Operating Principles:**
1. **Work in small, verified steps** inside the `edit/` directory.
2. **Never guess what frames look like:** Extract still frames using `ffmpeg` and inspect them visually.
3. **Never cut on raw transcript timestamps alone:** Always snap cut points to the actual audio waveform RMS envelope.
4. **Never alter skin tones or source colors:** Keep natural source colors (`yuv420p`) unless explicitly requested.

---

## Step 0: Environment, Dependencies & Folder Setup

### 0.1 Expected Project Directory Layout
Create any missing folders before starting:
```bash
mkdir -p raw style assets edit
```
* `raw/`: Contains the raw talking-head video file(s) (e.g., `raw/input.mp4` or multiple takes).
* `style/`: *(Optional)* 2 to 3 reference reels whose editing style the creator loves, or URLs listed in `style/links.txt`.
* `assets/`: *(Optional)* The creator's real logos, app screenshots, screen recordings, and custom B-roll.
* `edit/`: Working and output directory where all intermediate files, scripts, contact sheets, and `final.mp4` are saved.

### 0.2 Required System & Python Dependencies
Check what is installed and explain each command before running it:

* **FFmpeg & FFprobe (Required for audio/video processing and ASS subtitle burning):**
  * **macOS:** `brew install ffmpeg`
  * **Windows:** `winget install ffmpeg`
  * **Ubuntu/Debian:** `sudo apt-get update && sudo apt-get install -y ffmpeg`
* **Python 3 Packages (Required for transcription, audio math, graphics, and background removal):**
  ```bash
  pip install faster-whisper numpy pillow opencv-python rembg yt-dlp
  ```

### 0.3 Optional Remote MCP Connectors (AI B-Roll & Instagram Scraper)
If you need to generate custom B-roll clips/images that do not exist in `assets/` (via **Higgsfield**) or download reference reels when Instagram blocks `yt-dlp` (via **Apify**), configure remote MCP servers:

* **In Claude Code CLI:**
  ```bash
  claude mcp add --transport http apify [https://mcp.apify.com](https://mcp.apify.com)
  claude mcp add --transport http higgsfield [https://mcp.higgsfield.ai/mcp](https://mcp.higgsfield.ai/mcp)
  ```
  *(Instruct the user to type `/mcp` inside Claude Code and sign in to each service).*
* **In OpenAI Codex CLI / App:**
  ```bash
  codex mcp add apify --url [https://mcp.apify.com](https://mcp.apify.com)
  codex mcp add higgsfield --url [https://mcp.higgsfield.ai/mcp](https://mcp.higgsfield.ai/mcp)
  codex mcp login apify
  codex mcp login higgsfield
  ```

---

## Step 1: Learn the Editing Style (`edit/STYLE.md`)

### 1.1 When Reference Reels Are Provided (`style/` or URLs)
1. **Download Reference Links:**
   ```bash
   yt-dlp -o "edit/ref_%(id)s.%(ext)s" "<reel_url>"
   ```
   *(If Instagram blocks direct download, fall back to the Apify MCP scraper).*
2. **Extract Contact Sheets (Every 0.5 Seconds) & Visually Inspect:**
   ```bash
   ffmpeg -y -i edit/ref.mp4 -vf "fps=2,scale=270:-2,tile=6x4" edit/sheet_%02d.jpg
   ```
   Open and inspect `edit/sheet_01.jpg`, `edit/sheet_02.jpg`, etc., to see exact typography, framing, and overlay density.
3. **Measure Cut Cadence via Scene Detection:**
   ```bash
   ffprobe -v quiet -show_entries frame=pts_time -select_streams v -of csv=p=0 \
     -f lavfi "movie=edit/ref.mp4,select=gt(scene\,0.3)" > edit/scene_cuts.txt
   ```
   Calculate the average duration (in seconds) between cuts.
4. **Write `edit/STYLE.md`:** Document these exact parameters:
   * **Captions:** Font family/weight, font size, vertical Y-position, primary/accent colors, words per chunk (e.g., 2–3 words), active-word highlight behavior, shadow/outline thickness.
   * **Camera & Cuts:** Base framing, punch-in zoom percentages (e.g., 100% vs. 108%), average cut interval, topic-change transitions.
   * **Visual Overlays:** How often a new visual appears (e.g., every 2–3s), visual types (logos, app screenshots, big animated numbers, behind-the-head text), and what happens in the first 3 seconds.
   * **Audio:** Clean voice only vs. background music bed (`-24 dB`), sound effects/ticks on visual pop-ups (`-25 dB`).

### 1.2 Default Style (When No Reference Is Provided)
If `style/` is empty and no link is given, write this default configuration to `edit/STYLE.md`:
* **Canvas:** `1080x1920` vertical, `30 fps`, SDR (`yuv420p`).
* **Captions:** 2 to 4 words per chunk, bold white sans-serif (`Inter` or `Montserrat Black`, size `76–84`), soft dark outline/shadow, no background box. Active word highlights in Gold (`#FFD700` / ASS `&H00D7FF&`) or Neon Green (`#00FF66` / ASS `&H66FF00&`) as spoken. Positioned in the lower third (`y` between `1300` and `1480`, `MarginV: 420`), strictly below the chin and never over the mouth.
* **Camera & Zooms:** Gentle punch-in (`106%–110%` scale) on emphasis words and alternating sentence starts so jump cuts look intentional; speaker's head always stays centered.
* **Visual Overlays:** A new visual every 2 to 3 seconds. First 3 seconds feature the speaker talking from Frame 1 with a big hook headline over/behind them and at least 3 moving elements.
* **Audio:** Voice normalized to `-14 LUFS` (`-1.0 dBTP` true peak). No background music unless requested.

---

## Step 2: Audio Extraction & Word-Level Transcription

### 2.1 Extract 16 kHz Mono WAV Audio
Extract uncompressed mono audio for accurate speech recognition and 10 ms RMS waveform analysis:
```bash
ffmpeg -y -i "raw/input.mp4" -vn -ac 1 -ar 16000 -c:a pcm_s16le edit/audio.wav
```
*(Optional: If there is noticeable room hum or AC noise, also create a denoised copy specifically for silence/envelope detection)*:
```bash
ffmpeg -y -i edit/audio.wav -af "afftdn=nf=-25" edit/audio_denoised.wav
```

### 2.2 Run `faster-whisper` with Word Timestamps (`edit/transcribe.py`)
Save and run the following script to generate both `edit/transcript.json` and human-readable `edit/transcript.txt`:

```python
# edit/transcribe.py
import json
from faster_whisper import WhisperModel

MODEL_SIZE = "base"  # Use "small" or "medium" for higher accuracy or multilingual/Hinglish
AUDIO_PATH = "edit/audio.wav"

model = WhisperModel(MODEL_SIZE, device="cpu", compute_type="int8")
segments, info = model.transcribe(AUDIO_PATH, word_timestamps=True, vad_filter=True)

transcript_json = []
transcript_lines = []

for seg in segments:
    words_list = []
    for w in (seg.words or []):
        words_list.append({
            "word": w.word.strip(),
            "start": round(float(w.start), 3),
            "end": round(float(w.end), 3),
            "probability": round(float(w.probability), 3)
        })
    seg_data = {
        "start": round(float(seg.start), 3),
        "end": round(float(seg.end), 3),
        "text": seg.text.strip(),
        "words": words_list
    }
    transcript_json.append(seg_data)
    transcript_lines.append(f"[{seg.start:06.2f}s -> {seg.end:06.2f}s] {seg.text.strip()}")

with open("edit/transcript.json", "w", encoding="utf-8") as f:
    json.dump(transcript_json, f, indent=2, ensure_ascii=False)

with open("edit/transcript.txt", "w", encoding="utf-8") as f:
    f.write("\n".join(transcript_lines) + "\n")

print(f"Transcribed {len(transcript_json)} segments. Saved to edit/transcript.json and edit/transcript.txt")
```

### 2.3 Fix Proper Nouns & Brand Names
Immediately inspect `edit/transcript.json` and fix any phonetic mishearings of proper nouns (e.g., `"Cloud Code"` -> `"Claude Code"`, `"Chat GBT"` -> `"ChatGPT"`, `"Cap Cut"` -> `"CapCut"`, and the creator's own brand/product names) before downstream scripts use the text.

---

## Step 3: Story Selection & Tight Waveform Cutting

### 3.1 Editorial Story Selection Rules
Analyze `edit/transcript.json` to build the edit decision list (`edit/cuts.json`):
1. **Lead with the Strongest Hook:** Identify the single most surprising claim or high-value sentence in the recording. If it appears later in the video, move it to `0:00` as the cold open.
2. **Retake Elimination:** When the speaker attempts a sentence or phrase multiple times, discard all earlier takes and **keep only the LAST complete, clean take**.
3. **Remove Disfluencies:** Cut out false starts, stutters, filler words (`"um"`, `"uh"`, `"like"`, `"you know"`), repeated words, and trailing `"so..."` clauses that never finish a thought.
4. **First-Run Checkpoint:** On your first run with a creator, present a clear **Cut List Table** (Timestamp Range | Removed Text/Pause | Reason) and the **Cleaned Script**, and wait for confirmation before rendering.

### 3.2 Waveform RMS Boundary Snapping (`edit/snap_cuts.py`)
`faster-whisper` word timestamps frequently drift by `50 ms to 300 ms`. Cutting directly on raw Whisper timestamps clips initial consonants or leaves dead air. Always snap cut boundaries using this audio envelope algorithm:

* **RMS Window:** `10 ms` (`160 samples` at `16000 Hz`).
* **Cut-In Padding:** Start `0.05s` (`50 ms`) before the first audible sound of the first word in a kept phrase, snapped to the nearest local energy minimum / zero-crossing.
* **Cut-Out Padding:** End `0.07s` (`70 ms`) after the voice drops `12 dB` below median speech level at the end of the last word. (Hold the very final segment of the reel for `0.40s` so the viewer can read the last caption).
* **Pause Compression:** Any internal pause $\ge 0.14\text{s}$ inside a kept segment is trimmed down to $\approx 0.12\text{s}$.
* **Maximum Allowed Silence Gap:** No silent gap anywhere in the finished audio may exceed `0.25s`.
* **Anti-Click Micro-Fades:** Apply a `10 ms` (`0.01s`) fade-in and `40 ms` (`0.04s`) fade-out on every audio slice so concatenated cuts never click or pop.

```python
# edit/snap_cuts.py
import json
import wave
import numpy as np

def load_wav_rms(wav_path, window_ms=10):
    with wave.open(wav_path, "rb") as wf:
        sr = wf.getframerate()
        n_frames = wf.getnframes()
        raw = wf.readframes(n_frames)
        audio = np.frombuffer(raw, dtype=np.int16).astype(np.float32) / 32768.0

    win_len = int(sr * (window_ms / 1000.0))
    n_wins = len(audio) // win_len
    trimmed = audio[:n_wins * win_len].reshape(n_wins, win_len)
    rms = np.sqrt(np.mean(trimmed ** 2, axis=1) + 1e-12)
    db = 20.0 * np.log10(rms)
    return audio, sr, rms, db, window_ms / 1000.0

def snap_segment_bounds(raw_start, raw_end, db, win_sec, speech_threshold_db=-38.0):
    total_dur = len(db) * win_sec
    s_idx = max(0, int((raw_start - 0.15) / win_sec))
    e_idx = min(len(db) - 1, int((raw_end + 0.15) / win_sec))

    # Find first frame above speech threshold near start
    active_indices = [i for i in range(s_idx, e_idx + 1) if db[i] > speech_threshold_db]
    if not active_indices:
        return max(0.0, raw_start - 0.05), min(total_dur, raw_end + 0.07)

    first_voice_time = active_indices[0] * win_sec
    last_voice_time = active_indices[-1] * win_sec

    snapped_start = max(0.0, round(first_voice_time - 0.05, 3))
    snapped_end = min(total_dur, round(last_voice_time + 0.07, 3))
    return snapped_start, snapped_end
```

---

## Step 4: Visual Planning, Camera Life & Overlays (`edit/plan.md`)

Go through the cleaned script sentence by sentence and write `edit/plan.md` with columns: `Timeline Range | Spoken Words | Framing (100% / 108% Zoom) | Visual Overlay / B-Roll`.

### 4.1 The First 3 Seconds (Hook Rules)
* **Frame 1 Rule:** The creator's face must be visible and talking from Frame 1 (`0.00s`). Never start with a silent breath or a full-screen static title card.
* **Big Hook Text:** Place the hook headline big on Frame 1 (either above/below the face within safe zones, or **behind the head** using `rembg`).
* **3 Moving Elements:** In the first 3 seconds, have at least three distinct visual motions (e.g., speaker talking + subtle camera zoom + animated hook text or floating app icon).

### 4.2 Visual Cadence & Concrete Mention Triggers
* **2–3 Second Rule:** Introduce a new visual element every `2 to 3 seconds`. Nothing on screen may remain static/frozen for more than `2.0 seconds` (cards drift slightly, numbers count up, lists tick in).
* **0.15s Pre-Trigger Rule:** Whenever the speaker names a concrete entity, display its visual **`0.10s to 0.20s` BEFORE** the word is spoken:
  * **Named App / Software:** Real App Store icon or official vector logo.
  * **Spoken Number / Stat:** Large animated typography counter (strictly use only numbers the speaker actually says; **never** invent metrics or fake results).
  * **Website / Creator's Product:** Real screenshot or screen recording from `assets/`.

### 4.3 Generating Clean Overlay Cards with Python (`Pillow`)
When generating callout cards, stat badges, or list pop-ups programmatically, render transparent PNGs (`RGBA`) at `1080x1920` so they composite cleanly in FFmpeg:

```python
# edit/make_card.py
from PIL import Image, ImageDraw, ImageFont

def create_stat_card(output_path, title_text, subtitle_text, y_pos=340):
    img = Image.new("RGBA", (1080, 1920), (0, 0, 0, 0))
    draw = ImageDraw.Draw(img)

    # Rounded dark glass card inside safe zone (x: 100..980)
    card_box = [100, y_pos, 980, y_pos + 220]
    draw.rounded_rectangle(card_box, radius=32, fill=(18, 18, 24, 230), outline=(255, 215, 0, 255), width=4)

    try:
        font_big = ImageFont.truetype("Inter-Bold.ttf", 72)
        font_sub = ImageFont.truetype("Inter-Medium.ttf", 40)
    except IOError:
        font_big = ImageFont.load_default()
        font_sub = ImageFont.load_default()

    draw.text((150, y_pos + 35), title_text, font=font_big, fill=(255, 215, 0, 255))
    draw.text((150, y_pos + 130), subtitle_text, font=font_sub, fill=(255, 255, 255, 235))
    img.save(output_path, "PNG")
```

### 4.4 Magazine-Cover Text Behind the Speaker's Head (`rembg`)
To place bold title text behind the speaker's head:
1. Extract the frames for that segment.
2. Run `rembg` on each frame to get a foreground alpha cutout of the speaker (`fg_%04d.png`).
3. Layer in order: `(1) Original Background Frame` $\rightarrow$ `(2) Big Bold Headline Text (y ≈ 320–500)` $\rightarrow$ `(3) Speaker Foreground Cutout`.

### 4.5 Punch-In Zooms (Camera Life)
Alternate kept segments between two framings so jump cuts feel intentional and energetic:
* **100% Base Framing (`1080x1920`):**
  `scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920`
* **108% Punch-In Framing (Centered on Face):**
  `scale=1166:2074:force_original_aspect_ratio=increase,crop=1080:1920:43:77`
  *(Adjust `crop` X/Y offsets based on OpenCV face detection so the speaker's eyes stay in the upper-middle third).*

---

## Step 5: Word-Timed ASS Captions (`edit/captions.ass`)

Burn in dynamic word-by-word captions using the Advanced SubStation Alpha (`.ass`) format.

### 5.1 Caption Chunking & Formatting Rules
1. **2 to 4 Words Per Chunk:** Split chunks at natural breath or phrase boundaries.
2. **No Dangling Articles:** Never end a caption chunk on `"the"`, `"a"`, `"an"`, `"to"`, or `"of"`. Push those words to the start of the next chunk.
3. **Lower-Third Safe Position:** Place captions at `MarginV: 420` (`y ≈ 1380–1480` on a `1080x1920` frame)—always below the chin, never over the mouth, and safely above the `y = 1500` Instagram bottom UI zone.
4. **No Duplicate On-Screen Text:** Whenever a large full-screen graphic or hook headline displays the exact same words being spoken, suppress/mute the lower-third captions for those timestamps so the screen never says the same thing twice.
5. **BGR Color Encoding Warning:** ASS color codes use **`&HBBGGRR&`** (Blue-Green-Red), **NOT** RGB!
   * Gold (`#FFD700` RGB) $\rightarrow$ **`&H00D7FF&`** in ASS.
   * Neon Green (`#00FF66` RGB) $\rightarrow$ **`&H66FF00&`** in ASS.
   * Pure White (`#FFFFFF` RGB) $\rightarrow$ **`&HFFFFFF&`** in ASS.

### 5.2 Automated ASS Generator Script (`edit/generate_ass.py`)
Use this script to convert your retimed word timestamps (after cuts are applied) into a word-highlighted `.ass` file:

```python
# edit/generate_ass.py
import json

ASS_HEADER = """[Script Info]
ScriptType: v4.00+
PlayResX: 1080
PlayResY: 1920
WrapStyle: 0
ScaledBorderAndShadow: yes

[V4+ Styles]
Format: Name, Fontname, Fontsize, PrimaryColour, SecondaryColour, OutlineColour, BackColour, Bold, Italic, Underline, StrikeOut, ScaleX, ScaleY, Spacing, Angle, BorderStyle, Outline, Shadow, Alignment, MarginL, MarginR, MarginV, Encoding
Style: Default,Inter,78,&H00FFFFFF,&H0000D7FF,&H00000000,&H80000000,-1,0,0,0,100,100,0,0,1,5,2,2,80,80,420,1

[Events]
Format: Layer, Start, End, Style, Name, MarginL, MarginR, MarginV, Effect, Text
"""

DANGLE_WORDS = {"the", "a", "an", "to", "of", "in", "on", "for", "and", "or"}

def fmt_ass_time(seconds):
    h = int(seconds // 3600)
    m = int((seconds % 3600) // 60)
    s = seconds % 60
    return f"{h}:{m:02d}:{s:05.2f}"

def chunk_words(words, max_words=3):
    chunks = []
    current = []
    for w in words:
        current.append(w)
        # Check if we hit max_words or natural punctuation
        ends_punct = w["word"].endswith((".", ",", "!", "?", ";", ":"))
        is_dangle = w["word"].lower().strip(".,!?") in DANGLE_WORDS
        if (len(current) >= max_words and not is_dangle) or ends_punct or len(current) >= 4:
            chunks.append(current)
            current = []
    if current:
        chunks.append(current)
    return chunks

def generate_ass(retimed_words, output_ass_path="edit/captions.ass", highlight_bgr="&H00D7FF&"):
    chunks = chunk_words(retimed_words, max_words=3)
    dialogue_lines = []

    for chunk in chunks:
        for idx, active_w in enumerate(chunk):
            t_start = fmt_ass_time(active_w["start"])
            # Extend active highlight until next word in chunk starts
            if idx + 1 < len(chunk):
                t_end = fmt_ass_time(chunk[idx + 1]["start"])
            else:
                t_end = fmt_ass_time(active_w["end"])

            rendered_tokens = []
            for j, w in enumerate(chunk):
                clean_text = w["word"]
                if j == idx:
                    rendered_tokens.append(f"{{\\c{highlight_bgr}}}{clean_text}{{\\c&HFFFFFF&}}")
                else:
                    rendered_tokens.append(clean_text)

            line_text = " ".join(rendered_tokens)
            dialogue_lines.append(f"Dialogue: 0,{t_start},{t_end},Default,,0,0,0,,{line_text}")

    with open(output_ass_path, "w", encoding="utf-8") as f:
        f.write(ASS_HEADER + "\n".join(dialogue_lines) + "\n")

if __name__ == "__main__":
    with open("edit/retimed_words.json", "r", encoding="utf-8") as f:
        words = json.load(f)
    generate_ass(words)
    print("Generated edit/captions.ass")
```

---

## Step 6: Assembly, Color Preservation & Audio Normalization

### 6.1 HDR-to-SDR Tone Mapping & Color Preservation
* **iPhone HDR Check:** Inspect the source video color space first:
  ```bash
  ffprobe -v error -select_streams v:0 -show_entries stream=color_space,color_transfer,color_primaries -of default=noprint_wrappers=1 "raw/input.mp4"
  ```
* If `color_transfer=arib-std-b67` (HLG) or `smpte2084` (PQ), tone-map cleanly to standard SDR (`bt709`) before assembling:
  ```bash
  ffmpeg -y -i "raw/input.mp4" \
    -vf "zscale=t=linear:npl=100,format=gbrpf32le,zscale=p=bt709,tonemap=tonemap=hable:desat=0,zscale=t=bt709:m=bt709:r=tv,format=yuv420p" \
    -c:v libx264 -crf 16 -preset fast -c:a copy edit/input_sdr.mp4
  ```
* **Strict No-Filter Rule:** Never apply LUTs, artificial warming, contrast curves, or skin-smoothing filters unless the user explicitly asks for them.

### 6.2 Segment Cutting, Micro-Fades & Concatenation (`filter_complex`)
For each kept segment $i \in \{0, \dots, N-1\}$ with snapped bounds `[start_i, end_i]` and duration $d_i = \text{end}_i - \text{start}_i$:
* **Video Trim & Zoom:**
  * Even segments (100% scale): `trim=start={start_i}:end={end_i},setpts=PTS-STARTPTS,scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920`
  * Odd segments (108% zoom): `trim=start={start_i}:end={end_i},setpts=PTS-STARTPTS,scale=1166:2074:force_original_aspect_ratio=increase,crop=1080:1920:43:77`
* **Audio Trim & Anti-Click Micro-Fades (`10ms` in, `40ms` out):**
  `atrim=start={start_i}:end={end_i},asetpts=PTS-STARTPTS,afade=t=in:st=0:d=0.01,afade=t=out:st={d_i - 0.04}:d=0.04`

### 6.3 Master Render with ASS Captions & `-14 LUFS` Audio Normalization
Burn in `edit/captions.ass`, composite PNG/video overlays, normalize integrated loudness to `-14 LUFS` (`-1.0 dBTP` true peak), and encode to H.264 High Profile (`yuv420p`, `30 fps`, `48 kHz AAC`):

```bash
ffmpeg -y -i edit/assembled_rough.mp4 \
  -vf "ass=edit/captions.ass" \
  -af "loudnorm=I=-14:TP=-1.0:LRA=11" \
  -c:v libx264 -profile:v high -crf 18 -preset fast -pix_fmt yuv420p -r 30 \
  -c:a aac -b:a 192k -ar 48000 \
  -movflags +faststart \
  edit/final.mp4
```

* **If Background Music Is Requested:** Mix music at `-24 dB` under the normalized voice track, and **always export two files**: `edit/final.mp4` (with music) and `edit/final_clean.mp4` (voice only).
* **Extract Cover Frame:**
  ```bash
  ffmpeg -y -i edit/final.mp4 -ss 00:00:00.500 -vframes 1 -q:v 2 edit/cover.jpg
  ```

---

## Step 7: Automated Quality Control (Check Your Own Work)

**Never show `edit/final.mp4` to the user until all 3 verification checks pass.**

### 7.1 Visual Frame & Safe-Zone Inspection (`1080x1920` Canvas)
Extract verification frames at every cut point and every visual overlay:
```bash
ffmpeg -y -i edit/final.mp4 -vf "fps=2" edit/qc_frame_%03d.jpg
```
Visually inspect the extracted frames against the `1080x1920` Instagram/TikTok/Shorts safe-zone grid:

```text
+---------------------------------------+ y = 0
|        TOP UI UNSAFE ZONE             |
|     (Reels Camera / Top Bar)          |
|   NO TEXT OR GRAPHICS (y < 250)       |
+---------------------------------------+ y = 250
|   |                               |   |
| x |       SAFE CONTENT AREA       | x |
| < |      (x: 60 to 930/1020)      | > |
| 60|                               |1020
|   |   Speaker Face & Upper Body   |   |
|   |                               |---+ y = 1000
|   |                               | R |
|   |   Captions Zone:              | I | Right Icon
|   |   y = 1300 to 1480            | G | Column
|   |   (Below chin, never on mouth)| H | (Likes/Share)
|   |                               | T | x > 930
+---+-------------------------------+---+ y = 1500
|       BOTTOM UI UNSAFE ZONE           |
|  (Username, Caption, Audio Marquee)   |
|   NO TEXT OR GRAPHICS (y > 1500)      |
+---------------------------------------+ y = 1920
```

**Checklist:**
* [ ] **No Face Occlusion:** No caption or graphic covers the speaker's eyes, nose, or mouth.
* [ ] **Top Safe Zone:** Nothing important sits above `y = 250`.
* [ ] **Bottom Safe Zone:** Nothing important sits below `y = 1500` (`1520` max).
* [ ] **Right Icon Column:** Nothing sits in `x > 930` between `y = 1000` and `y = 1500`.
* [ ] **Horizontal Edge Margins:** No text clips left of `x = 60` or right of `x = 1020`.
* [ ] **Overlay Readability:** Every graphic/text card remains on screen for at least `1.0s to 1.5s` and is legible at phone screen size.

### 7.2 Re-Transcription Integrity Verification
Run `faster-whisper` on the rendered `edit/final.mp4` and compare the output word-for-word against the approved Cleaned Script:
* Confirm **zero doubled sentences** (no accidental retake left in).
* Confirm **zero clipped words** (no missing first or last syllables at cut joins).

### 7.3 Final Audio Gap Verification
Run an RMS silence check on `edit/final.mp4` to verify that **no silent gap exceeds `0.25s`** anywhere between sentences. If any check in 7.1, 7.2, or 7.3 fails, fix the coordinates or cut bounds, re-render `edit/final.mp4`, and re-verify before presenting to the user.

---

## Step 8: Hand-Off & Continuous Learning Loop

### 8.1 Final Hand-Off Package
Once QC passes, present the following to the creator:
1. **Final Video Path:** `edit/final.mp4` (plus `edit/final_clean.mp4` if music was mixed).
2. **Cover Frame Path:** `edit/cover.jpg`.
3. **Quality Control Report:** Max audio gap measured (e.g., `0.18s`), final duration, and safe-zone pass confirmation.
4. **3 On-Screen Hook Text Options:** Short, punchy 3–6 word cover/hook titles.
5. **Ready-to-Post Instagram Caption:**
   * Line 1: High-curiosity hook sentence.
   * Body: Short, single-sentence lines with blank lines between paragraphs.
   * Ending: Clear Call-to-Action (no hashtags unless explicitly requested).

### 8.2 Taking Revision Notes & Updating `Learned Rules`
When the creator gives feedback like a human editor (e.g., *"make captions bigger"*, *"cut faster in the first 5 seconds"*, *"put my app screenshot at 0:12"*, *"less zooming"*):
1. Apply the exact adjustment, re-render `edit/final.mp4`, and re-run the Step 7 QC checks.
2. Append the creator's preference as a concise, permanent one-line rule under **`## Learned Rules`** at the bottom of this `SKILL.md` file (and sync to `~/.claude/skills/edit-reel/SKILL.md` if running locally in Claude Code) so every future video automatically follows it without being asked again.

---

## Common Gotchas & Troubleshooting

* **Whisper Timestamp Drift (`50–300 ms`):** Never slice video/audio directly using raw `faster-whisper` word start/end times. Always run `snap_cuts.py` against the 10 ms WAV RMS envelope.
* **Audible Pops/Clicks at Cut Points:** Concatenating trimmed audio streams without micro-fades causes zero-crossing discontinuities. Always include `afade=t=in:st=0:d=0.01` and `afade=t=out:st=...:d=0.04` on every audio segment.
* **Wrong Highlight Color (Blue Instead of Gold):** Remember that `.ass` subtitles use `&HBBGGRR&` byte order. Gold `#FFD700` is `&H00D7FF&`, not `&HFFD700&`.
* **Caption Font Not Found by FFmpeg `ass` Filter:** Ensure the font specified in `Style: Default,<Fontname>` is installed in the system font directory, or use `subtitles=edit/captions.ass:fontsdir=assets/fonts/` to load a local `.ttf` file directly.

---

## Learned Rules

- Keep all captions and key overlays strictly outside the top 250px (`y < 250`), bottom 400px (`y > 1500`), and right-hand UI icon column (`x > 930, y: 1000..1500`) on a 1080x1920 vertical frame.
- Snap every cut-in (0.05s lead) and cut-out (0.07s tail) to the 10 ms audio RMS envelope and apply 10 ms fade-in / 40 ms fade-out so joins never clip words or click.
- Compress internal pauses >= 0.14s down to ~0.12s and ensure no gap anywhere in the finished reel exceeds 0.25s.
- Alternate 100% and ~108% punch-in zooms across cuts while keeping the speaker's face centered.
- Mute lower-third captions whenever a large on-screen graphic displays the exact same words.
- Never apply LUTs, color filters, or skin-tone modifications to source footage unless explicitly asked.